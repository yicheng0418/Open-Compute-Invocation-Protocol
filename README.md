# Open Compute Invocation Protocol (OCIP)

**An open, agent-native protocol for discovering, invoking, verifying, and settling compute services.**

OCIP aims to let authorized AI agents discover and use computing resources across independent providers through interoperable interfaces—without requiring a single cloud platform or hardware vendor.

> **The network must serve the intelligence, not interrupt it.**

## Status

OCIP is an early design project. This repository contains a working **v0.1 design draft**, not a ratified standard or production implementation. Protocol fields, scheduling policies, trust mechanisms, and conformance requirements remain subject to experiments and review.

## Core principles

1. **Latency First** — resource discovery and orchestration must not unnecessarily block task execution.
2. **Local First** — use suitable local resources before remote resources.
3. **Open Access** — independent providers and consumers can interoperate.
4. **Intent Based** — consumers describe workload requirements, not vendor-specific infrastructure.
5. **Human Authorized** — agent autonomy is bounded by explicit, verifiable authority.
6. **Verifiable Execution** — execution events and receipts are signed and auditable; verification strength depends on workload type.
7. **Decentralized Participation** — no single broker or ledger is mandatory.

## Architecture at a glance

- **Agent Runtime:** parses workload intent and manages invocation state.
- **Provider Registry:** maintains provider manifests, capabilities, health and performance metadata.
- **Authority Gate:** checks delegated permissions, budget, region, workload and expiry constraints.
- **Fast Scheduler:** filters incompatible providers, then ranks feasible candidates using end-to-end estimates.
- **Execution Runtime:** submits, monitors, cancels and receives workloads through provider adapters.
- **Async Control Plane:** refreshes discovery, health, benchmarks, offers, reservations, revocations and audit records outside the critical path.

See [architecture](docs/architecture.md), [authority and delegation](docs/authority-and-delegation.md), [compute units and exchange](docs/compute-units-and-exchange.md), and the [v0.1 draft](spec/v0.1/README.md).

## What OCIP is—and is not

OCIP is an interoperability protocol for compute-service discovery and invocation. It is not a cloud provider, GPU exchange, cryptocurrency, token, blockchain, or replacement for Kubernetes, Ray, Slurm, model-serving APIs, or payment networks.

Compute is a productive capability; a task-normalized compute unit is a measurement reference, not money or universal purchasing power. Compute services may be priced in fiat currency, exchanged for other compute services under explicit terms, or shared under an authorized cooperation agreement.

## Initial MVP

The first prototype should connect one consumer agent to at least two independent providers for simple asynchronous inference or batch workloads. It should test local-first selection, cached discovery, authority checks, two-stage scheduling, reservation, invocation, cancellation, execution receipts, timeout handling and fallback.

Initial non-goals: distributed multi-region training, public-chain consensus, tokens, unrestricted recursive delegation, autonomous cross-border payments, or a universal fixed GPU exchange rate.

## Contributing

Design discussion and implementation proposals are welcome. Please distinguish normative protocol requirements from reference algorithms and implementation choices. Do not claim compatibility or conformance until tests exist.

## License

No license has been selected yet. Unless and until a license is added, standard copyright applies; public visibility does not itself grant permission to reuse the code.
