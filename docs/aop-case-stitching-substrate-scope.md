# AOP Case Stitching (Substrate Scope)

Normative within the substrate tier. Case stitching is the operation that turns fragmented events, often across applications and actors, into the end-to-end cases the rest of the programme consumes. It is where observation becomes coherent, and it is the step most capable of quietly manufacturing false variants if done loosely. This document fixes the semantics.

## 1. Position in the pipeline

Stitching is the second half of the model stage of the pipeline (`aop-architecture`, compile-and-run pipeline): normalisation first, then stitching, then graph construction.

- Normalisation: source events from every declared capture surface are projected into the substrate's normal event form: timestamp, source, actor role, application, action, correlation hints. Source-specific details are retained as payload, never promoted to graph structure.
- Stitching: normalised events are joined into CASE, TASK, STEP instances under the rules below.
- Graph construction: stitched cases instantiate the entity model, with evidence attached per CG-2.

## 2. Case identity

CG-S1: A case is identified by the operational correlation key declared for the procedure family: the identifier that the domain itself uses to track one occurrence of the work (a fault ticket number, a claim reference, an order exception id). The key is declared per procedure family, with the source system that mints it.

CG-S2: Where a domain correlation key exists, it governs. Heuristic stitching (time windows, actor, application sequence) extends a key-stitched case; it never overrides the key.

CG-S3: Where no key exists, stitching is heuristic and every case stitched heuristically carries a stitching confidence attribute. Compilation MUST treat low-confidence cases as observations for pattern discovery, not as authoritative instances for thresholds (NM-STR-5 inputs).

## 3. Join rules

CG-S4: Events join into one case when they share the correlation key, directly or through a declared alias (a referenced ticket, a child task of a parent case).

CG-S5: Steps join into one task when they share the task-level correlation and occur within the declared task window. The window is declared per procedure family; it is configuration, not magic.

CG-S6: A step may be attributed to an ACTOR role only where the capture surface supplies the role. Where it does not, the step is carried with an unattributed marker. Guessing attribution to make the graph look complete is a defect, not a fill.

CG-S7: Cross-application stitching is the point of the exercise, not a special case. The interactions that never appear in API logs (UI-driven and legacy or VDI work) are exactly the steps the stitcher must not lose, and the declared capture surfaces exist to observe them.

## 4. Anti-join rules

CG-S8: Two cases with the same correlation key in disjoint time ranges are distinct cases, unless the domain declares case families (a fault that recurs and reopens). The `follows` relation between cases carries rework and family linkage; it does not merge cases.

CG-S9: Parallel unrelated work by the same actor in the same window does not join. Shared actor is not a join key.

CG-S10: An event that cannot be attributed to any case is quarantined with its reason. Unstitchable events are a first-class output: their rate is a quality metric of the capture surfaces, and their pattern is often the signature of undocumented work, which makes them mining input, not noise to be discarded.

## 5. Handoff integrity

CG-S11: A handoff between actors or systems, including a runtime handoff emitted by the harness (AOP-MM stage 07 vocabulary), is stitched as a STEP with a handoff attribute, or as an ESCALATION where the handoff transfers the decision to a human role. A handoff that breaks a case (the receiving side never observed) raises an incomplete-case marker on the case.

CG-S12: Incomplete cases are retained and marked, not discarded. The proportion of incomplete cases per family is a drift-relevant signal in its own right.

## 6. Versioning and determinism

CG-S13: Stitching is deterministic and versioned. The same input events under the same stitching version produce the same cases. A stitching version change that would alter case boundaries is a change request against this repository, because variant frequencies, thresholds and drift baselines are all computed from those boundaries.

CG-S14: Every case records the stitching version and the capture surface declaration version it was stitched under. Provenance must be able to answer not only which cases a rule came from, but under what observation rules those cases were formed.
