# OCIP v0.1 Protocol Semantics (Draft)

**Status:** design draft. This document defines an initial interaction contract; it is not a ratified standard.

## 1. Roles

- **Consumer:** requests compute on behalf of an application or agent.
- **Provider:** advertises and executes compute services.
- **Registry/Broker (optional):** distributes provider metadata and offers. It is not trusted to authorize work or prove execution merely because it lists a provider.
- **Authority Issuer:** user or organization that issues bounded permissions to a consumer agent.

## 2. Core objects

The JSON Schemas in `schemas/` define the initial wire-level shapes for:

1. Workload Intent
2. Provider Manifest
3. Authority Manifest
4. Resource Reservation / Lease
5. Invocation
6. Execution Receipt

Execution Events are optional progress messages and are described below. Fields marked as draft may change before a stable release.

## 3. Lifecycle

`DISCOVERED → FILTERED → RESERVED → SUBMITTED → RUNNING → SUCCEEDED | FAILED | CANCELLED | EXPIRED`

A request may terminate earlier with `REJECTED`, `NO_CAPACITY` or `DEADLINE_EXCEEDED`. Providers must not report success before the workload has completed according to the declared completion condition.

### Suggested exchange

1. Consumer creates a Workload Intent with a globally unique request ID and absolute deadline.
2. Consumer checks local resources first. If remote resources are needed, it reads a fresh-enough local cache of Provider Manifests.
3. Consumer validates its Authority Manifest locally. A provider independently validates the authority evidence relevant to its own service.
4. Consumer filters candidates against hard constraints and ranks feasible candidates using a workload-specific policy.
5. Consumer requests a bounded reservation lease. A reservation is not yet an invocation.
6. Consumer submits an Invocation referencing the intent, reservation and authorization.
7. Provider emits optional Execution Events and eventually a signed Execution Receipt.
8. Consumer verifies the receipt and performs metering, audit and settlement according to the separate service agreement.

## 4. IDs, idempotency and deadlines

- IDs are opaque strings. Producers should use collision-resistant identifiers (for example UUIDs).
- Every Invocation has an `idempotency_key` scoped to the Provider identity.
- Repeating the same key with the same request digest must return the original invocation state/result, not execute the work again.
- Reusing a key with a different digest must return `IDEMPOTENCY_CONFLICT`.
- Deadlines are absolute RFC 3339 timestamps in UTC. A Provider must reject work that cannot reasonably start or complete before the deadline under its advertised policy.
- Reservation leases have an explicit expiry. An expired lease cannot be used to submit a new Invocation.

## 5. Cancellation, timeout and retries

- Cancellation is best-effort and must be acknowledged with the current task state.
- A Provider may report that cancellation is too late if the task has already completed.
- Consumers must not retry non-idempotent work unless the workload explicitly declares safe retry semantics or uses a new application-level compensation strategy.
- Retries are bounded by the original deadline and policy. A timeout must not silently create unbounded duplicate work.
- Provider loss before acceptance permits trying another candidate. Provider loss after acceptance requires checking invocation state or idempotency before resubmission.

## 6. Errors

Initial error codes:

- `INVALID_REQUEST`
- `UNSUPPORTED_VERSION`
- `UNSUPPORTED_WORKLOAD`
- `UNAUTHORIZED`
- `POLICY_DENIED`
- `NO_FEASIBLE_PROVIDER`
- `NO_CAPACITY`
- `RESERVATION_EXPIRED`
- `PROVIDER_UNAVAILABLE`
- `DEADLINE_EXCEEDED`
- `IDEMPOTENCY_CONFLICT`
- `CANCELLED`
- `EXECUTION_FAILED`
- `RECEIPT_INVALID`
- `RATE_LIMITED`
- `INTERNAL_ERROR`

Errors should include a stable code, human-readable message, retryability hint and correlation/request ID. Implementations must not expose secrets or sensitive provider internals in error details.

## 7. Versioning and extensibility

- A message carries `protocol_version` (initially `0.1`).
- Unknown optional extension fields should be ignored; unknown required capabilities must cause a clear rejection.
- Breaking changes require a new incompatible protocol version. Additive fields should be introduced compatibly and documented.
- Transport and encoding are not fixed by the semantic model. The initial schemas use JSON; later encodings must preserve the same semantics.
- Provider capability negotiation must happen before invocation, not through trial-and-error execution on the critical path.

## 8. Security and trust

- Authenticate transport endpoints and bind signed manifests/receipts to issuer identity.
- Bind authorization to the consumer, action, workload scope, provider/resource scope, budget and expiry.
- Prevent replay through request IDs, idempotency keys, expiry and signature verification.
- A signed receipt proves who issued the statement and that it was not modified; it does not prove arbitrary computation was correct.
- Result verification is workload-specific and may use deterministic test vectors, application validation, sampling, redundant execution or hardware attestation where appropriate.

## 9. Not yet standardized

The following remain open: canonical transport (HTTP/gRPC/other), credential format and trust roots, exact reservation atomicity, event streaming protocol, schema for workload-specific inputs, metering precision, settlement interface, revocation freshness guarantees and conformance test suite.
