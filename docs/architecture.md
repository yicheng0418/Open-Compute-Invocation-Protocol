# OCIP Architecture (Draft)

## Components

1. **Agent Runtime**
   - Parses a Workload Intent.
   - Maintains the task state machine and invocation loop.
   - Handles deadlines, cancellation, retries and user-visible status.

2. **Provider Registry**
   - Stores Provider/Capability Manifests, endpoint metadata, health, benchmark profile and service offers.
   - Is refreshed asynchronously.
   - Supplies a local or regional cache to the fast path.

3. **Authority Gate**
   - Validates the Authority Manifest and delegated capability for the requested action.
   - Checks budget, workload class, provider allow/deny rules, data region, duration, sharing and delegation constraints.
   - Uses locally verifiable credentials where policy permits.

4. **Fast Scheduler**
   - Applies hard feasibility filters.
   - Ranks feasible candidates using task-specific policy and end-to-end estimates.
   - Reserves a provider resource under a bounded lease.

5. **Execution Runtime**
   - Invokes provider adapters.
   - Supports progress events, cancellation, timeout, idempotency and receipt generation.

6. **Asynchronous Control Plane**
   - Handles discovery, registration, health, benchmark refresh, price/offer updates, revocation distribution, reputation and audit.
   - Must not be synchronously traversed for every invocation.

## Invocation flow

1. Parse workload intent, deadline and constraints.
2. Check suitable local capacity.
3. Select a candidate tier appropriate to the task: local; pre-authenticated nearby resources; established remote providers; or wider market discovery. The scheduler need not mechanically traverse every tier.
4. Validate authority and policy.
5. Read cached candidates and filter hard constraints.
6. Rank feasible candidates and request a bounded reservation lease.
7. Submit invocation and stream/collect execution events.
8. On timeout or provider failure, cancel or retry only under explicit idempotency and retry policy; fall back to another feasible candidate or return a clear failure.
9. Verify the receipt, then perform metering, audit and settlement asynchronously where possible.

## Two-stage reference scheduler

### Stage 1: hard filtering

Reject candidates that fail authority, workload compatibility, hardware/memory/runtime requirements, data-region policy, budget, provider health, deadline feasibility or required security controls.

### Stage 2: policy-based ranking

Estimate end-to-end completion time as the sum of queue, startup, transfer, compute and return time.

Rank candidates using a workload-specific policy that may consider P50/P95/P99 latency, reliability, price, data locality, privacy, energy or cooperation preference. There is no universal fixed weighting or single objective for all workloads.

The scheduler should optimize the actual task outcome, not advertised peak FLOPS alone.

## Latency and observability

Measure at least: resource discovery time, authority-check time, queue time, startup time, transfer time, compute time, return time, end-to-end P50/P95/P99, scheduling overhead, success rate, timeout rate and fallback rate. Do not publish hard latency guarantees until representative experiments support them.

## Failure semantics

The protocol must distinguish invalid request, unauthorized request, no feasible provider, reservation expiry, provider unavailable, deadline exceeded, execution failure, cancellation, verification failure and settlement pending. Retries must be bounded and must not duplicate non-idempotent work.

## Trust boundaries

Provider manifests and benchmark claims are assertions unless independently attested. Signed receipts prove origin and integrity of statements, not correctness of arbitrary results. Use task-appropriate checks such as deterministic test vectors, benchmark runs, sampling, redundant execution, trusted execution attestations or application-level validation.
