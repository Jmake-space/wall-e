# Wall-E — Tools and Integrations

What each integration provides and where it plugs into the HLD
(`03-hld/hld.md`).

## Plaid — bank and card data (US)

- **Provides:** tokenized access to US bank accounts, credit cards, loans;
  transaction history.
- **Plugs into:** the Plaid connector. Reads 30 days in/out, stores
  12 months. The only path to bank data — Wall-E never touches bank
  logins/passwords.
- **Watch:** pricing, coverage gaps, API changes (threat model).

## Zelle — US bank transfers

- **Provides:** bank-to-bank transfers on US rails.
- **Plugs into:** a rail adapter. Candidate for the MVP's single payment
  type [DRAFT PLACEHOLDER — the team picks the MVP rail].

## Coinbase — crypto

- **Provides:** SOL, USDC (and other crypto) balances, transfers, and
  staking/unstaking.
- **Plugs into:** a rail adapter. The canonical Solana dialogue from the
  thread runs through this adapter: check staked state → unstake (2h) →
  notify → approve → execute.

## Trustly — bank payments

- **Provides:** direct bank payments on its network.
- **Plugs into:** a rail adapter (v1, after MVP).

## UPI / BHIM — India

- **Provides:** India's real-time payment rails.
- **Plugs into:** nothing yet. Deprioritized ("build this for US, 100x").
  v1 defines the integration *pattern* so the adapter interface doesn't
  assume US-only. No build until the US product is trusted.

## MCP — agent interface

- **Provides:** the protocol layer for agent-to-agent calls.
- **Plugs into:** the service endpoint. Wall-E as a skill/tool other agents
  (and Muse) can call — install, authenticate, authorize, transact.
- [DRAFT PLACEHOLDER — MCP server design needs the team.]

## What each tool is NOT

- None of these is Wall-E's ledger, custody, or money-transmitter license.
  Wall-E orchestrates; the rails move money (ADR 0002).
