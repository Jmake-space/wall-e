# Wall-E — Mission

## The mission

Wall-E is an AI wallet agent that owns your whole money flow — salary comes
in, bills and recurring payments go out — and makes every move safely.

Autopay today is a dumb single step: it fires and you hope the money is
there. Wall-E watches the entire chain (salary → bank balance → due date →
payment), prevents fraud, and *executes* payments — with your approval —
instead of just supervising them.

## Who it's for

People whose money moves across more rails than they can keep track of:
cleaning lady, landscaping, family transfers, credit cards — paid through
Zelle, UPI/BHIM, bank autopay, Coinbase, Trustly. The agent doesn't care
which rail a payment uses; it cares that the money is there, the recipient
is right, and nothing looks off.

## Why it has to be built, not just configured

Muse, GPay, and bank autopay already move money one step at a time. What
none of them do is the whole job: reconcile what came in against what must
go out, spot fraud across accounts, and execute a payment safely with
proof. That's the gap Wall-E fills.

## Trust is the product

Wall-E is distributed as an installable skill — install, authenticate,
authorize, transact — so trust is engineered in, not promised in marketing:

- **Zero Fraud** as the design goal: every payment is verified, not assumed.
- **MFA → 3FA/4FA**: authentication that gets stronger as stakes rise.
- **Provenance**: every action records who/what requested it and why.
- **Audit trail**: a complete, tamper-evident record of every move.
- **SOC2-aligned** controls for the whole operation.

Human approval stays in the loop for execution. Wall-E proposes; you
approve; it executes and logs.

## What a good interaction looks like

> Jaivir: "Hey Wall-E, it's me Jaivir — can you send Jaideep $100 of Solana?
> I have my wallet on my iPhone and some Solana in Coinbase. If it's short,
> just convert some USDC and use that."
>
> Wall-E: "Sure Jaivir. I see the Coinbase SOL is staked — unstaking takes
> about 2 hours. I'll start that now and notify you when it's available so
> you can approve the transfer before I execute."

Notice what's happening: it checks real balances, sees a constraint the user
didn't know about, acts within what it's allowed to do, and stops for
approval before moving money. That's the bar.

## Source of truth

This mission was agreed by the team in the Wall-E brainstorm (WhatsApp,
2026-10-17 — the user's pitch, Jaivir's feasibility pushback, the team's
decision). Where this doc and that thread disagree, the thread wins until the
team changes it.
