# ADR-001: Core Language and ABI Strategy

- **Status:** Accepted as a provisional implementation direction for v0.1
- **Date:** 2026-11-18
- **Scope:** Reference implementation and SDK boundary; this ADR does not make the wire protocol language-specific.

## Context

OCIP is intended to connect AI agents and independent compute providers across operating systems, hardware vendors, runtimes and programming languages. It must keep the invocation path responsive while handling network I/O, scheduling, authorization, provider failures and untrusted remote inputs.

C is attractive for low-level integration, small runtime footprints and a widely supported ABI. However, implementing the entire network-facing core in C would increase memory-safety and concurrency risks in security-sensitive code. Rust offers native performance, explicit resource management and memory-safety guarantees, while C ABI interoperability can preserve broad embedding options.

The protocol itself must remain independent of any implementation language.

## Decision

Adopt the following provisional strategy:

1. **Protocol is language-neutral.** Normative messages, schemas, state transitions, error semantics and conformance tests must not require Rust, C or any other implementation language.
2. **Rust is the preferred reference-core language for v0.1.** The Agent Runtime, Authority Gate, Provider Registry client, Fast Scheduler and Execution Runtime should initially be implemented in Rust, subject to benchmark and ecosystem validation.
3. **Expose a narrow, versioned C ABI where embedding requires it.** The C ABI is an integration boundary, not the protocol definition and not a requirement that all internal modules be written in C.
4. **Provide language-native SDKs.** Python and TypeScript are priority integration targets for AI agents. They may use a Rust core through bindings or communicate with an OCIP runtime over the protocol.
5. **Keep hardware/provider adapters replaceable.** C and C++ are appropriate where vendor SDKs, drivers or existing runtimes require them. Adapters may also be written in other languages if they satisfy the provider contract.
6. **Start with JSON-based schemas and messages for inspectability and ease of prototyping.** Consider Protobuf or another compact encoding only after interoperability and performance measurements show a need. Encoding choices must be negotiated/versioned and must not change protocol semantics.

## Consequences

### Positive

- The protocol remains implementable in many languages.
- Rust provides a memory-safe default for the security-sensitive reference runtime.
- C ABI enables integration with C/C++, Python extensions and other FFI-capable environments.
- Provider adapters can use the language best supported by their hardware and serving stack.
- Performance optimization can focus on measured end-to-end bottlenecks rather than assuming that C is automatically faster.

### Costs and risks

- FFI introduces ownership, lifetime, error-propagation and thread-safety complexity.
- Multiple SDKs and adapters increase conformance-testing requirements.
- Rust may not be the easiest choice for every provider ecosystem or embedded target.
- JSON may be inefficient for some high-volume data paths; binary transport may eventually be needed.
- The choice of async runtime, serialization library and GPU adapter stack remains open until prototype requirements are clearer.

## C ABI design constraints

If a C ABI is exposed, it should:

- use opaque handles for internal Rust-owned state;
- use fixed-width integer types and explicitly versioned structures;
- define ownership and lifetime rules for every pointer and buffer;
- provide explicit allocation/free or caller-owned buffer conventions;
- return stable error codes and never unwind a Rust panic across the ABI boundary;
- document thread-safety, cancellation and callback behavior;
- avoid exposing internal Rust types or committing the wire protocol to a C memory layout.

## Performance policy

Language selection is not a substitute for measurement. The project must measure end-to-end latency and its components: discovery, authorization, queueing, startup, transfer, compute and result return. Optimize only demonstrated bottlenecks. A C implementation may be introduced for a measured hot path or hardware boundary without rewriting the whole core.

## Alternatives considered

### Entire core in C

Rejected as the default because the core handles untrusted network inputs, authorization, concurrency and resource lifetimes. C remains available for narrow low-level components and adapters.

### Entire core in Python or TypeScript

Not selected for the reference runtime because the core is expected to be embedded in diverse environments and may require predictable resource control. These languages remain first-class agent integration targets.

### Entire core in C++

Not selected as the default reference core because OCIP benefits from a narrow, stable C ABI and a memory-safe core. C++ remains suitable for provider adapters and existing GPU/runtime integrations.

### Rust only, with no C ABI

Not selected because a narrow C ABI materially improves embedding and integration options without making the protocol language-specific.

## Open questions

- Which Rust async runtime and HTTP/transport stack best fit the first prototype?
- Should the C ABI be a library interface only, or should a stable local IPC interface be prioritized first?
- Which Python binding approach best balances packaging, safety and cross-platform support?
- Which message encoding and streaming transport are needed after baseline measurements?
- What minimum platform matrix should v0.1 conformance tests cover?

## Revisit conditions

Revisit this ADR if prototype benchmarks show the Rust core is unsuitable for target platforms, if FFI complexity outweighs its benefits, or if provider/agent ecosystem requirements point to a better implementation strategy. Any change must preserve language-neutral protocol semantics.
