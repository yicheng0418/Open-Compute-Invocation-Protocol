# CGA-01: Dynamic Collaborative Cognitive Growth Architecture

**Status:** Experimental architecture proposal  
**Version:** 0.1-draft  
**Relationship to OCIP:** Companion reference architecture; not a normative OCIP protocol extension.

## 1. Purpose

CGA explores how a capable cognitive system can be composed from multiple relatively small, replaceable models, deterministic software components, external tools, and a persistent shared cognitive workspace.

The objective is not to make several models imitate one large model. It is to organize limited capabilities into a system that can:

- select and coordinate models dynamically for each task;
- move beyond merely answering or disputing a user's framing and investigate reality-grounded unknowns;
- turn useful discoveries into explicit concepts, hypotheses, relations, and methods;
- preserve evidence, uncertainty, failures, and the history of revisions;
- reuse and test prior abstractions in new domains;
- change its collaboration topology when task demands or measured capability gaps change.

CGA is a research architecture, not a claim that a small model can reproduce all capabilities of a much larger model. External memory and orchestration can extend effective task capability, but they do not automatically recreate latent knowledge, language competence, or reasoning capacity absent from the component models.

## 2. Design principles

1. **Dynamic roles, not permanent agents.** A model is a capability-bearing node. Roles are temporary assignments derived from task requirements and observed performance.
2. **Task-relative capability.** Model selection is based on evidence for the relevant task class, not parameter count or a universal model ranking.
3. **Reality-grounded exploration.** New questions and concepts should arise from concrete tasks, observations, data, experiments, and identified explanatory gaps.
4. **Shared but governed cognition.** Models share a workspace, but no model may silently overwrite evidence, erase dissent, or promote its own hypothesis to fact.
5. **Abstraction with provenance.** Concepts and methods retain their origin, supporting evidence, counterevidence, assumptions, and scope of applicability.
6. **Independent verification.** Agreement among models is not proof. Important claims require suitable external checks.
7. **Bounded autonomy.** Delegation, tool access, compute, budget, data access, and exploration depth are constrained by explicit policy.
8. **Reversible evolution.** Changes to routing policies, memory structures, model composition, and learned methods are versioned and can be rolled back.
9. **Local-first, expandable execution.** Prefer suitable local models and tools; invoke remote models or compute only when authorized and justified by task value.

## 3. Initial cognitive interaction: Yin and Yang as a starting point

CGA uses a deliberately minimal initial distinction between two interaction directions:

- **Responsive direction (Yin):** receive a user's question or proposed approach, understand its intent and constraints, and work within that framing to help solve the problem.
- **Critical direction (Yang):** examine the framing, identify assumptions and omissions, offer counterarguments, and return useful questions or alternative paths to the user.

These are initial cognitive behaviors, not permanent agent roles, metaphysical claims, or an exhaustive taxonomy of intelligence. They should not force every problem into a binary choice.

The intended development is a further mode of **reality-grounded exploration**. While solving a task and interacting with the user, the system identifies unknown variables, unexplained observations, missing mechanisms, and testable questions. It may then form abstractions that are useful, irrelevant, or eventually disproven. Their value is determined through subsequent use and validation, not by the fact that they were generated.

CGA therefore does not define the third mode as a compromise between Yin and Yang. It is an expansion from user-framed interaction into independent, evidence-seeking exploration.

## 4. System architecture

CGA is composed of the following logical components. A component may be implemented by a model, deterministic code, a tool, or a combination.

### 4.1 Cognitive Orchestrator

Maintains task state and decides:

- what the current task is trying to achieve;
- which capabilities are required;
- which model or tool should be invoked;
- whether work should be parallel, sequential, adversarial, or exploratory;
- when more evidence is needed;
- when to stop, ask the user, or request authorization;
- whether a discovered capability gap warrants adding or replacing a component.

The orchestrator is a control component, not an oracle. Its decisions and outcomes must be logged and evaluated.

### 4.2 Model and Capability Registry

Maintains machine-readable manifests for available models and tools.

A capability record should include, where available:

- model or tool identifier and version;
- supported modalities and task classes;
- context and output limits;
- hardware and runtime requirements;
- measured task-specific performance and evaluation provenance;
- latency, resource consumption, and cost;
- data handling and deployment constraints;
- known failure modes and uncertainty;
- availability and health.

Capabilities are empirical and task-relative. A model's self-description is an assertion, not sufficient evidence.

### 4.3 Dynamic Collaboration Runtime

Assigns temporary roles such as:

- task interpreter;
- alternative analyst;
- hypothesis generator;
- domain specialist;
- evidence researcher;
- code or simulation executor;
- verifier;
- abstraction proposer;
- memory curator.

Roles may be combined, reassigned, duplicated for independent analysis, or left unfilled. The runtime may ask a model to challenge another model's assumptions, but must avoid treating stylistic disagreement as substantive evidence.

### 4.4 Shared Cognitive Workspace

A structured, versioned workspace through which participating components exchange task-relevant state.

Core object types:

| Object | Meaning |
| --- | --- |
| Task | Goal, constraints, owner, deadline, budget, status |
| Question | Known or newly discovered unresolved question |
| Fact | Claim supported by a source or observation |
| Hypothesis | Provisional explanatory or predictive claim |
| Relation | Proposed link between entities, concepts, or events |
| Concept | An abstraction with definition and scope |
| Evidence | Source, observation, experiment, counterexample, or result |
| Method | Reusable procedure, model, or analytical strategy |
| Decision | Chosen action, rationale, authority, and consequences |
| Dispute | Conflicting claims and the evidence each relies on |

Every object should carry provenance, timestamps, authoring component, confidence or uncertainty where meaningful, status, and links to supporting or contradicting objects.

### 4.5 Cognitive World Memory

Memory is more than a transcript or vector store. It is a queryable, versioned representation of what the system has encountered and how its understanding has changed.

Separate at least:

1. **Evidence memory:** source records, raw observations, datasets, experiment outputs, and immutable provenance.
2. **Exploration memory:** questions, hypotheses, alternatives, and abandoned paths.
3. **Conceptual memory:** concepts, relations, models, methods, assumptions, and applicability boundaries.
4. **Episodic memory:** tasks, decisions, outcomes, failures, and lessons learned.
5. **Policy memory:** approved routing rules, permissions, retention rules, and safety constraints.

Vector retrieval may help locate semantically related material, but it should not replace structured relations, provenance, versioning, or exact source records.

### 4.6 Verification and Evaluation Layer

Chooses validation methods appropriate to the claim:

- deterministic tests and formal checks where possible;
- source verification and data provenance;
- independent calculations or implementations;
- reproducible experiments and simulations;
- out-of-sample prediction;
- expert or human review where required.

Model consensus, repeated self-critique, and fluent explanations are not substitutes for independent verification.

### 4.7 External Reality and Tool Interface

Provides authorized access to search, databases, code execution, simulations, sensors, specialist models, and external compute. Tool outputs are recorded as evidence with source, time, parameters, and limitations.

## 5. Dynamic orchestration lifecycle

A typical task proceeds through a revisable loop:

1. **Receive:** parse the user's goal, constraints, context, and authority.
2. **Frame:** identify the task, known facts, assumptions, unknowns, and success criteria.
3. **Assess capability:** estimate required skills, uncertainty, risk, latency, and resource budget.
4. **Select and assign:** choose suitable model/tool nodes and temporary roles.
5. **Collaborate:** run sequential or parallel work; allow nodes to propose counter-analysis and new subtasks.
6. **Reconcile:** distinguish agreement, disagreement, unsupported claims, and genuinely new questions.
7. **Explore:** investigate high-value unknowns using authorized evidence sources, experiments, or simulations.
8. **Verify:** test important conclusions and abstractions independently.
9. **Abstract:** convert validated or promising results into reusable concepts, relations, or methods with explicit status.
10. **Update memory:** append provenance-rich results and preserve superseded versions.
11. **Reassess topology:** decide whether the current nodes and workflow remain suitable or a new capability is needed.
12. **Stop or continue:** stop when marginal information value is low, the budget is exhausted, a decision is ready, or human authorization is required.

Not every task needs every step. Simple tasks should remain simple.

## 6. Task-relative model selection

Model selection must not use parameter count as a proxy for competence.

A scheduler may estimate candidate utility using task-specific evidence:

`Utility(m,t) = Quality(m,t) - Cost(m,t) - Risk(m,t) - LatencyPenalty(m,t)`

This is a conceptual expression, not a mandated scoring formula. Implementations should define measurable terms, normalize them carefully, and avoid false precision.

Selection should consider:

- demonstrated performance on comparable tasks;
- independence from already selected models;
- expected information gain;
- runtime and context constraints;
- privacy, authority, and data locality;
- latency, energy, and monetary cost;
- model availability and failure history.

For high-impact claims, prefer independent evidence or genuinely diverse methods over repeated calls to the same model.

## 7. Exploration, abstraction, and cognitive growth

CGA treats exploration as a task that can emerge during problem solving, not as unrestricted background activity.

A candidate discovery should record:

- the concrete observation or problem that motivated it;
- the gap in the current explanation;
- the proposed new question, variable, relation, or concept;
- competing explanations;
- what evidence could support or falsify it;
- expected cost and potential value of further investigation.

Concepts may be retained even when immediate utility is unknown, but they must be labelled accordingly. A generated abstraction is not a fact. Cross-domain transfer is a hypothesis until tested under the receiving domain's conditions.

The system should distinguish:
- **generated:** proposed by a model;
- **plausible:** coherent but not sufficiently tested;
- **supported:** backed by relevant evidence;
- **validated within scope:** passed specified tests within declared boundaries;
- **rejected or superseded:** contradicted or replaced, with history retained.

Cognitive growth is measured by improved performance, explanatory power, calibration, transfer, and useful discovery—not by the number of stored concepts or the apparent complexity of the memory graph.

## 8. Safety, authority, and governance

Dynamic collaboration must not imply unrestricted autonomy.

- Every tool call and delegated task is subject to explicit authority and least-privilege permissions.
- Budget, time, recursion depth, model calls, data access, and external actions have hard limits.
- External content is untrusted input and cannot override system policy.
- Sensitive or consequential actions require the appropriate human approval.
- Memory updates are provenance-tracked; destructive edits and silent overwrites are prohibited.
- Conflicts and minority hypotheses are retained where material.
- The system must support cancellation, audit, rollback, and incident review.
- Private data must not be moved to remote models or providers without authorization and applicable policy checks.

OCIP's Authority Gate and invocation controls may be used when CGA requests external compute or model services.

## 9. Relationship to OCIP

CGA and OCIP have distinct responsibilities:

- **CGA** organizes cognition: task decomposition, model collaboration, exploration, abstraction, memory, and evaluation.
- **OCIP** organizes compute-service interoperability: capability discovery, authority, scheduling, invocation, execution events, verification receipts, and settlement.

CGA may use local models directly and invoke remote models or compute through OCIP adapters. OCIP does not define how a cognitive system reasons, and CGA does not replace OCIP's authority, provider, invocation, or settlement mechanisms.

This document is a companion architecture proposal. It does not modify OCIP's normative protocol requirements or claim OCIP conformance.

## 10. Evaluation plan

Compare at least four configurations under controlled task sets and matched compute budgets:

1. one standalone small model;
2. multiple small models with fixed roles;
3. multiple small models with dynamic collaboration;
4. dynamic collaboration plus persistent cognitive-world memory and verification.

Evaluate:

- task success and factual accuracy;
- calibration and uncertainty quality;
- cost, latency, energy, and total model calls;
- useful discovery rate for previously unasked questions;
- quality and falsifiability of generated hypotheses;
- correction rate for detected errors;
- transfer success on held-out domains;
- memory retrieval precision and provenance completeness;
- robustness to model disagreement, unavailable nodes, and misleading inputs.

Use blinded or independently scored tasks where possible. Separate gains caused by extra inference budget, retrieval, tools, and collaboration. A system should not be credited with cognitive growth merely because it has more context or more opportunities to sample answers.

## 11. Minimal prototype roadmap

### CGA-01A — Local collaboration baseline
- Two or three local model endpoints.
- Simple capability registry.
- Task state and bounded orchestrator.
- Shared structured workspace.
- Explicit user-visible trace of assignments and outputs.

### CGA-01B — Evidence and memory
- Structured fact, hypothesis, question, concept, and evidence records.
- Provenance and version history.
- Retrieval across prior tasks.
- Separation of evidence from generated hypotheses.

### CGA-01C — Dynamic collaboration
- Task-relative model selection.
- Temporary role assignment and reassignment.
- Independent critique and verification paths.
- Cost, latency, and stop-budget controls.

### CGA-01D — Reality-grounded exploration
- Discovery of missing variables and unresolved questions.
- Authorized search, code, and simulation tools.
- Concept formation and cross-domain transfer tests.
- Controlled evaluation against fixed-role baselines.

### CGA-01E — OCIP integration
- Discover external model and compute capabilities through OCIP.
- Apply OCIP authority and workload constraints.
- Invoke remote resources with bounded leases and cancellation.
- Record execution receipts and link them to cognitive task provenance.

## 12. Open research questions

1. What is the smallest useful initial cognitive kernel, and how should its initial responsive and critical directions be represented without making them permanent constraints?
2. How can a system distinguish a genuinely new explanatory variable from a relabeling of known information?
3. How should it estimate the value of exploring a question with no immediate user-facing utility?
4. What evidence is sufficient to promote a concept from plausible to validated within a declared scope?
5. How can dynamic role assignment avoid feedback loops, correlated errors, and self-reinforcing model consensus?
6. Which parts of cognitive growth belong in model weights, external memory, executable tools, or orchestration policy?
7. Under what controlled conditions can a multi-model small system outperform a single larger model at comparable total compute cost?

## 13. Current limitations

CGA is a testable design hypothesis. It does not establish that arbitrary small models can reproduce frontier-model capabilities, that recursive exploration necessarily produces intelligence, or that a larger memory graph implies better reasoning. Progress must be demonstrated on reproducible tasks with external evaluation and transparent resource accounting.

---

**Design maxim:** Build a system that can change how it organizes its capabilities as it learns about the task and the world—without confusing generated ideas with verified knowledge.
