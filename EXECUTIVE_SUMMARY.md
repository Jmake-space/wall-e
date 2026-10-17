# Wall-E — Project Executive Summary

**Date:** October 17, 2026
**Source:** WhatsApp brainstorm — Jaideep Bir, Karan Singh, Jaivir Khurana
**Status:** Planning — repo scaffolded, 11 planning tracks open

## Vision

An AI wallet and money-management agent that owns the whole money flow —
salary → bank → autopay — instead of today's single dumb autopay step.
Wall-E manages recurring payments (cleaning lady, landscaping, family
transfers, credit cards), prevents fraud, and can **execute** payments, not
just supervise them. Think "Wealthfront agent" / "Wallet Muse".

Related sparks from the thread: a Zelle Agent and a UPI/BHIM Agent
(Coinbase has built one too).

## How it works — example from the thread

> Jaivir: "Hey Wall-E, it's me Jaivir, can you send Jaideep $100 of Solana?
> I have my wallet on my iPhone and some Solana in Coinbase. If it's short,
> just convert some USDC and use that."
>
> Wall-E: "Sure Jaivir, I see that Coinbase has some SOL but it's staked, so
> I'll unstake it now — that will take 2 hours to be available. I'll notify
> you when it's ready so you can approve the transfer before I execute."

Note the shape of the interaction: Wall-E sees across accounts, plans around
constraints (staking lockup), and executes only after explicit approval.

## Trust is the product

Wall-E is distributed as an installable/importable "skill": install,
authenticate, authorize — then transact without losing trust, in fact
gaining it. Security pillars:

- **Zero Fraud** — fraud prevention is a core feature, not a checkbox
- **MFA evolving to 3FA/4FA**
- **Provenance** — every action traceable to its source
- **SOC2** compliance
- **Audit trail** — full observability of every decision and transaction

## Architecture (agreed)

- **Not a payment gateway.** Use existing rails: Zelle, UPI/BHIM, Coinbase,
  Trustly.
- Built as a **service/endpoint** (like an 1800 number) reachable by any agent
  or human: AI + MCP + Guardrails + Auth/Identity + Observability + Audit Trail.
- **Bank & card integration via Plaid (US):** read the last 30 days of
  incoming/outgoing transactions; keep 12 months of records.
- **US market first ("100x")**; India TBD and deprioritized.

## Open questions

1. How bank logins/passwords are handled securely (raised by Jaivir) — to be
   designed around Plaid.
2. What blocks today's Muse from doing this — the gap Wall-E fills.

## Planning tracks

The 11 numbered folders in this repo map to the planning tracks: goal/mission,
scope (MVP → capabilities → BRD → PRD), HLD, execution plan (milestones,
dependencies, threat model/risks), policies & governance, dev schedule +
architecture decisions, operational model, tools & integrations, ownership &
RACI, data protection, finance & cost management.

## Action items

1. Create GitHub repo, raise a PR, share with the team for review (Jaideep).
2. Draft the Goal / Mission doc.
3. Define scope: MVP → capabilities → BRD → PRD.
4. Write the project HLD.
5. Execution plan: high-level milestones, dependencies, threat model / risks.
6. Policies and governance model.
7. Development schedule + architecture decisions.
8. Operational model.
9. Tools and integrations (Plaid for US banks; India approach TBD).
10. Ownership and RACI tree.
11. Data protection plan.
12. Finance and cost management.
13. Each team member: test with 12 months of bank statements (a dormant account is fine).
