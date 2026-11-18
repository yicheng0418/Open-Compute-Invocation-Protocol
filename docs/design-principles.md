# OCIP Design Principles

## Normative direction

### 1. Latency First

The protocol must avoid placing broad resource discovery, complex negotiation, remote authorization round-trips, ledger consensus, or settlement on every invocation's critical path. No fixed latency SLA is asserted before measurement.

### 2. Local First

A consumer should consider suitable local compute before remote resources. Local-first is a preference subject to workload requirements, data policy, deadline, reliability and total cost—not a rule to use local hardware when it cannot meet the task.

### 3. Open and hardware-agnostic

Providers expose capabilities through interoperable manifests. OCIP describes workload requirements and service outcomes without requiring one accelerator vendor, cloud platform, scheduler or model API.

### 4. Intent based

A consumer describes the workload, constraints and desired service level. The provider decides how to map the request onto its implementation, subject to the declared capability and contract.

### 5. Human authorized autonomy

An agent may act only within authority delegated by a user or organization. Technical capability does not create authority. Budget, workload, data location, duration, sharing and sub-delegation constraints must be machine-checkable.

### 6. Verifiable execution

Signed manifests, events and receipts establish who made which statements and what was recorded. They do not automatically prove that arbitrary computation was correct. Verification must be workload-specific.

### 7. Decentralized participation

Providers and brokers may be independently operated. A central registry or broker may be useful, but it must not be a protocol-level single point of control.

## Control plane / execution plane separation

The control plane performs asynchronous discovery, registration, health checks, benchmark updates, offers, reservation preparation, revocation propagation and audit. The execution plane uses cached candidates and locally verifiable credentials to authorize and invoke work quickly.

The execution plane must have explicit freshness and revocation policies. A cache is not a reason to ignore expired credentials or known revocations.

## Market and cooperation

OCIP supports competitive offers, direct purchase, compute-for-compute exchange, and authorized resource-sharing agreements. The protocol does not prescribe one allocation ideology or require every interaction to be a spot market transaction.
