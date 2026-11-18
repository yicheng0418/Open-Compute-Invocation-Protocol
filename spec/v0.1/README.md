# OCIP v0.1 — Protocol Draft

**Status:** exploratory draft; not a ratified standard and not yet an implementation contract.

## Scope

v0.1 defines the conceptual interaction surface for one consumer agent to discover and invoke one of multiple independent providers for simple asynchronous inference or batch workloads.

## Core protocol objects

1. **Workload Intent** — task type, inputs/references, runtime/model constraints, quality target, deadline, data policy, budget and verification requirements.
2. **Provider Manifest** — provider identity, endpoint, supported workload/runtime capabilities, resource profile, service offers, region, health and evidence references.
3. **Authority Manifest** — signed, bounded permissions for the consumer agent and requested operation.
4. **Resource Reservation / Lease** — provider's temporary commitment to a defined capacity and offer until expiry.
5. **Invocation** — idempotent task submission bound to intent, reservation and authorization.
6. **Execution Event** — optional progress, state, metrics and diagnostic events.
7. **Execution Receipt** — signed summary of provider, invocation, workload digest, execution status, metering evidence, timestamps and verification references.

## Required lifecycle semantics to specify

- Protocol version negotiation and capability discovery.
- Unique request/invocation IDs and idempotency keys.
- Deadlines, lease expiry and cancellation.
- Typed errors and bounded retry rules.
- Provider disappearance and reservation failure.
- Duplicate submission and non-idempotent workload handling.
- Receipt signatures, evidence references and verification outcomes.
- Compatibility and extension rules.

## Reference algorithm

Use two-stage scheduling: hard feasibility filtering followed by workload-specific ranking. Estimate end-to-end time as queue + startup + transfer + compute + return. Ranking policy is replaceable; no universal score weights are mandated.

## MVP

- One Consumer Agent.
- At least two independent Providers.
- Simple asynchronous inference or batch tasks.
- Local-first selection and cached discovery.
- Local verification of bounded authority.
- Reservation, invocation, progress, cancellation and signed receipt.
- Timeout, provider failure and bounded fallback.
- Metrics for P50/P95/P99 and each latency component.

## Explicit non-goals for v0.1

- Public blockchain, consensus on every invocation, or tokens.
- Universal compute currency or fixed GPU exchange rate.
- Multi-region distributed training.
- Unrestricted recursive delegation.
- Autonomous cross-border financial settlement.
- Mandatory centralized broker or registry.

## Open design questions

- Canonical schema and transport binding.
- Provider identity and trust roots.
- Credential format, revocation freshness and emergency stop.
- Reservation atomicity and lease semantics.
- Receipt evidence profiles by workload type.
- Streaming and cancellation semantics.
- Conformance tests and interoperability profiles.


## Machine-readable schemas and interaction contract

- [Protocol semantics](protocol.md)
- [JSON Schema index](schemas/README.md)
- [Workload Intent](schemas/workload-intent.schema.json)
- [Provider Manifest](schemas/provider-manifest.schema.json)
- [Authority Manifest](schemas/authority-manifest.schema.json)
- [Resource Reservation / Lease](schemas/resource-reservation.schema.json)
- [Invocation](schemas/invocation.schema.json)
- [Execution Receipt](schemas/execution-receipt.schema.json)
- [Optional Execution Event](schemas/execution-event.schema.json)

These are draft schemas and require interoperability tests before being treated as stable contracts.
