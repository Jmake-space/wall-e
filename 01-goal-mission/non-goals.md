# Wall-E — Non-goals

Explicit boundaries, so the project doesn't sprawl. Anything here is out of
scope unless the team formally moves it in.

## Not a payment gateway

Wall-E rides existing rails — Zelle, UPI/BHIM, Coinbase, Trustly, bank
autopay. It never becomes its own rail, ledger, or money transmitter.

## Not a bank, wallet, or investment advisor

The "Wealthfront agent" / "Wallet Muse" framing is about *orchestrating*
money flow, not holding custody or giving financial advice.

## Not a credential vault

Wall-E never stores bank logins or passwords. Bank access goes through
Plaid tokenized integration only. How credentials are handled was an open
question in the brainstorm (Jaivir's pushback) — the answer is: it never
touches them.

## No autonomous money movement at MVP

Execution requires explicit human approval. The agent proposes, surfaces
constraints (like staked SOL needing 2 hours to unstake), and waits. Removing
the approval gate is a separate, later decision with its own threat model.

## US-first

India (UPI/BHIM design, local rails) is explicitly deprioritized. "Build this
for US, 100x." India stays TBD.

## Not a general-purpose agent

Wall-E does money management: recurring payments, fraud prevention, payment
execution with audit. It doesn't try to be everything Muse is.
