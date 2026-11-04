# AOP Context Graph

`aop-context-graph` is the single authority for the substrate of observed work: the entity model of the Context Graph of Work, the case schema, the case stitching semantics, the Digital Twin of Operations, the drift detection obligations, and the observation posture that constrains capture.

| Field | Value |
|---|---|
| Authority | The substrate: entity model, case schema, stitching, twin, drift detection, observation posture |
| Tier | Substrate |
| Landing wave | 3 |
| Version | 0.2.1 |
| Status | Stable |
| Licence | MIT |

## What this repository owns

- The Context Graph of Work: the entity model (CASE, TASK, STEP, ACTOR, APPLICATION, DECISION, RULE, EXCEPTION, ESCALATION, OUTCOME), the relationship model with cardinalities, and the machine-readable graph schema.
- The case schema: the structure of a stitched end-to-end case, the unit that compilation consumes and that provenance reaches back to.
- The case stitching semantics: how fragmented events across systems become one case, and when stitching may join or must not join.
- The Digital Twin of Operations: the five aspects of the twin and the distinction from a knowledge graph.
- Drift detection: what counts as drift, at what latency it must be detected, and how a drift observation triggers the recalibration obligation declared in an AOP's Control dimension.
- The observation posture: the declared capture surface, the excluded content classes, and the minimisation rules that observation operates under.

## What this repository does not own

- The compiler that consumes the graph: the miners, extractors and the AOP generator. That is `aop-toolkit`.
- The runtime that emits execution evidence back into the graph. That is `aop-reference-harness`.
- The normative shape of the compiled AOP, including the `cg://` snapshot reference scheme. That is `aop-spec`, which this substrate serves.
- The change process and the decision records. That is `aop-governance`.

## Why this repository exists

It answers the hardest question in the programme: how does the system know what actually happens, as opposed to what a document claims happens? Everything above the substrate is downstream of this observation capability. Without it there is no variant mining, no reconciliation of intent against reality, and no way to know that a procedure has drifted. An AOP compiled from this graph is a measurement; the SOP it may have come from was a hypothesis.

## Documents

| Document | Scope |
|---|---|
| [The entity model](./docs/aop-entity-model-substrate-scope.md) | The ten entities, relationships, cardinalities, and the carried-forward metamodel vocabulary |
| [The case schema](./docs/aop-case-schema-substrate-scope.md) | The stitched case, its fields, and its machine-readable schema |
| [Case stitching](./docs/aop-case-stitching-substrate-scope.md) | Normalisation, case identity, join and anti-join rules, handoff integrity |
| [The Digital Twin of Operations](./docs/aop-digital-twin-substrate-scope.md) | The five aspects, the graph-versus-knowledge-graph distinction |
| [Drift detection](./docs/aop-drift-detection-substrate-scope.md) | Drift classes, detection latency, the recalibration trigger |
| [The observation posture](./docs/aop-observation-posture-substrate-scope.md) | Declared capture surface, excluded classes, minimisation, retention |
| [Process alignment](./docs/aop-process-alignment-substrate-scope.md) | Associating CASE, TASK and STEP with the OpenDEA Business Process Catalog, by reference or declared gap |

## Schemas

| Schema | Validates |
|---|---|
| [context-graph.schema.json](./schema/context-graph.schema.json) | A Context Graph of Work export: typed nodes, typed edges, per-type required attributes |
| [case-record.schema.json](./schema/case-record.schema.json) | A stitched case, including its provenance and outcome |
