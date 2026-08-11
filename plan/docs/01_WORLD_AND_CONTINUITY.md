---
category: feature
---

# TL100 Canonical Graph and Acquisition-State Specification (Design v3)

> Status: binding Design v3 architecture for canonical records and state.
>
> This document replaces the Design v2 fictional world-and-continuity specification.

## 1. Purpose

TL100 needs a machine-readable account of:

- what information-bearing items exist;
- how those items relate;
- when they become available in the canonical stream;
- what the situated learner could know at each point;
- what the learner accepts, doubts, rejects, or has not yet encountered;
- which later events apply, revise, or transfer earlier information;
- which transformations a training export applies without altering canon.

The canonical object is a directed, typed graph plus one reviewed canonical stream.

The graph is not a fictional biography database. It is an experimental substrate for constructing, validating, transforming, and evaluating relational training data.

## 2. Scope

This specification defines:

- canonical node identity and lifecycle;
- persistent entity identity;
- claim and concept identity;
- typed graph edges;
- acquisition and belief state;
- demonstrated competence state;
- state deltas and snapshots;
- chronology and ordering constraints;
- canonicality and release immutability;
- provenance and content identity;
- graph queries needed by validators and compilers.

This specification does not define:

- prose voice;
- a fictional town or cast;
- a human developmental simulation;
- final file formats;
- training architecture;
- optimizer behavior;
- export algorithms;
- source rights policy details;
- evaluation datasets.

Those concerns reference this architecture but are specified elsewhere.

## 3. Design principles

### 3.1 Separate truth from learner state

For an important claim, TL100 may need to represent all of the following independently:

- controlled-environment truth;
- whether the information was available;
- how it became available;
- the learner’s current stance;
- evidence supporting or conflicting with that stance;
- whether the learner has demonstrated competent use;
- whether later information superseded an earlier formulation.

No single knowledge flag can represent these distinctions.

### 3.2 Preserve acquisition paths

Important information must have a traceable path from an accepted node to a learner-state transition.

If the learner uses a claim before any valid acquisition path makes it available, the corpus is invalid unless the use is explicitly represented as a guess, hypothesis, or prior assumption.

### 3.3 Prefer categorical state over invented precision

Do not assign numeric belief probabilities merely to make the data appear rigorous.

Use categorical stance and confidence labels unless a number is:

- measured;
- explicitly reported by the learner;
- produced by a defined scoring process;
- required by an approved experiment.

### 3.4 Keep canon independent of training views

The canonical graph records accepted relationships and acquisition order.

A training export may:

- shuffle windows;
- mask cross-node attention;
- omit selected bridges;
- replay nodes;
- create a declared counterfactual derivative.

Those transformations belong to export records. They do not mutate canonical nodes or edges.

### 3.5 Make hard constraints deterministic

Schema validity, referential integrity, ordering, rights eligibility, hashes, and declared state transitions must be checkable without a language model.

Interpretive quality may still require human or model review.

## 4. Identifier namespaces

Identifiers are opaque, stable, and namespaced by record type.

Recommended prefixes:

| Record | Prefix | Example |
|---|---|---|
| canonical node | node_ | node_000001 |
| relation edge | edge_ | edge_000001 |
| persistent entity | ent_ | ent_instrument_meter_01 |
| claim | claim_ | claim_supply_drops_under_load |
| concept | concept_ | concept_measurement_loading |
| source | source_ | source_meter_manual_01 |
| source segment | segment_ | segment_meter_manual_safety |
| state snapshot | state_ | state_000014 |
| state delta | delta_ | delta_000014 |
| stream item | stream_ | stream_000021 |
| artifact | artifact_ | artifact_voltage_log_01 |
| release | release_ | release_pilot_001 |
| export | export_ | export_pilot_relational_ordered_001 |
| replacement | replace_ | replace_node_000014_001 |

Identifiers:

- never encode mutable display names;
- never encode a stream ordinal that may change before release;
- never get reused;
- remain resolvable after supersession;
- are unique within the project.

## 5. Canonical node model

A canonical node is the smallest independently reviewable information-bearing event or object placed in the relational graph.

### 5.1 Required conceptual fields

Every node records:

- node ID;
- schema version;
- node type;
- canonical status;
- concise purpose;
- payload mode and payload identity;
- referenced entities;
- referenced claims and concepts;
- source references where applicable;
- proposed state-delta reference;
- provenance;
- content hash;
- creation and review metadata.

Stream placement is recorded by stream items, not embedded as node identity.

### 5.2 Initial node types

#### Encounter

A bounded situation through which information becomes available.

Examples:

- encountering an unexpected instrument reading;
- receiving a recommendation;
- inspecting an artifact;
- observing a failed procedure.

#### Observation

A recorded perception or result without requiring a causal interpretation.

An observation should distinguish:

- raw or minimally processed result;
- measurement conditions;
- units and uncertainty where applicable;
- linked artifact or instrument.

#### Action

An intervention, procedure, or attempted change.

Actions can succeed, fail, or produce ambiguous results.

#### Conversation

An information exchange among identified participants.

Conversation nodes may contain multiple viewpoints. Only explicitly linked acquisition deltas change learner state.

#### Source encounter

A canonical encounter with one or more registered source segments.

The source payload remains externally authored and independently identified.

#### Artifact

A code file, log, table, specification, diagram, configuration, calculation, or other structured object whose form matters.

#### Reflection

An interpretation, comparison, hypothesis, explanation, plan, or stated uncertainty derived from information currently available.

#### Assessment

A test, probe, prediction, or task intended to provide evidence about learner competence or an experimental hypothesis.

#### Transition

A metadata-bearing boundary used to record a justified change in phase, environment, or availability when no training payload is required.

### 5.3 Node payload modes

A node may be:

- **inline text** — small accepted payload stored with the record;
- **artifact reference** — payload stored as a structured artifact;
- **source segment reference** — external content addressed through the source registry;
- **metadata only** — canonical event with no training text;
- **composite reference** — ordered references to immutable component payloads.

The payload mode determines which hashes and eligibility checks apply.

### 5.4 Node atomicity

A node should be small enough to:

- review independently;
- attach precise graph edges;
- identify state changes;
- compile under different context-boundary policies.

A node should be large enough to preserve:

- coherent source boundaries;
- measurement conditions;
- conversational meaning;
- causal interpretation;
- artifact structure.

Token quotas must not force arbitrary fragmentation.

## 6. Persistent entity registry

Entities provide stable reference identity across nodes.

Initial entity classes:

- situated learner;
- participant or actor;
- physical object;
- instrument;
- system or machine;
- environment or location;
- project or investigation;
- organization;
- dataset;
- software component;
- model;
- source creator or publisher where needed.

An entity record contains:

- entity ID;
- entity class;
- display label;
- stable properties;
- stateful properties;
- first valid appearance;
- current status;
- aliases;
- provenance;
- forbidden contradictions where deterministic;
- replacement or merge history.

Entities do not require fictional characterization.

A recurring meter, dataset, codebase, collaborator, or test environment is an entity because identity across encounters matters experimentally.

## 7. Claim registry

A claim is a stable proposition whose availability, truth status, and learner stance may change over the stream.

Examples:

- the supply voltage falls under a defined motor load;
- the parser treats a missing value as zero;
- the current dataset split leaks project identity;
- negative feedback always stabilizes a system.

### 7.1 Claim fields

Each claim records:

- claim ID;
- canonical statement;
- scope and conditions;
- truth status;
- truth authority or evidence basis;
- concept references;
- supersedes or refines relationships;
- version sensitivity;
- review status.

### 7.2 Truth-status vocabulary

Initial truth statuses:

- true in controlled environment;
- false in controlled environment;
- conditionally true;
- unresolved;
- contested;
- source-reported only;
- not applicable.

Truth status may change only through an explicit versioned correction or a defined environment change.

### 7.3 Claims versus text spans

A node may express several claims, and a claim may appear in several nodes.

Claim identity is semantic and reviewed. It is not inferred solely from string equality.

The project must avoid creating a unique claim ID for every paraphrase.

## 8. Concept registry

A concept is a reusable abstraction or skill target rather than a proposition.

Examples:

- reference surface;
- measurement loading;
- state machine;
- train-validation-test separation;
- causal confounding.

Concept records include:

- concept ID;
- name;
- operational description;
- prerequisite concept IDs;
- boundary or non-example notes;
- expected evidence of competence;
- transfer targets;
- version and review status.

Concept prerequisites create graph constraints but do not automatically imply mastery.

## 9. Relation-edge model

Edges express reviewed relationships between canonical records.

### 9.1 Required conceptual fields

Every edge records:

- edge ID;
- edge type;
- source record ID;
- target record ID;
- source and target record kinds;
- design rationale;
- ordering constraint;
- evidence or reviewer basis;
- visibility class;
- canonical status;
- provenance.

### 9.2 Edge endpoint types

Edges may connect:

- node to node;
- node to claim;
- claim to claim;
- concept to concept;
- node to concept;
- node to entity;
- source segment to node;
- state snapshot to delta;
- replacement record to superseded record.

Allowed endpoint combinations are defined by schema and validator rules.

### 9.3 Edge types

#### Temporal

The source precedes the target in canonical time.

Temporal edges can be:

- immediate;
- before;
- not-after;
- simultaneous group;
- interval overlap.

#### Causal

The source caused or materially contributed to the target under the controlled scenario.

Causal edges require a rationale and must not be created merely because two events are adjacent.

#### Prerequisite

The source concept or information is expected to support comprehension or performance at the target.

Prerequisites may be:

- hard;
- recommended;
- preview allowed.

#### Entity recurrence

The endpoints concern the same persistent entity in a way relevant to continuity or evaluation.

#### Project continuation

The target continues an objective, constraint, or unresolved state established at the source.

#### Acquisition

The source node makes a claim, concept, procedure, or source segment available to the learner state.

#### Belief support

The source provides evidence supporting an existing or candidate learner stance.

#### Belief conflict

The source provides evidence inconsistent with an existing stance.

#### Correction

The target explicitly revises, rejects, narrows, or supersedes a prior learner stance or claim formulation.

#### Source application

The target applies information from an earlier registered source encounter.

#### Memory or callback

The target intentionally reuses an earlier encounter after an interval.

This edge is about designed recurrence, not a claim of human memory phenomenology.

#### Analogy or transfer

The target applies an underlying structure to a meaningfully different surface domain.

Transfer edges require a statement of:

- source structure;
- target structure;
- surface difference;
- evaluation intent.

### 9.4 Ordering constraints

Each edge declares one of:

- strict before;
- not after;
- same stream group;
- unconstrained;
- derived from another hard edge.

Hard ordering edges must form an acyclic constraint graph.

Semantic edges may be cyclic where appropriate, but their ordering constraints may not introduce a hard cycle.

### 9.5 Edge visibility

An edge may be:

- explicit in payload text;
- inferable from adjacent payloads;
- metadata only;
- withheld from training but used for evaluation;
- export-dependent.

This field supports tests of whether metadata-designed relationships survive when textual bridges are removed.

## 10. Acquisition state

Acquisition state describes what information is available to the situated learner at a point in the canonical stream.

It is not a hidden mental simulation.

### 10.1 State dimensions

For tracked claims:

- availability;
- stance;
- confidence category where justified;
- acquisition modes;
- supporting evidence references;
- conflicting evidence references;
- supersession status;
- last changed by.

For tracked concepts:

- exposure state;
- demonstrated competence;
- supporting assessment or application references;
- transfer evidence;
- last changed by.

For sources:

- encountered segments;
- encounter nodes;
- reread or reference count;
- notes or unresolved questions where recorded.

For entities:

- known properties;
- uncertain properties;
- observed state;
- last valid update.

### 10.2 Availability vocabulary

- unavailable;
- available but unattended;
- encountered;
- partially processed;
- available through reference;

“Available but unattended” is permitted only when an artifact or source is accessible in the controlled environment without implying that its contents were learned.

### 10.3 Stance vocabulary

- no recorded stance;
- hypothesized;
- uncertain;
- tentatively accepted;
- accepted;
- rejected;
- superseded;
- intentionally unresolved.

Unavailable claims normally have no recorded stance.

### 10.4 Confidence categories

When needed:

- low;
- medium;
- high;
- not recorded.

Numeric confidence is prohibited unless generated by an explicit method recorded in provenance.

### 10.5 Acquisition modes

- observation;
- measurement;
- conversation;
- source reading;
- artifact inspection;
- experiment;
- inference;
- explanation or teaching;
- prior assumption;
- correction.

Several modes may contribute to one state transition.

## 11. Demonstrated competence

Availability and belief do not establish competence.

Concept competence uses evidence-bearing categories:

- not exposed;
- exposed;
- recognized with support;
- applied with support;
- applied independently;
- explained accurately;
- transferred;
- contradicted by assessment;

A competence transition requires a referenced node or assessment.

The system must permit:

- accepted belief without practical competence;
- correct action without correct explanation;
- memorized explanation without transfer;
- temporary regression;
- domain-specific competence without general mastery.

## 12. Questions and unresolved state

Open questions are first-class records or claims with unresolved status.

They record:

- question ID or claim ID;
- originating node;
- current candidate explanations;
- evidence gathered;
- blocked prerequisites;
- current status;
- resolution or abandonment node if any.

The graph must support questions that:

- resolve immediately;
- remain open across many nodes;
- are reframed;
- are answered conditionally;
- are abandoned without resolution.

## 13. State deltas

A node does not mutate state directly.

It proposes a state delta.

### 13.1 Delta operations

Initial operations:

- make claim available;
- record claim stance;
- change claim stance;
- add supporting evidence;
- add conflicting evidence;
- supersede claim stance;
- expose concept;
- record demonstrated competence;
- record source segment encounter;
- update known entity property;
- open question;
- update question;
- resolve question;
- add unresolved uncertainty.

### 13.2 Delta requirements

Every delta records:

- delta ID;
- triggering node ID;
- pre-state hash;
- ordered operations;
- expected post-state hash;
- rationale;
- validation status;
- human review status where required.

### 13.3 Acceptance protocol

1. Load the accepted pre-state.
2. Validate the triggering node and referenced records.
3. Validate each operation against allowed transitions.
4. Apply operations deterministically.
5. Compute the post-state hash.
6. Compare it with the declared post-state hash.
7. Reject on mismatch.
8. Commit the accepted node, delta, edges, stream item, and post-state atomically.

Partial canonicalization is prohibited.

## 14. State snapshots

State snapshots provide deterministic checkpoints over accumulated deltas.

A snapshot records:

- state ID;
- schema version;
- stream position;
- previous snapshot ID;
- included delta range;
- claims state map;
- concepts state map;
- source encounter map;
- entity-known-state map;
- open questions;
- snapshot hash.

Snapshots may be full or incremental, but the reconstruction procedure must be deterministic.

The project should be able to rebuild any release state from:

- initial state;
- accepted ordered deltas;
- schema versions;
- migration records.

## 15. Chronology

### 15.1 Stream position

Every accepted canonical placement receives:

- stream item ID;
- release-scoped ordinal;
- node or boundary reference;
- canonical phase or block where used;
- state before;
- state delta;
- state after.

### 15.2 Time representation

The initial micro-life may use:

- ordinal only;
- relative time index;
- controlled experiment time;
- explicit timestamp when naturally meaningful.

Real-world dates and simulated ages are not required.

### 15.3 Chronology invariants

- Ordinals are unique and strictly increasing within a release.
- Hard temporal and acquisition edges agree with stream order.
- A correction follows the stance it corrects.
- A source application follows the relevant source encounter.
- An assessment used as competence evidence is at or before the transition it supports.
- State-before of one state-changing item equals the prior accepted state-after.
- Metadata-only boundaries cannot silently mutate acquisition state.

## 16. Canonical status and lifecycle

Record statuses:

- draft;
- under review;
- accepted;
- rejected;
- superseded;
- withdrawn before release.

Only accepted records enter a release.

### 16.1 Before release

Drafts may be revised in place while preserving authoring provenance.

Accepted-but-unreleased material may be withdrawn through explicit review state.

### 16.2 After release

Released records are immutable.

A correction creates:

- a new record;
- a replacement record;
- a reason;
- affected releases;
- migration guidance;
- new hashes;
- a new release or export.

Historical manifests remain resolvable.

## 17. Provenance

Every canonical record contains provenance appropriate to its origin.

For project-authored nodes:

- planner or author identity;
- model and prompt versions where used;
- grounding references;
- creation timestamp;
- revision chain;
- reviewers;
- acceptance decision.

For external sources:

- creator;
- title;
- version;
- locator;
- acquisition method;
- rights fields;
- source and segment hashes;
- storage mode.

For derived records:

- parent record IDs;
- transformation type;
- transformation configuration;
- tool version;
- deterministic seed where applicable.

Provenance metadata is never part of the training payload unless an experiment explicitly includes it.

## 18. Content identity and hashing

Hashes distinguish:

- record envelope;
- normalized training payload;
- raw stored payload;
- external source segment;
- state snapshot;
- compiled export.

Normalization rules must be versioned and must specify:

- Unicode normalization;
- newline normalization;
- text encoding;
- trailing whitespace policy;
- field ordering for structured records;
- canonical JSON serialization.

Changing normalization rules requires a new hash-policy version.

## 19. Canonical graph invariants

The validator must enforce at minimum:

- all referenced IDs exist in the correct registry;
- ID namespaces are unique;
- accepted hard-order edges are acyclic;
- stream order satisfies hard constraints;
- acquisition use follows availability;
- corrections reference an existing prior stance;
- source applications reference encountered eligible segments;
- competence transitions cite evidence;
- pre-state and post-state hashes chain;
- content hashes match payloads;
- superseded records remain resolvable;
- released records are immutable;
- no export-only transformation is written back into canon.

## 20. Required graph queries

The implementation must support deterministic queries for:

- all predecessors required before a node;
- all nodes involving an entity;
- first and latest encounter of a claim, concept, source, or entity;
- all acquisition paths for a claim;
- learner stance at stream position T;
- evidence supporting or conflicting with a stance;
- all corrections and the beliefs they supersede;
- all source-to-application paths;
- all callbacks beyond a specified interval;
- all transfer edges;
- all unresolved questions at T;
- all nodes affected by replacing a record;
- all graph edges exposed or hidden in an export.

These queries support validation, compilation, evaluation generation, and manual review.

## 21. Training-view relationship

Canonical records state what relationships exist.

Export manifests state which relationships the model can access and how.

Examples:

- Related nodes may share one attention context.
- A boundary mask may prevent cross-node attention while preserving token order.
- Windows may be globally shuffled while preserving local node packing.
- A node may be replayed with an explicit exposure count.
- Metadata-only acquisition events may affect canonical order without contributing tokens.

The compiler must never infer canonical relationships from file adjacency alone.

## 22. Counterfactual and delinked derivatives

Content-matched relational-ablation experiments may require rewritten payloads.

Such material is not alternate canon.

It is a derived experimental dataset with:

- derivative ID;
- parent node IDs;
- transformation objective;
- removed or replaced edge classes;
- semantic-equivalence review;
- token-matching report;
- authoring provenance;
- known residual confounds.

Derived payloads cannot be used to update canonical learner state.

## 23. Migration from Design v2

Design v2 records may migrate as follows:

| Design v2 concept | Design v3 treatment |
|---|---|
| episode | one or more canonical nodes |
| narrator knowledge | acquisition state |
| person, place, machine | optional persistent entity |
| memory | callback edge |
| mistake | claim stance plus later conflict or correction |
| project arc | project entity plus continuation edges |
| reading event | source-encounter node plus acquisition delta |
| concept arc | concept record plus evidence-bearing nodes and edges |
| chronological episode list | canonical stream constrained by graph |

Alex, Rookfield, ages, personality traits, and the proposed fictional cast do not migrate automatically.

Migration requires explicit IDs, provenance, and review. Detail in a legacy document is not evidence of canonical validity.

## 24. Minimal implementation boundary

The first operational substrate needs:

- registries for entities, claims, concepts, and sources;
- canonical node records;
- typed relation-edge records;
- state-delta records;
- reconstructable state snapshots;
- stream-item records;
- deterministic hash policy;
- release and replacement records.

It does not yet need:

- a graph database;
- a web interface;
- model-generated prose;
- a large source library;
- a 100M-parameter training run.

JSONL plus deterministic indexes is an acceptable initial storage model if it satisfies the required queries and integrity checks.

## 25. Design completion criteria

This architecture is ready for schema implementation when:

- node and edge types are reflected in machine-readable schemas;
- allowed edge endpoints are enumerable;
- state transitions have a closed operation vocabulary;
- example records reconstruct one valid state chain;
- one invalid example exists for each hard invariant class;
- the compiler can reference nodes without depending on prose genre;
- no schema requires a fictional biography.
