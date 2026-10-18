# ADR 0006 — GitHub Actions + Terraform for delivery

## Context

Wall-E needs CI/CD and infrastructure-as-code from day one: money moves
through this system, so every change to code *and* infrastructure has to be
reviewed, tested, and auditable. The team already lives on GitHub — the repo,
the PRs, the reviews are all there.

## Decision

- **GitHub Actions** for all automation: CI (`ci.yml`), builds (`build.yml`),
  deploys (`deploy.yml`). GitHub Environments gate production.
- **Terraform** for all infrastructure: modules per concern
  (`network`, `containers`, `functions`, `data`, `dns`), per-environment
  tfvars, remote state with locking.
- No click-ops. If it isn't in a PR, it doesn't happen.

[DRAFT PLACEHOLDER — cloud provider, registries, and state backend are not
chosen. The module layout is written to survive that decision.]

## Consequences

- **Good:** everything that ships is reviewed, versioned, and in the audit
  trail — which is the whole trust story. One toolchain (GHA + TF) instead
  of three. Promotion-by-version instead of rebuild-between-envs kills a
  whole class of "works in staging" surprises.
- **Bad:** Terraform state is a new operational burden (locking, drift,
  state surgery when modules change). Someone has to own it — see the RACI
  placeholder in `09-ownership-raci/raci.md`.
- **Neutral:** GHA minutes and state storage cost money at scale; tracked in
  `11-finance-costs/costs.md` as a placeholder until the cloud decision lands.
