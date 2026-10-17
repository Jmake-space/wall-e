# Wall-E — Finance and Cost Management

What Wall-E costs to build and run. Numbers are the team's to fill in —
this doc is the shape of the model.

## Cost categories

**Plaid**
- Paid API (from the thread: "there's a paid API — called PLAID").
- [DRAFT PLACEHOLDER — pricing model unknown: per connected account? per
  API call? The team needs Plaid's current pricing before M1. This is the
  biggest variable cost; get the number early.]

**Infrastructure**
- Hosting for the agent core, endpoint, database (12 months of transaction
  records per account), audit-log storage.
- [DRAFT PLACEHOLDER — hosting choice and estimates need the team.]

**Per-payment costs**
- Rail fees: what Zelle/Coinbase/Trustly charge per transaction.
- [DRAFT PLACEHOLDER — fee schedules need research per rail. Coinbase
  spread/fees especially matter for the crypto path.]

**Compliance and legal**
- SOC2 audit costs (aligned vs certified — see `10-data-protection/`).
- Legal read on money-transmitter exposure (see threat model).
- [DRAFT PLACEHOLDER — get quotes before v1.]

**Team**
- Three people, part-time or full-time — [DRAFT PLACEHOLDER.]

## Cost discipline

- Track Plaid + infra spend monthly from M1 onward; the agent that watches
  money should watch its own.
- Per-payment cost must be visible per execution in the audit log's
  metadata — if a rail gets expensive, we see it immediately.
- [DRAFT PLACEHOLDER — budget cap and who approves spend need the team.]

## What "100x" costs

[DRAFT PLACEHOLDER — the US-scale ambition from the thread has no cost
model yet. Don't scale the infra bill before the MVP proves the concept.]
