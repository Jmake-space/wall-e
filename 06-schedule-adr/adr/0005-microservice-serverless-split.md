# ADR 0005 — Microservice / serverless split

## Context

Wall-E has two kinds of work. Some of it is steady and stateful: routing
requests, orchestrating a payment across several steps, verifying identity,
writing audit records. Some of it is bursty and event-driven: pulling bank
data on a schedule, executing a rail payment, running fraud checks on a
single request, sending a notification. The question is which deploy shape
each component gets.

## Decision

- **Microservices (containers):** API Gateway, Agent Core, Auth + Identity,
  Audit Writer. Long-running, hold connections and in-memory state, deploy
  independently with rolling updates and health checks.
- **Serverless workers (functions):** Plaid Connector, Rail Adapters,
  Guardrails, Notifier. Stateless, triggered by events or schedules, scale
  to zero when idle.
- **Data:** managed stores, not self-hosted at MVP — Audit Store
  (tamper-evident), Transaction Store (12 months), Token Vault (Plaid tokens
  only, never logins).

[DRAFT PLACEHOLDER — no hosting platform chosen. AWS / GCP / Fly / other is
still an open team decision, and it affects cold-start behavior, VPC design,
and cost.]

## Consequences

- **Good:** workers cost nothing idle; each component deploys and scales on
  its own; a rail-adapter failure can't take down the core; matches the
  "not a payment gateway" posture — the heavy lifting stays with Plaid and
  the rails.
- **Bad:** cold starts on the latency-sensitive path (approval → execution →
  notify). Mitigation is an open design task — provisioned concurrency or
  keeping the hot path warm; still to be decided.
- **Neutral:** two deploy pipelines to maintain (containers + functions);
  distributed tracing becomes mandatory, not optional — every request needs
  the request ID the gateway assigns, end to end into the audit log.
