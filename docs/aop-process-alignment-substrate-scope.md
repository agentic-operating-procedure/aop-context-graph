# AOP Process Alignment: Associating the Substrate with the DEA Process Catalog (Substrate Scope)

Normative within the substrate tier. This document states how the substrate's CASE, TASK and STEP entities associate with the enterprise process catalog deployed from the OpenDEA Business Process Catalog (`technehub-labs/dea-catalog-business-processes`). It exists so that every observed case, task and step can be read against the enterprise's own process architecture, and so that operational work observed in the substrate is attributable to the process levels the enterprise recognises.

## 1. The association model

The DEA catalog decomposes processes across levels with stable entity identifiers of the form `processes:process-*`, `processes:activity-*` and `processes:task-*`. The substrate's execution hierarchy maps onto that decomposition one level down:

| Substrate entity | DEA catalog level | Identifier form |
|---|---|---|
| CASE | Process | `processes:process-*` |
| TASK | Activity | `processes:activity-*` |
| STEP | Task | `processes:task-*` |

CG-PA-1: A case SHOULD carry a `process_ref` pointing at the `processes:process-*` entry the case is an occurrence of, and each task SHOULD carry a `process_ref` pointing at the `processes:activity-*` entry the task instantiates. Where the catalog's decomposition goes to task level and observation can resolve it, a step MAY carry a `processes:task-*` reference.

CG-PA-2: The association is by reference and never by copy. The substrate records the catalog identifier and the catalog version it was resolved against; it does not duplicate process definitions, classifications or descriptions into the AOP estate. The DEA catalog remains the single authority for what the process is (the same rule the repository map states for sibling organisations).

CG-PA-3: Every case and task records the catalog version its references were resolved against (`process_catalog_version` in the case provenance). A reference is only as good as the version it points into; provenance must be able to answer what the process looked like when the work was observed.

## 2. Reference and gap

CG-PA-4: Where a canonical catalog entry exists for the work, the reference is mandatory at the level the catalog supports, and the estate uses the canonical identifier exactly as the catalog publishes it.

CG-PA-5: Where no canonical entry exists, the case or task carries an explicit gap declaration instead of an invented identifier: the work is described, and the missing entry is lodged as a contribution to the DEA catalog through that catalog's own contribution process. Inventing a process identifier is prohibited: a fabricated reference is worse than a declared gap, because it poisons the alignment silently.

CG-PA-6: Gap declarations are a work queue. The substrate reports the work observed under gap declarations, per catalog level, so that the enterprise can see which of its operational processes lack a canonical entry and prioritise the contributions. A gap that stays open across catalog versions is itself a drift signal worth escalating.

## 3. What alignment gives the estate

- **Reading work against architecture.** A case corpus grouped by `process_ref` is the enterprise's process architecture as it actually runs, which is the input the Digital Twin of Operations serves to business stakeholders.
- **Scoping AOPs.** A procedure compiled from cases aligned to one `processes:process-*` entry inherits a defensible scope boundary (NM-INT-2), stated in the enterprise's own vocabulary.
- **Metrics that bind.** The DEA metrics catalog binds performance metrics to `dea:BusinessProcess`. A case corpus with process references makes the AOP's human baseline (NM-ASR-2) and the evaluation results computable against those canonical metrics. The AOP-side of this binding is the `process_alignment` block in `aop-spec` (NM-INT-4 to NM-INT-5), which carries the same reference-or-gap rule.

## 4. What this alignment does not do

It does not make the DEA catalog an authority over AOP content: the catalog says what the enterprise's processes are; the AOP estate says how agents are governed executing them. It does not require the catalog to model agent-specific concepts; the mapping is substrate-to-catalog, never catalog-to-substrate. And it does not couple the substrate's schemas to the catalog's schemas: the reference is an identifier plus a version, so either side can evolve independently.
