# AOP Case Schema: The Stitched Case (Substrate Scope)

Normative within the substrate tier. The case is the unit that compilation consumes, the unit that provenance reaches back to (NM-PRV-1 to NM-PRV-4), and the unit the runtime's case record is modelled on. This document states the case schema; the machine-readable form is `schema/case-record.schema.json`.

## 1. The case

A case is one end-to-end occurrence of the operational work. It is stitched from events that may span applications, actors and hours, and it is the smallest unit that carries an outcome.

CG-C1: Every case carries a stable identifier, unique within the observation estate, in the form the `cg://` scheme references: `cg://case/<case-id>@<timestamp>` (NM-CTX-2, NM-ID-5). The timestamp pins the graph state the reference resolves to.

CG-C2: Every case carries:

| Field | Meaning |
|---|---|
| `case_id` | Stable identifier |
| `procedure` | The operational procedure family the case belongs to (for example `fault-management`) |
| `started_at`, `ended_at` | Case boundaries |
| `tasks` | The ordered tasks, each with its steps |
| `actor_roles` | The roles that participated, never named persons (CG-1) |
| `decisions` | The decision points, with branch condition and evidence |
| `exceptions` | The exceptions raised, with class and severity where observable |
| `escalations` | The escalations triggered, with target role and reason |
| `outcome` | Result, cycle time, cost per case |
| `provenance` | Source events, capture surface declaration version, stitching version |

CG-C3: The outcome dispositions at case level use the same closed set as the run level in `aop-spec` (NM-STR-14): `achieved`, `partially_achieved`, `not_achieved`, `achieved_with_deviation`, `inconclusive`. An unclassifiable outcome is `inconclusive`, never silently dropped.

## 2. Metrics the case carries

Every case contributes to the domain metrics that the AOP's human baseline (NM-ASR-2) and `aop-evaluation` are computed from:

- Cycle time: ended_at minus started_at, and per-task and per-step decomposition.
- First-pass resolution: whether the outcome was `achieved` without rework loops firing and without exception beyond the anticipated set.
- Exception rate: exceptions per case, per variant, per application.
- Escalation precision: of the cases escalated, the proportion where escalation was retrospectively warranted.
- Cost per case: where the estate supplies cost data.

These metric names and definitions are the substrate's contribution to `aop-evaluation`; the metric registry and the published results are owned there, per the repository map.

## 3. Relationship to the runtime case record

The runtime case record that the harness appends to (SEC-8, NM-ASR-1) is a case of the same schema family: the run's inputs, context snapshot, rule, provenance, decision, approver and outcome are the runtime projection of the case fields above. The reason is the closed loop: execution evidence must land in the substrate as a first-class case (ARC-P5 in `aop-architecture`), not as a foreign import, or the next compile would treat agent work as second-class observation.

## 4. What the schema does not fix

The schema does not fix the event schemas of capture sources, the stitching algorithm's implementation, or the storage format at rest. It fixes what a stitched case must carry so that compilation, provenance and evaluation all read the same unit.
