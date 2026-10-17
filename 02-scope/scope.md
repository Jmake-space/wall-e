# Wall-E — Scope (MVP → capabilities → BRD → PRD)

Action item 3. Built on `01-goal-mission/goals.md` and the WhatsApp brainstorm
(2026-10-17).

## MVP — what's in

The smallest Wall-E that proves the concept:

1. **One Plaid-connected US bank account** — read last 30 days of incoming
   and outgoing transactions; keep 12 months of records.
2. **Recurring-payment view** — "what you regularly send": cleaning lady,
   landscaping, family transfers (Laila), credit cards. Detected from history,
   listed for the user.
3. **One payment type, end-to-end** — execute a single rail's payment with
   explicit human approval before money moves, full audit entry after.
4. **Zero fraud on the pilot** — every execution verified; anything
   unverifiable is refused, loudly.
5. **Human approval before every execution.** No exceptions at MVP.

## MVP — what's out

- More than one bank account or rail.
- Autonomous (approval-free) money movement.
- India / UPI-BHIM integration (deprioritized: "build this for US, 100x").
- Holding custody, giving investment advice, storing bank logins/passwords
  (Plaid tokens only — see `01-goal-mission/non-goals.md`).
- Becoming a payment gateway (rides existing rails).

## Capabilities

| # | Capability | MVP? |
|---|-----------|------|
| 1 | Bank/card connection via Plaid (US) | Yes — one account |
| 2 | Transaction history: 30 days read, 12 months stored | Yes |
| 3 | Recurring-payment detection and listing | Yes |
| 4 | Payment proposal with constraint surfacing (e.g. staked SOL needs 2h to unstake) | Yes |
| 5 | Human approval gate before execution | Yes |
| 6 | Payment execution via rail adapter | Yes — one rail |
| 7 | Fraud checks on every execution | Yes |
| 8 | Notifications (ready-to-approve, constraint updates) | Yes |
| 9 | Audit log of every decision and movement | Yes |
| 10 | Agent-to-agent access (service/endpoint, "1800 number" model) | v1 |
| 11 | 3FA/4FA for high-stakes actions | v1 |
| 12 | Multi-rail (Zelle, Coinbase, Trustly, UPI-BHIM pattern) | v1 |
| 13 | SOC2 audit | v1 |

## BRD outline

[DRAFT PLACEHOLDER — structure proposed; content needs the team.]

1. Business objectives — why Wall-E exists, what "100x US" means.
2. Stakeholders — Jaideep Bir, Karan Singh, Jaivir Khurana; pilot users.
3. Success criteria — the MVP goals from `01-goal-mission/goals.md`.
4. Constraints — Plaid dependency, US-only, approval-gated execution.
5. Risks — see `04-execution-plan/threat-model.md`.
6. Cost envelope — see `11-finance-costs/costs.md`.

## PRD outline

[DRAFT PLACEHOLDER — structure proposed; content needs the team.]

1. Problem statement — autopay is a dumb single step; nobody watches the
   whole salary → bank → payment chain.
2. Users — people whose money moves across more rails than they can track.
3. Functional requirements — the capability table above, MVP column.
4. Non-functional requirements — zero fraud, 100% audit coverage,
   approval-to-execution in minutes, SOC2-aligned controls.
5. UX flows — connect account → review recurring payments → propose →
   approve → execute → audit entry. The Solana dialogue from the thread is
   the canonical example.
6. Acceptance criteria — one approved payment end-to-end on the pilot
   account, with audit entry, zero fraud.
