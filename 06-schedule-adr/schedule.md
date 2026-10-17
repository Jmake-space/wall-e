# Wall-E — Development Schedule

[DRAFT PLACEHOLDER — phases follow the milestone order in
`04-execution-plan/milestones.md`; dates and owners need the team.]

## Phase 0 — Statements test (M0)

Each team member runs 12 months of bank statements (dormant account fine)
through the concept. Output: real recurring-payment patterns to design
against.

## Phase 1 — Data foundation (M1–M2)

Plaid connection for one US account; 30-day read, 12-month store; then the
recurring-payment view. Nothing moves money yet.

## Phase 2 — First payment (M3)

One rail adapter, one payment type, end-to-end with human approval and a
full audit entry. The Solana dialogue is the acceptance test. Guardrails and
audit log ship here, not later.

## Phase 3 — Trust hardening (M4)

3FA/4FA design for high-stakes actions; guardrail coverage review; threat
model revisited with real execution data; SOC2 audit begins.

## Phase 4 — Service + rails (M5)

Wall-E as a reachable endpoint ("1800 number") for any agent or human, with
identity and auth on every call. More rail adapters: Zelle, Coinbase,
Trustly. UPI/BHIM pattern defined but not built (India TBD).

## Rules

- No phase starts until the previous phase's "done" criteria are met
  (see `04-execution-plan/milestones.md`).
- Security work (threat model, guardrails, audit) is in every phase, not a
  phase of its own.
- The approval gate is never "temporarily" removed to hit a date.

## Architecture decisions

Recorded in `adr/` — one file per decision, context / decision /
consequences format.
