# Wall-E — High-Level Design

## Components

**Agent core** — the decision-maker. Reads state (balances, history, due
dates), proposes payments, surfaces constraints, and waits for approval.
Never moves money on its own at MVP.

**Plaid connector** — the only path to bank/card data. Tokenized integration;
Wall-E never sees or stores bank logins or passwords. Reads 30 days of
transactions, stores 12 months.

**Rail adapters** — one adapter per payment rail, each wrapping an existing
gateway (never a Wall-E-built rail):
- Zelle-style bank transfers (US)
- Coinbase (crypto: SOL, USDC, staking/unstaking)
- Trustly (bank payments)
- UPI/BHIM pattern (India — TBD, deprioritized)

MVP ships one adapter; the interface is uniform so more rails plug in later.

**Auth + identity** — proves who is asking. MFA at MVP, evolving to 3FA/4FA
for high-stakes actions. Every request — human or agent — carries identity.

**Guardrails** — policy checks before any proposal or execution: recipient
verification, amount sanity, fraud signals, rail availability. Unverifiable
requests are refused, loudly.

**Audit log** — tamper-evident record of every decision, approval, and
movement. 100% coverage is an MVP goal.

**Notifier** — tells the user when something needs them: approval requests,
constraint updates ("unstaking done, ready for your approval").

## Data flow

```
Human/agent request
  → Auth + identity (who is this?)
  → Agent core (what's the state? balances, history, due dates)
  → Plaid connector (bank data) / Rail adapter (rail state, e.g. staked SOL)
  → Guardrails (is this verifiable? any fraud signal?)
  → Proposal + constraints surfaced to user
  → Human approval (the gate — nothing moves without it)
  → Rail adapter executes
  → Audit log records everything
  → Notifier confirms
```

## Canonical sequence — the Solana dialogue

The approval pattern every rail adapter follows, from the thread:

1. **Jaivir:** "Hey Wall-E, it's me Jaivir — can you send Jaideep $100 of
   Solana? I have my wallet on my iPhone and some Solana in Coinbase. If
   it's short, just convert some USDC and use that."
2. **Wall-E checks state:** Coinbase adapter reports SOL is staked; Plaid/iPhone
   wallet balances checked.
3. **Wall-E surfaces the constraint:** "I see the Coinbase SOL is staked —
   unstaking takes about 2 hours. I'll start that now."
4. **Wall-E acts within allowance:** starts the unstake (reversible, no money
   moved to a recipient).
5. **Wall-E notifies:** "Unstaking is done — ready for your approval to send
   $100 of SOL to Jaideep."
6. **Jaivir approves.** Wall-E executes via the Coinbase adapter.
7. **Audit log** records: request, identity, balances seen, constraint,
   approval, execution, result.

The shape to preserve: check real state → surface constraints the user didn't
know about → act only within allowance → stop for approval → execute → log.

## What's deliberately not here

[DRAFT PLACEHOLDER — needs the team.]

- Exact API shapes between components.
- Where state lives (database choice, hosting).
- The 3FA/4FA mechanism design (tap, voice, hardware key — open question
  from goals.md).
- How the "1800 number" endpoint is exposed (API, voice, chat — TBD).
