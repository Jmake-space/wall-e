# ADR 0002 — Not a payment gateway; ride existing rails

## Context

Jaivir framed it as "an agentic payment gateway with more personal access."
The team decided otherwise: building a gateway means becoming a money
transmitter — licenses, custody, ledgers, and a completely different risk
profile.

## Decision

Wall-E is not a payment gateway. It orchestrates payments through existing
rails via adapters: Zelle-style transfers, UPI/BHIM, Coinbase, Trustly,
bank autopay. It never becomes its own rail, ledger, or money transmitter.

## Consequences

- **Good:** No money-transmitter licensing burden; no custody risk; each
  rail's fraud and compliance machinery stays in place underneath us.
- **Bad:** We're limited by what the rails allow; rail outages or API
  changes hit us (see `04-execution-plan/threat-model.md`).
- **Neutral:** The adapter interface must be uniform enough that adding a
  rail doesn't reshape the core.
