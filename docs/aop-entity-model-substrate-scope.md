# AOP Entity Model: The Context Graph of Work (Substrate Scope)

Normative within the substrate tier. This document states the entity model of the Context Graph of Work and the relationships between entities. The compiled AOP that `aop-toolkit` produces must be traceable to instances of these entities; the identifier and provenance clauses in `aop-spec` (NM-PRV-1 to NM-PRV-4) bind that traceability.

## 1. What the graph is

The Context Graph of Work models how work is executed: sequence, systems, decisions, dependencies, exceptions, and the reasons behind the paths taken. It answers what is happening and why this path.

The contrast is deliberate. A knowledge graph answers what is true. The Context Graph of Work answers how work actually flows. It is built from observed operational activity and updated continuously, not in periodic batches, because a batch-built graph cannot detect drift at the rate work changes.

## 2. The entities

Ten entity types. Every node in the graph is exactly one of them, and every node carries evidence: which cases traversed it, how often, at what cost, and with what outcome.

| Entity | Definition | Key attributes |
|---|---|---|
| CASE | One end-to-end occurrence of the operational work, stitched from events | case id, start, end, channel, source events |
| TASK | A unit of work within a case, the level at which responsibility is assigned | task id, name, owner role |
| STEP | One observed action within a task: the atomic unit of execution | action, application, actor role, timestamp |
| ACTOR | The role (not the named person) that performed a step | role id, role name |
| APPLICATION | The system in which a step executed | application id, interface class (API, UI, legacy/VDI) |
| DECISION | A choice point observed in the work, with the condition evaluated | branch condition, evidence |
| RULE | The inferable rule a decision instantiates, before compilation names it | candidate condition, threshold observations |
| EXCEPTION | An observed departure from the anticipated path | condition, class, severity |
| ESCALATION | A transfer of the case to a human decision-maker | target role, reason, bundle reference |
| OUTCOME | The terminal result of a case | result, cycle time, cost per case |

Two modelling rules bind the whole model:

CG-1: The graph models roles, not persons. The ACTOR entity carries a role. Named individuals do not appear in the graph. This is the substrate side of the observation posture and of NM-CTX-4.

CG-2: Every node and edge carries evidence: the case references that instantiate it, the observed frequency, and the observed cost and outcome distributions where applicable. A node without evidence is not part of the graph; it is an unverified claim.

## 3. The relationships

| From | To | Relationship | Cardinality |
|---|---|---|---|
| CASE | TASK | contains | 1 to N |
| TASK | STEP | comprises | 1 to N |
| STEP | ACTOR | performedBy | N to 1 |
| STEP | APPLICATION | executesIn | N to 1 |
| STEP | DECISION | evaluates | 1 to N |
| DECISION | RULE | applies | N to M |
| STEP | EXCEPTION | raises | 1 to N |
| EXCEPTION | ESCALATION | triggers | 1 to N |
| CASE | OUTCOME | produces | 1 to N |
| CASE | CASE | follows | N to N, rework and case families |

The relation set is closed. A relationship type not in this table is a change request against this document, because the compiler in `aop-toolkit` and the runtime in `aop-reference-harness` key their behaviour to exactly these edges.

## 4. Alignment with the staged metamodel

The ten entities are the substrate's core, carried forward from the framing documents' entity-relationship model. The staged metamodel's richer vocabulary aligns as follows, and is referenced, not duplicated:

- The runtime entities (AOP-MM stage 07, E61 to E75: AOP Run, Execution Context, Runtime Event, Runtime Handoff, Runtime Evidence Record, Run Outcome, and the rest) are runtime-tier vocabulary. Their substrate-side shadows are: a Runtime Event arrives as a source event, a Runtime Handoff appears as a STEP with a handoff attribute or as an ESCALATION, a Runtime Evidence Record lands as an OUTCOME attribute, and the Run Outcome maps to OUTCOME.
- The exception, recovery and resilience entities (stage 08, E76 to E86) refine EXCEPTION: the exception class, severity and recoverability attributes declared there are the vocabulary the substrate's EXCEPTION carries where observation can supply them.
- The governance entities (stage 09, E87 to E103) do not appear in the graph; governance evidence lives in the estate's repositories, not in the observation substrate.

Where a metamodel term and a substrate term could be confused (notably EXCEPTION versus Exception Occurrence, and OUTCOME versus Run Outcome), the substrate term governs inside this repository and the mapping above resolves the correspondence.

## 5. What the model does not fix

The model fixes what the entities are and how they relate. It does not fix the event schemas of the capture sources, the storage engine, the query interface, or the mining methods. Capture-source normalisation is defined in the stitching document as far as the substrate is concerned; the executable parts belong to `aop-toolkit` and the runtime.
