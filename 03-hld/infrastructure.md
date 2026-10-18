# Wall-E — Infrastructure & Deployment (GitHub Actions + Terraform)

Companion to `deployment-flow.svg`. All automation lives in GitHub Actions;
all infrastructure lives in Terraform. No click-ops: every environment change
is a pull request.

## Pipeline

PR → GHA CI → human review → merge to main → GHA build (containers +
function bundles, in parallel) → registries → GHA deploy
(`terraform apply`) → dev/staging auto → human approval → production.

See `architecture.svg` (network zones, service accounts) and
`access-model.svg` (auth flows, least-privilege grants).

## Network

One VPC, three tiers. [DRAFT PLACEHOLDER — cloud provider not chosen;
names below are the intent, not the product.]

- **Public subnets** — internet ingress only. The API Gateway lives here
  (behind the cloud load balancer). Security group: 443 in from the
  internet, nothing else.
- **Private subnets** — all workloads: the 4 microservices (gateway is
  public; here: agent core, auth, audit writer) and the 4 function workers
  (plaid connector, rail adapters, guardrails, notifier). No inbound from
  the internet. Outbound to third-party APIs (Plaid, Coinbase, Trustly,
  notification providers) goes via NAT egress.
- **Isolated subnets** — data only: audit store, transaction store, token
  vault. No internet route at all, inbound or outbound. Security groups
  allow only the workload security groups, on the store ports.

Default-deny everywhere; every allow is an explicit security-group rule
between named tiers.

## Auth

- **Humans** — MFA (TOTP / WebAuthn) at MVP; step-up to 3FA/4FA for
  high-stakes approvals. Auth + Identity issues short-lived session tokens;
  the gateway validates every request.
- **Agent clients** — mTLS + API key, scoped to what the agent may ask for.
- **Service to service** — every component runs as its own service account
  (badges on the architecture diagram), mutual TLS with short-lived SA
  tokens. No shared credentials.
- **GHA → cloud** — OIDC federation; GitHub Actions assumes a
  per-environment deploy role. No long-lived cloud keys in repo secrets.
  The production role is only assumable after the GitHub Environment
  approval.

## Service accounts & grants

Least privilege, and separation of duties as a design rule:

| SA | Token Vault | Txn Store | Audit Store | External APIs |
|----|-------------|-----------|-------------|---------------|
| sa-gateway | — | — | — | — |
| sa-core | DENY | read | via writer | — |
| sa-auth | — | — | — | — |
| sa-plaid | read/write, scoped | write | — | Plaid API |
| sa-rails | DENY | DENY | — | rail APIs |
| sa-guardrails | — | read | — | — |
| sa-notify | — | — | — | notify providers |
| sa-audit | — | — | append only | — |

The component that reads money (sa-plaid) cannot move it; the component
that moves it (sa-rails) cannot read it; the component that decides
(sa-core) can touch neither directly — it works through workers, and every
step is audited. Only sa-plaid can read the Token Vault, and only the
tokens it needs.

## GitHub Actions — `.github/workflows/`

**`ci.yml`** — runs on every PR. Required checks before merge:
- lint + unit tests
- payment-path tests — any change touching a payment path must be covered
- secret scanning (no credentials in code, ever)

**`build.yml`** — runs on merge to main. Matrix build:
- container images → container registry: `gateway`, `agent-core`,
  `auth`, `audit-writer`
- function bundles → function registry: `plaid-connector`, `rail-adapters`,
  `guardrails`, `notifier`
- tags are immutable and content-addressed; the same artifact is promoted
  through environments, never rebuilt between them

**`deploy.yml`** — runs on build success and on manual dispatch:
- `terraform plan` always runs; the plan is attached to the run
- dev/staging: auto-apply on merge
- production: applies only after approval in the `production` GitHub
  Environment (a human clicks approve)
- every deploy writes an audit entry: who, when, what versions

Auth to the cloud is via OIDC — no long-lived keys sitting in repo secrets.
[DRAFT PLACEHOLDER — cloud provider and OIDC roles not chosen yet.]

## Terraform — `infra/`

```
infra/
  main.tf  variables.tf  outputs.tf
  modules/
    network/      # VPC, subnets, security groups [PLACEHOLDER]
    containers/   # gateway, agent-core, auth, audit-writer services
    functions/    # plaid-connector, rail-adapters, guardrails, notifier
    data/         # audit store, transaction store, token vault
    dns/          # [PLACEHOLDER]
  envs/
    dev.tfvars  staging.tfvars  prod.tfvars
```

- Remote state with locking. [DRAFT PLACEHOLDER — backend follows the cloud
  decision.]
- Promotion between environments = promoting artifact versions via tfvars.
- Secrets live in the cloud secret manager. Plaid tokens live **only** in
  the Token Vault — never in Terraform state, variables, or outputs
  (mark all token-adjacent values `sensitive`).

## Environments

- **dev** — for development; may be ephemeral.
- **staging** — prod-like; auto-deploys on merge; the last gate before prod.
- **prod** — manual approval only; rollback is `terraform apply` of the
  previous known-good versions (see the rollback path in
  `deployment-flow.svg`).

## Open

Cloud platform, container registry, function platform, state backend, DNS —
all [DRAFT PLACEHOLDER]. Decided together with the ADR 0005 follow-up; none
of it blocks the planning docs.
