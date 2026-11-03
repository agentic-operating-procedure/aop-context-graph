# AOP Digital Twin of Operations (Substrate Scope)

Informative. This document states what the Digital Twin of Operations is in this programme, the five aspects it carries, and the boundary it does not cross. The twin is the operating layer that the Context Graph of Work powers; this document explains the concept and its obligations, while the entity model and the schemas carry the structure.

## 1. The concept

The Digital Twin of Operations is a continuously updated, observable model of how the operational work is actually executed, built from the Context Graph of Work. It is a twin of the work, not of the organisation chart, not of the systems architecture, and not of any document.

The distinction from a knowledge graph bears repeating, because it decides what the twin can be used for. A knowledge graph models what is true (entities and facts). The twin models how work is executed: sequence, systems, decisions, dependencies, exceptions, and the reasons behind the paths taken. It answers what is happening and why this path. That is why it can compile procedures, detect drift, and compare agents against baselines, and why a knowledge graph cannot.

## 2. The five aspects

ARC-D1: A twin of operations in this programme carries five aspects, and a deployment missing one is not a twin in the sense this programme uses the term.

| # | Aspect | Meaning | Substrate owner |
|---|---|---|---|
| 1 | Observed execution | The work as performed: stitched cases, steps, roles, timings, outcomes | Entity model, case schema, stitching |
| 2 | Connected operational context | The applications, systems and interfaces the work flows through, including legacy and UI-driven surfaces the API view never shows | APPLICATION entity, capture surfaces |
| 3 | Cross-system visibility | One case traceable across every system it touched, end to end | Stitching join rules, handoff integrity |
| 4 | Variants and exceptions | The real path distribution: which paths run, how often, where the work leaves the anticipated flow, where it reworks | Evidence per node and edge (CG-2) |
| 5 | Continuous change detection | The twin notices when the work changes: new workarounds, shifting frequencies, rising exception rates | Drift detection obligations |

## 3. What the twin is used for

- **Compilation.** The variant inventory, the decision rules with their thresholds, and the exception patterns that `aop-toolkit` mines are read from the twin. The AOP is a measurement of the twin at a point in time, and its provenance block says which point (NM-PRV-1).
- **Shadow-mode evaluation.** Comparing agent choices with human choices (`aop-evaluation`) is done against the twin's case corpus and the human baseline it yields.
- **Drift response.** When the twin detects drift, the recalibration obligation declared in the AOP's Control dimension (NM-CTL-4) fires, and the loop produces a new AOP version.
- **Investigation.** After an incident or a conformance question, the twin answers how the work actually flowed, per case, with evidence.

## 4. What the twin is not

- It is not a surveillance system. The observation posture constrains capture to work activity on the declared surface; persons are not modelled (CG-1). The twin sees roles, steps and systems.
- It is not a record of truth about the business. It models execution of the procedures in its declared scope, not the enterprise.
- It is not a substitute for the systems of record. It observes them; it does not become one.
- It is not a mandate to adopt a particular product. The twin is defined by the five aspects and the substrate semantics; implementations satisfy them or they are not twins in this sense.

## 5. Freshness obligation

ARC-D2: The twin is updated continuously from the declared capture surfaces, not in periodic batches. A batch-built twin cannot detect drift at the rate work changes, which is the failure mode (coverage decay) the programme exists to escape. The freshness expectation per procedure family is declared configuration, and drift detection latency is measured against it.
