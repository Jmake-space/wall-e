# Wall-E — Operational Model

How Wall-E runs as a service/endpoint ("1800 number") that any agent or
human can reach.

## The service shape

One endpoint, reachable by humans and agents alike. Every call carries
identity; every call is authenticated. There is no back door, no
unauthenticated mode, no "just this once" bypass.

[DRAFT PLACEHOLDER — transport, hosting, and API shape need the team.]

## Observability

- **Audit trail**: every decision, approval, and movement recorded,
  tamper-evident, 100% coverage (MVP goal). This is the product's memory
  and its proof.
- **Metrics**: the measures from `01-goal-mission/goals.md` — execution
  success rate, fraud incidents (target: 0), false-refusal rate,
  approval-to-execution latency.
- **Logs**: structured; never contain tokens, credentials, or full account
  numbers.
- [DRAFT PLACEHOLDER — tooling choices (what collects metrics/logs/traces)
  need the team.]

## Incident handling

Money-moving incidents get their own playbook:

1. **Freeze**: stop all executions immediately. Proposals can queue; nothing
   moves.
2. **Assess**: audit trail tells us exactly what happened — that's what
   it's for.
3. **Notify**: the account owner is told plainly what happened and what's
   frozen.
4. **Fix and review**: root cause, threat-model update, then unfreeze.

[DRAFT PLACEHOLDER — the full runbook, severity levels, and who gets paged
need the team.]

## On-call

[DRAFT PLACEHOLDER — rotation, paging policy, and escalation path need the
team. With three people, this needs to be explicit early: Wall-E watches
money, so "we'll check it Monday" isn't an option once real payments flow.]

## Change management

- Deploys go through the same PR review as code (`05-policies-governance/policies.md`).
- Anything touching the approval gate, auth, or token handling gets the
  unanimous-review rule from `05-policies-governance/governance.md`.
- [DRAFT PLACEHOLDER — deploy cadence and rollback procedure need the team.]
