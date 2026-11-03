# AOP Drift Detection (Substrate Scope)

Normative within the substrate tier. Drift is the divergence between the work as last compiled and the work as currently observed. Drift detection is the substrate's alarm for the coverage-decay failure mode: the silent widening of the gap between document and work that the programme exists to escape. This document fixes what counts as drift, the detection obligations, and how a drift observation becomes a recalibration.

## 1. Drift classes

CG-D1: The substrate detects drift in five classes, and every drift observation records its class.

| Class | Definition | Typical signal |
|---|---|---|
| Variant drift | A new path appears, or a path's frequency shifts beyond its declared band | A previously unseen step sequence crossing the frequency floor |
| Threshold drift | The observed values around a decision point move relative to the threshold compiled into the AOP | Escalations clustering at values the compiled rule would not escalate |
| Exception drift | The exception rate or exception mix changes | A known exception firing more often, or a new exception signature |
| Workaround drift | Undocumented paths consolidate into repeated patterns | Unstitchable and unattributed events forming a stable shape (CG-S10) |
| Coverage drift | The capture surface stops seeing work it used to see | Falling case volume in a family without a business cause |

The last class is included deliberately: the twin's own observation can decay, and a drift detector that watches only the work and never the lens is half a detector.

## 2. Detection obligations

CG-D2: Drift detection runs continuously against the twin (ARC-D2). It is not a report run at review time.

CG-D3: Every procedure family carries a declared drift profile: per class, the band or threshold that separates normal movement from drift. The profile is configuration owned with the procedure family, and the compiled AOP's drift obligation (NM-CTL-4) references the same bands.

CG-D4: Detection latency is measured per class, per family, from the first observed case that constitutes drift to the drift observation. The declared latency target is part of the drift profile. Latency is one of the domain metrics `aop-evaluation` measures.

CG-D5: A drift observation is a first-class record in the substrate: class, family, the cases that evidence it, the band crossed, and the time of detection. It is evidence, and it lands in the case corpus like any other observation.

## 3. From drift to recalibration

CG-D6: A drift observation triggers the recalibration obligation declared in the affected AOP's Control dimension (NM-CTL-4). The substrate raises the trigger; what happens next is governance, not substrate behaviour: recalibration produces a new AOP version through `aop-toolkit` and lands through `aop-governance` (NM-ASR-4, ARC-P6). The substrate never mutates an AOP.

CG-D7: Recalibration of the drift profile itself (tightening or loosening a band) is a change against this repository, because variant frequencies and thresholds are computed against those bands. It cannot be done casually by the runtime that happens to find the band inconvenient.

## 4. What drift detection is not

It is not anomaly detection in the security sense: drift is change in the work, whether or not anyone is to blame, and most drift is ordinary operational evolution. It is not incident management: a drift observation is a signal to re-derive the procedure, not a page to an on-call engineer. And it is not the AOP's exception handling: exceptions are per-case and handled at run time under the AOP's Control dimension; drift is per-population and handled by recalibration.
