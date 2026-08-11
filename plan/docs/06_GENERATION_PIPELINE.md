---
category: feature
---

# TL100 Canonical-Construction Pipeline (Design v3)

> Status: binding Design v3 stage and interface specification.
>
> “Generation” is only one optional authoring operation inside this pipeline.

## 1. Purpose

TL100 constructs a provenance-rich relational stream around one situated acquisition path. The pipeline must make that path inspectable before it makes it large.

The system is not a one-shot story generator and not a broad web-ingestion pipeline. It combines deterministic record operations, deliberate source curation, optional model-assisted authoring, independent review, atomic canonical acceptance, reproducible compilation, and small-model experimentation.

## 2. Pipeline invariants

- Canonical chronology is append-oriented and never silently rewritten.
- A node cannot use tracked information without an allowed acquisition path.
- External source payloads retain source identity and bypass project-authored prose rewriting.
- Models propose records; they do not grant canonical status.
- Canonical state changes only through validated deltas.
- Source discovery does not imply source eligibility.
- Compilation does not mutate canon.
- Training and evaluation results inform later versions, never historical records.
- Throughput is irrelevant until the 100k–250k-token pilot survives full manual inspection.

## 3. Systems and trust boundaries

### 3.1 Deterministic core

Trusted for repeatable mechanics:

- schema resolution;
- identifier allocation;
- registry lookup;
- hash calculation;
- graph and chronology checks;
- state reconstruction;
- rights-policy enforcement;
- compilation and token accounting;
- manifest and report generation.

The core may contain bugs, so it must be versioned and tested. Its outputs are reproducible claims, not infallible truth.

### 3.2 Authoring and analysis tools

Humans, language models, scripts, simulators, and domain tools may propose:

- research objectives;
- source candidates;
- nodes and edges;
- claim and concept registrations;
- state deltas;
- project-authored payloads;
- technical reviews;
- counterfactual derivatives;
- evaluation items.

Every proposal records origin and tool/model identity.

### 3.3 Human authority

Named project reviewers decide:

- whether the acquisition path is scientifically useful;
- whether claims are scoped and supported;
- whether a source is appropriate;
- whether project rights decisions are sufficiently evidenced;
- whether relationships are genuine;
- whether prose or artifacts meet editorial and technical standards;
- whether a phase gate is passed.

Human approval cannot override a deterministic hard error without a versioned rule change.

## 4. Pipeline state machine

Each work package moves through:

```text
proposed
  -> structurally_valid
  -> review_ready
  -> reviewed
  -> accepted | rejected
  -> released
  -> compiled
  -> experimentally_evaluated
```

`rejected` proposals remain in authoring history but do not enter canon. `released` records are immutable. Revision after release creates new records and replacement metadata.

## 5. Stage 0 — Protocol freeze

### Inputs

- research question and hypothesis hierarchy;
- intended experimental factors;
- pilot token and model budgets;
- supported schema, validation, hash, rights, and compiler policy versions;
- predeclared evaluation families.

### Outputs

- protocol ID and content hash;
- declared independent and dependent variables;
- condition matrix;
- controlled variables and known residual confounds;
- stopping and scale criteria;
- approved toolchain identities.

No pilot content should be accepted until its protocol is identifiable. Exploratory changes are allowed, but they create a new protocol version and are reported as exploratory.

## 6. Stage 1 — Registry and dependency design

### Inputs

- bounded pilot domain;
- research protocol;
- existing accepted registries.

### Operations

- register the situated learner as an epistemic reference point;
- register recurring tools, environments, systems, projects, datasets, and participants only as needed;
- register important claims with scoped truth status;
- register concepts with prerequisite and competence criteria;
- design initial dependency, recurrence, correction, and transfer opportunities;
- identify unresolved questions worth carrying through the stream.

### Outputs

- proposed entity, claim, and concept records;
- proposed prerequisite graph;
- coverage and dependency report;
- unresolved design decisions.

This stage creates the vocabulary the rest of the pipeline may use. Authoring tools cannot invent a persistent ID while composing payloads.

## 7. Stage 2 — Source candidate registration

### Inputs

- claims and concepts needing grounding or encounter material;
- allowed source-selection policy;
- project storage boundaries.

### Operations

- identify creator, title, version, publisher, and locator;
- record acquisition method and timestamp;
- record intended roles independently from legal status;
- establish rights, training-use, redistribution, and storage decisions;
- segment coherent units without arbitrary token-driven chopping;
- calculate raw and normalized hashes where payload access is authorized;
- assess authority, fit, redundancy, and known limitations.

### Outputs

- source record proposals;
- immutable segment identities;
- source-review findings;
- explicit eligibility or fail-closed status.

External content remains outside project-authored payload fields. A source may be accepted as metadata while every segment remains ineligible for training.

## 8. Stage 3 — Acquisition scheduler

The scheduler chooses the next information need or recurrence objective, not prose.

### Inputs

- reconstructed acquisition state;
- unresolved questions;
- prerequisite graph;
- accepted project/investigation state;
- recurrence and transfer targets;
- source availability;
- pilot coverage and concentration reports;
- protocol constraints.

### Outputs

- scheduler decision ID;
- target claims/concepts/entities;
- intended epistemic function;
- required predecessors;
- candidate acquisition modes;
- desired later callbacks or assessments;
- “no useful next node” decision where appropriate.

The scheduler must be able to stop. It must not fabricate an encounter merely to satisfy a token quota.

## 9. Stage 4 — Encounter and node planning

The planner turns one scheduler decision into a small proposed subgraph.

### Inputs

- scheduler decision;
- current state snapshot;
- accepted registries and source records;
- hard graph constraints;
- anti-duplication report.

### Outputs

- node plan with node type and purpose;
- planned payload mode;
- exact record references;
- proposed edges and ordering constraints;
- proposed state operations;
- technical evidence requirements;
- review requirements;
- expected post-state assertions;
- possible failure or unresolved outcome.

A node plan may describe an observation, action, conversation, source encounter, artifact, reflection, assessment, or transition. It does not need a scene, character arc, or first-person narrator.

## 10. Stage 5 — Factual substrate

### Inputs

- approved node plan;
- eligible grounding sources;
- controlled measurements, simulations, calculations, or project definitions;
- current acquisition state.

### Outputs

- claim-scoped factual substrate;
- equations, values, units, conditions, uncertainty, and version boundaries;
- grounding record IDs;
- conflicts among sources;
- prohibited unsupported extensions.

The substrate separates what the authoring tool may rely on from what the learner has encountered. Grounding a payload with a source does not make that source available to the situated learner.

## 11. Stage 6 — Payload production or attachment

The operation depends on payload mode.

### Inline project-authored text

A human or model-assisted writer produces only the planned payload. The writer receives the current state, factual substrate, record references, and negative constraints. It may not invent persistent entities, sources, claims, or state changes.

### Artifact reference

An authorized process creates or captures the artifact, records its toolchain and environment, and stores it under the artifact policy.

### Source-segment reference

The pipeline attaches exact registered segment identities. External prose bypasses the project writer and editor. Context around the encounter may be separately authored, but source and project payloads keep distinct identities.

### Metadata-only node

No text is manufactured to make the record look substantial.

### Composite reference

The plan supplies an explicit immutable component order and combined normalized payload identity.

## 12. Stage 7 — Interpretive critics and revision

Independent roles are useful where their scopes are explicit.

### Technical critic

Checks scope, facts, equations, units, causal claims, uncertainty, and whether conclusions exceed evidence.

### Relational critic

Checks that proposed edges are meaningful, recurrence is not decorative, and callbacks or transfer claims have an identifiable shared structure.

### Epistemic critic

Checks whether payload assertions match the reconstructed acquisition state and whether uncertainty, hypotheses, corrections, and source attribution are represented honestly.

### Source-integrity critic

Checks source identity, segment boundaries, representation of the source, and suspicious copying into project-authored text. It does not rewrite external source prose.

### Editorial critic

Checks readability, information density, boilerplate, monotony, and genre fit without enforcing one synthetic narrator voice.

### Scientific critic

Checks whether the candidate strengthens the intended experimental manipulation or introduces an uncontrolled difference.

Critic findings are proposals with provenance. Revision changes only draft records and produces a revision chain. A critic score never grants acceptance.

## 13. Stage 8 — Deterministic validation

Run the gates in `07_CURATION_AND_QA.md` against the complete proposed atomic bundle:

- node;
- edges;
- any new registry records;
- state delta;
- expected post-state;
- stream item;
- source decisions and payload identities;
- review records.

The bundle must pass schema, reference, hash, graph, chronology, state, source, rights, and duplication checks before acceptance.

## 14. Stage 9 — Atomic canonical acceptance

Acceptance is one transaction:

1. lock the current canonical head;
2. verify its state and stream hashes;
3. rerun deterministic validation against that exact head;
4. write new immutable records;
5. append the stream item;
6. append or checkpoint the computed state;
7. update indexes;
8. write an acceptance receipt;
9. release the lock.

If any write or verification fails, no part of the bundle becomes canonical. Retrying against a changed head requires re-planning or revalidation.

## 15. Stage 10 — Release construction

### Inputs

- accepted canonical head;
- release selection boundary;
- schema and policy suite;
- warning dispositions;
- manual-review evidence.

### Outputs

- immutable release ID;
- exact record and payload inventory;
- ordered canonical stream inventory;
- schema, policy, validator, and source-registry hashes;
- reconstructed terminal state hash;
- exclusions, replacements, limitations, and rights summary;
- dataset card;
- release manifest and validation report.

Creating a release does not automatically create a training export.

## 16. Stage 11 — Deterministic compilation

The compiler consumes only an accepted release and explicit export configuration. It:

- resolves eligible payloads;
- normalizes and tokenizes them once;
- constructs one condition-independent packing plan for the primary 2x2;
- applies the declared cross-item attention policy;
- applies canonical or seeded-shuffle update order to complete packing groups;
- emits token, boundary, attention/position, loss-mask, and schedule artifacts;
- records exact exposure and source accounting;
- writes an export manifest;
- independently reproduces and validates the output.

See `08_CORPUS_FORMAT_AND_VERSIONING.md`.

## 17. Stage 12 — Training and evaluation

Training consumes the compiled schedule exactly. The loader must not add hidden global shuffling, dynamic packing, implicit replay, undocumented truncation, or boundary changes.

Evaluation reports:

- protocol and export IDs;
- architecture, initialization, tokenizer, optimizer, and runtime identities;
- every seed and checkpoint;
- aggregate and per-seed outcomes;
- evaluation-set provenance and leakage checks;
- failures and excluded runs;
- external-language or breadth penalties;
- deviations from the predeclared protocol.

The canonical corpus is never updated because a trained model produced a convenient answer.

## 18. Interface contract

Every stage invocation records:

- invocation ID;
- stage name and interface version;
- exact input record IDs and hashes;
- configuration hash;
- human/tool/model identity;
- deterministic seed where applicable;
- start and finish timestamps;
- output record IDs and hashes;
- warnings and failures;
- parent invocation IDs.

A stage accepts IDs and immutable payloads, not unversioned prose pasted from a previous stage.

## 19. Failure handling

- Deterministic failure produces a stable report and no canonical mutation.
- Interpretive rejection preserves the proposal and rationale outside canon.
- Source-rights failure removes payload eligibility, not source metadata history.
- Technical uncertainty becomes scoped truth status or an unresolved question; it is not polished away.
- Conflicting concurrent proposals rebase against the new canonical head.
- Tool or model unavailability is recorded; substituting a different tool changes invocation provenance.
- Partial compiler output is quarantined and cannot receive an accepted manifest.

## 20. Model-assisted authoring constraints

Before any model call, construct a bounded context containing only:

- registered records relevant to the plan;
- reconstructed learner state at the target position;
- approved factual substrate;
- source text permitted for the call's purpose;
- explicit negative constraints;
- requested output schema.

After the call:

- treat all returned IDs, facts, edges, and state changes as untrusted proposals;
- reject unknown persistent identities;
- detect copied source spans;
- validate structured output before editorial review;
- retain model, prompt, sampling, and tool provenance.

Model diversity may help detect correlated errors, but it is not a substitute for evidence or deterministic checks.

## 21. Pilot operating mode

For the 100k–250k-token pipeline pilot:

- use one bounded technical or investigative domain;
- keep entity, claim, concept, and source registries small enough to inspect completely;
- prefer project-authored or unambiguously approved source fixtures initially;
- manually inspect every node, edge, state delta, source encounter, and compiled span;
- include at least one misconception/correction chain, one source-to-application chain, one delayed callback, one assessment, and one transfer attempt;
- run the complete four-condition compiler even before interpreting model quality;
- train very small diagnostics before scaling corpus production.

The pilot succeeds when the data lineage and experimental controls are trustworthy, not when the prose is impressive.

## 22. Deferred capabilities

Do not prioritize yet:

- bulk model-generated content;
- automatic web or book ingestion;
- a graph database;
- a corpus dashboard;
- elaborate narrator-voice systems;
- mature mixture optimization;
- large distributed training;
- a 100M-parameter final run.

These become useful only after the canonical store, validator, compiler, and smallest experiments work end to end.
