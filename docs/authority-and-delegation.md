# Authority and Delegation (Draft)

## Principle

Agent autonomy derives from explicit user or organizational authorization. An agent cannot expand its own authority merely because it can technically perform an action.

## Authority Manifest

The manifest should express a composable permission vector rather than relying only on a single autonomy level. Candidate fields include:

- issuer, subject agent, audience and credential identifier;
- permitted actions: discover, reserve, invoke, purchase, share, exchange, negotiate, delegate;
- resource scope and provider allow/deny rules;
- workload types and prohibited workloads;
- spending limits, currency and accounting period;
- validity interval and maximum lease duration;
- data classification, residency and processing constraints;
- sharing and sub-delegation permissions;
- revocation reference and audit requirements.

The final schema, issuer trust model and credential format remain open.

## Multi-level delegation

Delegation may be supported when explicitly authorized. A child delegation must be no broader than its parent in resource scope, actions, budget, duration, geography, workload and re-delegation rights. The chain must be verifiable and auditable.

The real-time invocation path should not synchronously ask every upstream delegator for approval. Use signed, bounded-lifetime credentials and locally verifiable delegation evidence. Revocation propagation, cache freshness and emergency stop behavior require explicit policy.

## Human checkpoints

Require renewed approval when an action exceeds the delegated budget, changes data jurisdiction, introduces a new sharing or re-delegation right, violates provider policy, or materially changes risk.

## Security considerations

Protect against credential theft, replay, confused-deputy attacks, scope escalation, stale revocation state, malicious providers, unauthorized resale and budget exhaustion. Bind invocation authorization to task identity, provider, amount/scope and expiry where practical.
