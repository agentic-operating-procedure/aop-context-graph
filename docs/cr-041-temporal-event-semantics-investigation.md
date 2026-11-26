# CR-041 Investigation: Temporal and Event Semantics Reconciliation

**Status:** Investigation proposal only; not a normative change or implementation decision.  
**Date:** 2026-11-26  
**Related:** AOP Governance CR-041; AO-WE-001 integration; governance acceptance proposal PR #29.  
**Authority:** This repository owns the Context Graph case schema and stitching semantics.

## Purpose

Map the temporal/event semantics needed to diagnose the fault-management fixture against existing normative material, identify ambiguities or gaps, and define an evidence-first disposition. This investigation must not edit or regenerate fixture data, change schema compatibility, or prescribe event ordering without domain evidence and owner review.

## Existing contract that must be preserved and considered

- Case-schema documentation defines cycle time as `ended_at - started_at` and says per-task/per-step decomposition should be carried.
- Case schema has `started_at`, `ended_at` and step `timestamp` fields; current schema patterns are date-prefix and non-empty string constraints, not a complete timezone-aware timestamp format contract.
- Stitching semantics describe normalization into an event form with timestamp/source/actor-role/application/action/correlation hints; source details remain payload.
- Stitching uses domain correlation keys where present; heuristic joining extends keys, not overrides; task windows are declared per procedure family.
- Case stitching is deterministic and versioned; incomplete cases are retained and marked; unstitchable events are quarantined with reasons.
- Case provenance includes source events, capture-surface declaration version and stitching version; corpus quality includes sampling, cohort, date range, missingness and coverage gaps.

## Questions to resolve with evidence

1. **Temporal field identity:** Is the existing `timestamp` intended to be event occurrence time, capture/observation time, source-system record time, or a declared canonical time? If multiple are materially required, determine whether additional fields or retained source payload are needed.
2. **Timezone and precision:** Define accepted timezone/offset and precision requirements for case boundaries and event timestamps, including interpretation of legacy/local timestamps. Do not infer a timezone for existing records.
3. **Ordering:** Separate procedural precedence, event chronology, capture order and source sequence where they differ. Array order alone must not be assumed to encode multiple meanings.
4. **Concurrency:** Determine how concurrent or overlapping steps/events are represented without artificial serial ordering.
5. **Case boundaries:** Define whether event occurrence time governs interval membership; classify delayed capture, pre-run observations, post-run evidence, reopened cases, and handoff events. Decide how exceptions are typed and justified.
6. **Duration semantics:** Existing normative case-cycle definition is elapsed end-start. Distinguish that from active-work duration, task duration, queue/wait duration or other metrics, with explicit units and provenance if those are needed.
7. **Integrity and traceability:** Preserve source timestamp, source identity, capture time (if available), transformation, adjudication rationale, and event inclusion/exclusion decisions sufficient to reproduce the case.

## Evidence reconciliation protocol

Before a fixture repair is proposed, pin:

- corpus file blob SHA and commit SHA;
- validator implementation commit/version and exact command;
- diagnostic definitions and whether they examine all timestamps or a subset;
- timezone/offset and precision assumptions (or absence thereof);
- per-case diagnostic output with event identities, not only aggregate counts;
- case-owner adjudication for legitimate boundary exceptions and branch/order behavior.

The aggregate discrepancy between CR-041 and AO-WE-001 diagnostics is not resolved in this investigation. Neither set of counts should be promoted as authoritative until this protocol is completed.

## Deliverable proposal

Following owner review, either:

- a narrowly scoped normative clarification to the case/stitching semantics and schema (with compatibility assessment and tests), or
- a documented finding that existing semantics are adequate, with a traceable toolkit validator gap and no unnecessary schema changes.

No automatic timestamp normalization, event sorting, boundary clipping, deletion, or fixture regeneration is permitted as a conclusion of this investigation alone.

## Dependencies and boundary

Governance acceptance of CR-041 is proposed, not ratified (see AOP governance PR #29). This investigation is suitable for review in parallel but implementation changes should be sequenced behind the accepted CR and approved semantic disposition. Domain-specific fault-management branch/authority decisions remain with their owners and are not decided here.
