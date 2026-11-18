# Compute Units, Service Pricing and Exchange (Draft)

## Separate the concepts

- **Hardware asset:** physical GPU/CPU/accelerator and associated equipment.
- **Compute service:** a provider's execution of a defined workload under service conditions.
- **Task-normalized compute unit:** a measurement reference derived from a defined benchmark/workload profile.
- **Exchange coefficient or offer:** a task- and context-specific comparison between providers or services.
- **Money:** the settlement instrument, such as an agreed fiat currency.

Compute is a productive capability, not money. A compute unit is not automatically currency, a security, a universal claim on goods, or general purchasing power.

## No universal compute exchange rate

Different hardware may differ in model compatibility, precision, memory, interconnect, software stack, queueing, data locality, latency, reliability and energy use. Therefore, an exchange coefficient must be conditional on a workload profile and service constraints.

A comparison should specify at least workload/model, input and output shape, precision, quality threshold, latency/deadline, memory, data location, reliability and measurement method. Benchmark results must include environment and version information.

## Supported commercial patterns

1. Compute service purchased for money.
2. Compute service exchanged for another compute service under an explicit contract.
3. Authorized sharing/cooperation with contribution and usage accounting.

The protocol does not define a token, stablecoin, universal compute currency or fixed GPU exchange rate. Pricing and legal settlement remain subject to applicable law and contract.

## Open questions

- How should benchmark suites represent diverse inference, training, simulation and data workloads?
- How should quality and output equivalence be measured?
- How should dynamic offers account for queueing, locality, reliability and energy?
- Which metering data can be independently audited without exposing trade secrets?
- How should disputes and partial completion be settled?
