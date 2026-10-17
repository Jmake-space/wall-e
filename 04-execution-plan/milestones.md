# Wall-E — Execution Plan: Milestones

[DRAFT PLACEHOLDER — ordering follows the brainstorm's logic; dates and
owners need the team.]

## M0 — Statements test (unblocks everything)

Each team member runs their own 12 months of bank statements through the
concept (a dormant account is fine). Goal: real data to detect recurring
payments against, before any code moves money.

- Depends on: nothing.
- Done when: three statement sets reviewed, recurring-payment patterns
  listed.

## M1 — Plaid connection + history

One US bank account connected via Plaid. Read last 30 days in/out, store
12 months. This is the data foundation.

- Depends on: M0 (know what to look for).
- Done when: transactions flowing, 12-month store populating.

## M2 — Recurring-payment view

"What you regularly send": detect and list recurring payments from history
(cleaning, landscaping, transfers, cards).

- Depends on: M1.
- Done when: the view matches what the user actually sends, by their
  confirmation.

## M3 — First approved payment

One rail adapter, one payment type, end-to-end: propose → approve → execute
→ audit entry. The Solana dialogue is the acceptance test.

- Depends on: M2 (know what to propose), guardrails + audit log (track 04
  threat model, track 03 HLD).
- Done when: a real payment executes on the pilot account with approval and
  a complete audit entry. Zero fraud.

## M4 — Trust hardening

3FA/4FA design for high-stakes actions; guardrail coverage review; SOC2
audit begins.

- Depends on: M3 (real executions to harden against). Runs alongside M5.
- Done when: [DRAFT PLACEHOLDER — criteria need the team.]

## M5 — Service endpoint + more rails

Wall-E as a reachable service ("1800 number"): any agent or human can call
it, identity and auth on every call. Additional rail adapters (Zelle,
Coinbase, Trustly).

- Depends on: M3 (execution proven), M4 (trust proven).
- Done when: [DRAFT PLACEHOLDER — criteria need the team.]

## Dependency map

```
M0 (statements) → M1 (Plaid+history) → M2 (recurring view) → M3 (first payment)
                                                              ├→ M4 (hardening)
                                                              └→ M5 (endpoint+rails)
```

Threat model and risks: `threat-model.md`.
