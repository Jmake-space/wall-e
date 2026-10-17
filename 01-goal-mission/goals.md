# Wall-E — Goals (MVP and v1)

Draft targets, set by the team in the brainstorm's spirit and meant to be
challenged by Jaivir and Karan. Numbers are placeholders until the team
commits to them.

## MVP goals (first shippable)

1. **Connect one US bank account** via Plaid: read last 30 days of incoming
   and outgoing transactions, keep 12 months of records.
2. **List recurring payments** detected from that history (cleaning, bills,
   transfers, cards) — the "what you regularly send" view.
3. **Execute one payment type** end-to-end with explicit human approval
   before money moves, and a full audit entry after.
4. **Zero fraud on the pilot**: every execution verified, provenance
   recorded; any unverifiable request is refused, loudly.
5. **Time to first payment**: a new team member goes from install to first
   approved payment in one sitting.

## v1 goals (after MVP is trusted)

- Multiple rails: Zelle-style transfers, Coinbase crypto, UPI/BHIM
  integration pattern defined (US-first; India TBD).
- Agent-to-agent access: Wall-E as a service/endpoint any agent or human
  can reach, with identity and auth on every call.
- 3FA/4FA live for high-stakes actions; SOC2 audit underway.

## Measures that matter

- Payment execution success rate (target: ≥ 99%).
- Fraud incidents: 0, by design — and a defined response when one is
  attempted.
- False-refusal rate: legit payments the agent refused (should be near 0
  after the pilot; trust means it can act, not just say no).
- Approval-to-execution latency (target: minutes, not hours).
- Every execution has a complete audit entry (target: 100%).

## What's still open

- Which bank to pilot on (a dormant account is fine).
- What exactly counts as approval (tap, voice, hardware key?) — that's the
  3FA/4FA design work.
- Realistic MVP targets: the team calibrates these after the statement test.
