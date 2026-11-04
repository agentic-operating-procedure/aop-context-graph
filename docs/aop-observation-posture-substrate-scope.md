# AOP Observation Posture (Substrate Scope)

Normative within the substrate tier. Observation is a privileged activity: it watches work as it happens, across systems, including surfaces that were never designed to be observed. This document fixes the posture observation operates under. The AOP-side obligations it serves are NM-CTX-3 and NM-CTX-4; the architecture-side constraints are ARC-P1 and ARC-C4.

## 1. The stance

You model the work, not the person. Observation exists to answer how the work is executed, and nothing in the substrate needs a named individual to answer it. Everything else in this document follows from that stance.

## 2. The declared capture surface

CG-O1: Observation operates on a declared subset of the work surface. The declaration is per estate, is versioned, and enumerates: the applications and interfaces observed, the interaction classes captured on each (API events, UI actions, screen-context signals), and the procedure families in scope. Anything not declared is not captured. The declaration version is recorded in every case's provenance (CG-S14).

CG-O2: The capture surface is designed to see the work that the API view misses: cross-application flows, UI-driven steps, and legacy or VDI interactions. Seeing that work is the reason the substrate exists; seeing persons is not, in any form.

## 3. Excluded content classes

CG-O3: The following are excluded from capture by design, at the source, not by later filtering: message and email body content, keystroke content, free-form personal notes, and any content class the estate's privacy review names for its jurisdiction. At-source exclusion means the substrate never holds the content, so no later bug can leak it.

CG-O4: Screen-context capture, where declared, captures the work-context signals (application, window class, object under work) and not the content of documents being read or written. The boundary between a work-context signal and content is part of the capture surface declaration, and the privacy review approves that boundary, not the substrate code.

## 4. Minimisation, retention and access

CG-O5: Roles, not persons: the ACTOR entity carries a role (CG-1). Where a source event carries a person identifier, normalisation projects it to the role or to the unattributed marker (CG-S6) and discards the identifier. The substrate does not hold a person-to-role map.

CG-O6: Retention is declared per estate: how long raw events, stitched cases and drift observations are kept. The default posture is that raw events age out once stitched, cases persist for compilation and evaluation, and nothing is kept that no stage of the pipeline consumes.

CG-O7: Access to the substrate is role-based and audited. The twin is not generally browsable; queries against it are for the programme's stages (compile, evaluate, investigate) and for the governance reviews the estate requires.

CG-O8: These rules bind the runtime's observation too: the case records the harness emits (SEC-8) land in the substrate under the same posture. Agent execution gets no wider capture rights than human execution had.

CG-O9: Observation operates only under a declared lawful basis for the capture surface, and only after the consultation the basis requires (employee representative or works-council consultation where the jurisdiction provides for it) is complete and recorded. The declaration version carries both, and capture does not begin until they are present. A privacy review approval (section 4) is necessary but not sufficient: the lawful basis and the consultation are recorded facts, not implied ones.

CG-O10: Contestability. An operator or affected party can contest a derived rule or a data use through the estate's governance: the contest is filed as a finding against `aop-governance`, the contested artefact's ratification is reviewed, and the outcome (uphold, amend, withdraw) is recorded. Contesting is a governed act with a record, not an off-channel complaint.

CG-O11: Quarantine on provenance failure. Where source identity or integrity verification fails (CG-S17), the affected events and cases are quarantined with the failure reason, compilation consuming them fails closed, and the quarantine is a recoverable incident record (CR-020, CR-025).

## 5. What the posture does not fix

The posture fixes what may be captured and held. It does not replace the estate's legal review, its regulatory obligations, or its jurisdiction-specific privacy law compliance. Each estate's declaration is expected to be approved by its own privacy review; the substrate carries the declaration and enforces the rules above, and it refuses to operate where no declaration exists.
