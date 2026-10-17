# Wall-E — Infrastructure & Deployment (GitHub Actions + Terraform)

Companion to `deployment-flow.svg`. All automation lives in GitHub Actions;
all infrastructure lives in Terraform. No click-ops: every environment change
is a pull request.

## Pipeline

PR → GHA CI → human review → merge to main → GHA build (containers +
function bundles, in parallel) → registries → GHA deploy
(`terraform apply`) → dev/staging auto → human approval → production.

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
