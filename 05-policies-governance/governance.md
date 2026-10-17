# Wall-E — Governance: Decision Rights and Value Alignment

Who decides what, and how we stay pointed at the mission.

## Decision rights

[DRAFT PLACEHOLDER — the team hasn't assigned these; proposed starting
point below.]

- **Scope and money decisions** (what's in/out of MVP, budget, rail
  choices): Jaideep Bir has final call — it's his pitch and his risk.
- **Technical design** (HLD, ADRs, component choices): whoever authors the
  track proposes; all three review; Jaideep breaks ties.
- **Security exceptions** (anything touching the approval gate, auth, or
  token handling): unanimous. One "no" stops it until the threat model is
  updated.
- **Day-to-day code**: PR review by at least one other team member.

## Value alignment

The mission is the constitution (`01-goal-mission/mission.md`): own the
money flow, trust as the product, human approval before execution. When a
decision is close:

1. Does it make fraud harder or easier? Harder wins.
2. Does it keep the human in the loop? It must, at MVP.
3. Does it keep Wall-E off the money-transmitter hook? Not a gateway, no
   custody — always.

If a proposal fails any of the three, it doesn't ship without a written
exception and a new threat-model entry.

## Changing the plan

- The 11 tracks are the plan. Changing scope, milestones, or a non-goal
  requires updating the doc and getting team review — same as code.
- Non-goals stay non-goals unless the team formally moves them in
  (`01-goal-mission/non-goals.md`).

## Cadence

[DRAFT PLACEHOLDER — review rhythm needs the team: weekly sync? async PR
reviews only?]
