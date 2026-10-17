# ADR 0004 — US-first ("100x"); India TBD

## Context

The brainstorm started with both a Zelle agent and a UPI/BHIM agent. Jaideep
closed the question: "For India we will have to see. But who cares about
India. Build this for US. 100x."

## Decision

Build for the US first. Plaid covers US banks; rails at MVP are US rails
(Zelle-style, Coinbase, Trustly). UPI/BHIM gets an integration *pattern*
defined in v1 so the adapter interface doesn't assume US-only — but no
India build until the US product is trusted.

## Consequences

- **Good:** One regulatory regime, one integration story (Plaid), faster to
  a trusted MVP.
- **Bad:** The UPI/BHIM idea from the thread stays on the shelf; if the
  adapter interface bakes in US assumptions, India gets harder later.
- **Neutral:** "100x" is a direction, not a plan — the v1 scope still needs
  the team to define what US scale actually means.
