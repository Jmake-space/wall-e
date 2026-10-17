# ADR 0001 — Plaid tokenized integration for US bank/card access

## Context

Wall-E needs to read bank and credit-card transactions: 30 days of
incoming/outgoing, 12 months of records. Jaivir's pushback in the brainstorm
was direct: "How does it handle bank logins/passwords?" Building our own
bank integrations means touching credentials — the exact thing that would
destroy trust.

## Decision

Use Plaid for all US bank/card integration. Tokenized access only: Plaid
holds the credentials, Wall-E holds tokens. Wall-E never sees, stores, or
transmits a bank login or password.

## Consequences

- **Good:** No credential vault to build or breach; answers Jaivir's
  question with architecture, not promises; Plaid covers "all US banks"
  (fetch accounts, cards, loans).
- **Bad:** Plaid is a hard dependency — pricing, coverage, and API changes
  are outside our control (see `04-execution-plan/threat-model.md`).
- **Neutral:** Tokens need encrypted storage, least-privilege scopes, and
  rotation — that design is still open.
