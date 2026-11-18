# OCIP v0.1 JSON Schemas

These schemas are an initial machine-readable draft using JSON Schema Draft 2020-12.

| Schema | Purpose |
|---|---|
| [Workload Intent](workload-intent.schema.json) | Consumer task request |
| [Provider Manifest](provider-manifest.schema.json) | Provider identity and capabilities |
| [Authority Manifest](authority-manifest.schema.json) | Bounded human/organizational delegation |
| [Resource Reservation](resource-reservation.schema.json) | Time-limited capacity lease |
| [Invocation](invocation.schema.json) | Idempotent task submission |
| [Execution Receipt](execution-receipt.schema.json) | Provider-signed execution record |
| [Execution Event](execution-event.schema.json) | Optional progress/state event |

## Important limitations

- These schemas define shape, not complete business or security semantics.
- Signature envelope formats, credential trust roots, canonicalization and key rotation are not yet standardized.
- JSON Schema `format` validation may require explicit format assertion by validators.
- Workload-specific payloads should normally be referenced by digest and secure URI, not embedded in manifests.
- Do not treat a signed receipt as proof that arbitrary computation is correct.
- Breaking changes are possible before v0.1 stabilizes.

See [protocol semantics](../protocol.md) for lifecycle, idempotency, deadlines, cancellation, errors and versioning.
