# Wall-E — Diagrams

Three views of the same system. Colors are consistent across all of them:

| Color | Meaning | Examples |
|-------|---------|----------|
| Blue | **Microservice** — long-running container | API Gateway, Agent Core, Auth + Identity, Audit Writer |
| Amber | **Serverless worker** — event-triggered function | Plaid Connector, Rail Adapters, Guardrails, Notifier |
| Purple | **External integration** — someone else's system | Plaid API, bank rails, Coinbase, Trustly |
| Green | **Data store / registry** | Audit Store, Transaction Store, Token Vault |
| Gray | People and pipeline steps | Human, CI, deploy stages |

The microservice / serverless split is a proposal, not a final call — see
`06-schedule-adr/adr/0005-microservice-serverless-split.md` and
`06-schedule-adr/adr/0006-gha-terraform-delivery.md` for the reasoning and
what's still open (hosting platform, cold-start mitigation, state backend).

## The diagrams

- **`architecture.svg`** — the static shape: clients, edge, core services,
  integration workers, external rails, and data stores, with the main
  call paths. Dashed bands are network zones (public / private / isolated);
  dark badges are the components' service accounts. Read this first.
- **`access-model.svg`** — auth flows (human MFA, agent mTLS, GHA OIDC) and
  the service-account least-privilege matrix, including the explicitly
  denied paths that enforce separation of duties.
- **`data-flow.svg`** — the dynamic shape: one payment end to end, numbered
  step by step. Uses the Solana example from the original thread
  (staked SOL → unstake → notify → approve → execute). Solid arrows are
  requests/commands, dashed arrows are responses/notifications. The approval
  gate (steps 20–21) is the only path to execution — nothing moves without it.
- **`deployment-flow.svg`** — how code ships: PR → GitHub Actions CI → review →
  merge → parallel builds (containers + function bundles) → dev/staging
  auto-deploy → human approval → `terraform apply` to production, with
  rollback path. Spec in `infrastructure.md`; decision in ADR 0006.

## Conventions

- Every deploy writes an audit entry.
- Payment-path changes need green CI *and* human review.
- Production deploys need explicit human approval.
