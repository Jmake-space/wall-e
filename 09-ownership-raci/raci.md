# Wall-E — RACI

[DRAFT PLACEHOLDER — the team hasn't assigned roles; this is a proposed
starting point for them to correct. Jaideep = Jaideep Bir, Karan = Karan
Singh, Jaivir = Jaivir Khurana. R = responsible (does it), A = accountable
(final call), C = consulted, I = informed.]

| Track / decision | Jaideep | Karan | Jaivir |
|---|---|---|---|
| 01 Goal/mission | A | C | C |
| 02 Scope (MVP/BRD/PRD) | A | R | C |
| 03 HLD | C | R | A |
| 04 Execution plan + threat model | A | R | R |
| 05 Policies + governance | A | C | R |
| 06 Schedule + ADRs | A | R | C |
| 07 Operational model | C | R | A |
| 08 Tools + integrations | C | A | R |
| 09 Ownership + RACI | A | I | I |
| 10 Data protection | A | C | R |
| 11 Finance + costs | A | I | C |
| GitHub repo + PRs | A | R | R |
| Security exceptions (approval gate, auth, tokens) | A | C | C — unanimous required (see `05-policies-governance/governance.md`) |
| MVP rail choice | A | R | C |
| 3FA/4FA design | C | C | R |

Notes:
- One A per row. Where Jaideep is A, he's the tiebreaker.
- Karan was tagged into the brainstorm but hasn't weighed in yet — his
  columns are guesses until he does.
- Revisit this table once M0 (statements test) is done and real work
  starts.
