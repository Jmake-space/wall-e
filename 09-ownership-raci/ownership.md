# Wall-E — Code Ownership

[DRAFT PLACEHOLDER — rules proposed; the team confirms.]

## The rule

Every directory has an owner. The owner reviews every PR touching it. No
orphan code.

## Proposed ownership

| Area | Owner |
|---|---|
| Agent core, guardrails | [DRAFT PLACEHOLDER] |
| Plaid connector | [DRAFT PLACEHOLDER] |
| Rail adapters (Zelle, Coinbase, Trustly) | [DRAFT PLACEHOLDER] |
| Auth + identity, 3FA/4FA | [DRAFT PLACEHOLDER] |
| Audit log | [DRAFT PLACEHOLDER] |
| Notifier, endpoint | [DRAFT PLACEHOLDER] |
| Planning docs (this repo) | shared — all three review |

## Mechanics

- CODEOWNERS file once there's code to own (not yet — this repo is docs).
- Owner approval required before merge on their area; one other reviewer
  minimum everywhere.
- Ownership follows the RACI (`raci.md`): the R for a track owns its code.
- If an owner is unavailable, Jaideep reassigns — code never waits on one
  person silently.
