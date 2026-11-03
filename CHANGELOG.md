# Changelog

All notable changes to this repository are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning is semantic: the major version changes when the entity model, the relationship set, or the case schema changes in meaning, the minor version when substantive substrate content is added, and the patch version for corrections that do not change meaning.

## [Unreleased]

## [0.1.0] - 2026-11-04

### Substrate foundation

- Published the entity model of the Context Graph of Work: the ten entities, the ten relationships with cardinalities, the evidence obligation (CG-2), and the alignment with the staged metamodel's runtime, exception and governance vocabularies.
- Published the case schema: the stitched case, its fields, the closed outcome dispositions, and the domain metrics the case corpus feeds.
- Published the case stitching semantics: case identity through domain correlation keys, join and anti-join rules, handoff integrity, quarantine of unstitchable events, and deterministic versioned stitching.
- Published the Digital Twin of Operations: the five aspects, the distinction from a knowledge graph, and the freshness obligation.
- Published the drift detection obligations: the five drift classes, declared drift profiles, detection latency, and the recalibration trigger that hands drift to governance.
- Published the observation posture: the declared capture surface, at-source exclusion of personal content classes, role-not-person modelling, minimisation, retention and access rules.
- Published the machine-readable schemas: the Context Graph export schema and the stitched case record schema, both validated by the shared reference validator in `aop-spec`.

[Unreleased]: https://github.com/agentic-operating-procedure/aop-context-graph/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/agentic-operating-procedure/aop-context-graph/releases/tag/v0.1.0
