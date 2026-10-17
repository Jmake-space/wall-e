# Wall-E — Data Protection

Wall-E reads people's bank transactions. That data is the product's fuel
and its biggest liability. Rules:

## What we hold

- Transaction history: 30 days read live, 12 months stored (from the
  brainstorm — "keep records for 12 months").
- Plaid tokens (encrypted, never logged).
- Audit entries: who asked, what was approved, what moved.
- **Never held:** bank logins, passwords, full account numbers in logs.

## Handling rules

- Least privilege: components see only the data they need. The notifier
  doesn't need transaction history; the audit log doesn't need tokens.
- Encryption in transit and at rest, always.
- [DRAFT PLACEHOLDER — specific mechanisms (KMS, field-level encryption,
  tokenization of PII) need the team.]
- Logs and error messages never contain tokens, credentials, or full
  account numbers. This is a code-review checklist item, not a hope.

## Retention

- Transaction records: 12 months, then [DRAFT PLACEHOLDER — delete or
  archive policy needs the team and a legal read].
- Audit entries: kept longer than transaction data — they're the proof.
  [DRAFT PLACEHOLDER — exact period needs the team and a legal read.]
- On account disconnect: tokens revoked immediately; data handling per the
  retention policy.

## SOC2 alignment

SOC2 was named in the brainstorm as a pillar. Alignment means:

- Access controls with least privilege, reviewed.
- Change management on every deploy (see `05-policies-governance/`).
- Audit trail of who did what (we have this by design).
- Incident response playbook (see `07-operational-model/`).

[DRAFT PLACEHOLDER — "SOC2-aligned" vs "SOC2-certified" is a real
distinction the team needs to decide, with a legal/compliance read. Don't
claim certification we don't have.]

## Breach posture

[DRAFT PLACEHOLDER — breach notification plan, timelines, and owner need
the team. With financial data, this can't be improvised later.]
