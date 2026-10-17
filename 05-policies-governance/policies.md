# Wall-E — Policies: Engineering Quality Bars

How we keep the code trustworthy. Money-moving code gets stricter rules
than usual.

## Commits and review

- **Conventional commits, always** (`feat:`, `fix:`, `docs:`, `chore:`,
  `refactor:`, `test:`). History must read like a changelog.
- **Every change goes through a PR.** No direct pushes to `main`.
  The team reviews every PR — this was the deal from the start ("raise a PR
  and share with rest of us for review").
- [DRAFT PLACEHOLDER — approval count and merge rules need the team.]

## Payment-path rules

- Any code touching proposal → approval → execution must have tests that
  prove: approval is required, amount/recipient can't change after approval,
  and every execution writes an audit entry.
- [DRAFT PLACEHOLDER — test coverage targets and CI setup need the team.]
- No secrets, tokens, or credentials in code, logs, or chat. Ever.

## Audit-log coverage

- Every decision the agent makes and every cent it moves gets an audit
  entry. 100% coverage is an MVP goal, not an aspiration.
- [DRAFT PLACEHOLDER — tamper-evidence mechanism needs the team.]

## Documentation

- The 11 planning tracks stay current: if a decision changes, its doc
  changes in the same PR.
- ADRs (`06-schedule-adr/adr/`) for every architecture decision, no
  exceptions.

## What stays out of the codebase

- Bank logins and passwords (Plaid tokens only — non-goal).
- Anything that weakens the approval gate. Removing or bypassing human
  approval is a separate, explicit team decision with its own threat model —
  never a drive-by commit.
