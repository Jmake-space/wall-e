# ADR 0003 — Human approval before any money movement

## Context

The whole point of Wall-E is that it *executes*, not just supervises. The
question is where the line sits between "agent acts" and "human decides."
The Solana dialogue from the thread shows the intended shape: Wall-E
unstakes (reversible, no recipient) on its own, then stops and waits for
approval before sending.

## Decision

At MVP, no money moves without explicit human approval. The agent proposes,
surfaces constraints, and waits. Approval binds the exact amount and
recipient; execution re-verifies both. Removing this gate is a separate,
later decision with its own threat model — never a drive-by change.

## Consequences

- **Good:** The strongest single defense against fraud, prompt injection,
  and confused-deputy attacks; it's also the trust story ("it can't go
  rogue with your money").
- **Bad:** Friction on every payment; approval fatigue is a real risk
  (mitigation is a UX design task — still open).
- **Neutral:** Reversible, non-recipient actions (like unstaking) may
  proceed without approval; the line is "money moves to someone" = approval
  required.
