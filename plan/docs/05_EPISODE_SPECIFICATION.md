---
category: feature
---

# TL100 Canonical Record and Schema Specification (Design v3)

> Status: binding Design v3 record contract.
>
> This document replaces the Design v2 episode-first specification.

## 1. Purpose

TL100 stores a reviewed relational learning history, not a fictional biography. The canonical unit is therefore a typed node, not an episode or prose genre.

This document maps the architecture in `01_WORLD_AND_CONTINUITY.md` to machine-readable records. It defines the first schema boundary, field ownership, record relationships, and example requirements. Compilation policy is specified separately.

## 2. Schema principles

All canonical schemas must:

- declare JSON Schema draft 2020-12;
- use stable `https://tl100.local/schemas/...` identifiers;
- reject undeclared properties;
- include an explicit schema version;
- use opaque, type-prefixed project identifiers;
- use full `sha256:` content identities rather than placeholders in accepted records;
- distinguish record metadata from training payloads;
- preserve provenance and review state;
- leave cross-record and temporal invariants to a deterministic validator where JSON Schema is insufficient.

Schema validity is necessary but not sufficient for canonical acceptance.

## 3. Canonical record suite

| Schema | Record responsibility |
|---|---|
| `common.schema.json` | Shared identifiers, hashes, statuses, provenance, and review records |
| `entity.schema.json` | Stable identity for recurring actors, objects, systems, environments, projects, datasets, and tools |
| `claim.schema.json` | Stable propositions and controlled truth status |
| `concept.schema.json` | Reusable abstractions, prerequisites, and competence criteria |
| `source.schema.json` | External-source identity, provenance, rights, storage, and immutable segments |
| `artifact.schema.json` | Inspectable code, logs, tables, measurements, configurations, and other payload-bearing artifacts |
| `node.schema.json` | Independently reviewable information-bearing events or objects |
| `relation_edge.schema.json` | Reviewed typed relations and ordering constraints |
| `state_delta.schema.json` | Ordered, evidence-bearing acquisition-state transitions |
| `state_snapshot.schema.json` | Reconstructable state checkpoints |
| `stream_item.schema.json` | One exact canonical placement of an accepted node |
| `replacement.schema.json` | Explicit non-destructive correction and migration history |
| `acceptance_receipt.schema.json` | Atomic acceptance transaction, reviewed bundle, validation evidence, and state transition |
| `validation_report.schema.json` | Deterministic gate results and stable machine-readable findings |
| `release_manifest.schema.json` | Immutable release inventory, policies, rights snapshot, graph/state anchors, and dataset card |
| `tokenizer_manifest.schema.json` | Complete glass-box tokenizer algorithm, corpus, vocabulary, implementation, and artifact identity |
| `decision_record.schema.json` | Inspectable owner decisions, alternatives, evidence, risks, and failure tests |
| `dependency_boundary.schema.json` | Borrowed component behavior, defaults, scientific effects, and conformance tests |
| `token_span.schema.json` | Condition-independent atomic tokenized payload span |
| `packing_group.schema.json` | Condition-independent physical context packing unit |
| `update_schedule_item.schema.json` | Exact epoch, optimizer, batch, slot, group, and exposure placement |
| `export_manifest.schema.json` | Exact compiled view, policies, inputs, token accounting, and output identities |

`common.schema.json` is a definition library and is not itself instantiated.

## 4. Record ownership

### 4.1 Nodes own meaning-bearing events

A node owns:

- event/object type;
- purpose;
- payload mode and payload identity;
- semantic references to entities, claims, concepts, sources, and artifacts;
- an optional proposed state delta;
- creation and review provenance.

A node does not own canonical ordinal, training-window placement, optimizer order, or export token offsets.

### 4.2 Stream items own canonical placement

A stream item owns:

- canonical stream identity;
- ordinal and optional simultaneous group;
- referenced node;
- state-before and state-after identities;
- whether the node supplies a training payload in the canonical view.

The same immutable source segment may be encountered in several nodes. Each encounter has its own node and stream item while retaining the segment's content identity.

### 4.3 Export manifests own experimental transformations

An export manifest owns:

- selected release and records;
- compiler, environment, normalization, and tokenizer identities;
- condition-independent selection, atomic spans, and packing-plan identities;
- the two declared experimental factors;
- exact token, attention, position, loss-mask, batch-slot, and update-schedule artifacts;
- deterministic seeds and epoch count;
- unique, exposure, boundary, padding, loss-bearing, and excluded-token accounting;
- source eligibility decision and validation artifacts;
- known deviations and the final manifest hash.

Export operations never mutate canonical nodes or stream order.

## 5. Node records

### 5.1 Node types

The initial closed vocabulary is:

- `encounter`;
- `observation`;
- `action`;
- `conversation`;
- `source_encounter`;
- `artifact`;
- `reflection`;
- `assessment`;
- `transition`.

This vocabulary describes epistemic function, not literary genre.

### 5.2 Payload modes

- `inline_text`: accepted project-authored text stored in the node;
- `artifact_reference`: one registered artifact provides the payload;
- `source_segment_reference`: ordered registered source segments provide external payloads;
- `metadata_only`: the node changes structure or records a boundary without emitting text;
- `composite_reference`: ordered immutable components provide the payload.

The payload discriminated union prevents a metadata-only event from silently carrying text and prevents external prose from being embedded as project-authored text.

### 5.3 References

Node reference arrays are explicit and unique. Their existence and correct registry kind are validator responsibilities. Referencing a source does not by itself grant source-text inclusion rights.

## 6. Entities, claims, and concepts

Entities provide stable recurrence identity. Stable and stateful properties are structured values, but assertions important to the experiment should also have claim IDs so their evidence and truth status can be audited.

Claims separate controlled truth from learner stance. Claim records contain truth status; snapshots contain what was available and what stance was recorded at a given stream point.

Concepts identify abstractions or skills. Their records specify prerequisites and observable competence criteria. Exposure and competence belong to learner-state snapshots, not the concept definition.

## 7. Source records

A source record contains no implicit permission. It records:

- bibliographic identity and acquisition provenance;
- origin and intended role;
- rights status, license evidence, redistribution decision, and training-use decision;
- storage mode;
- immutable segment locators and hashes;
- segment-level eligibility decisions.

The deterministic rights gate may be stricter than schema validity. In particular, `unknown`, `review_required`, and `not_approved` decisions cannot yield training text in a releasable export.

Source segments identify coherent units. Segment records do not embed copyrighted prose. A payload locator points to approved repository or local storage where policy permits.

## 8. Relation edges

Each relation edge states endpoint kinds as well as IDs. The validator checks the allowed endpoint matrix from the architecture specification.

Edge type, ordering constraint, and visibility are independent fields. A causal relationship is not inferred from adjacency, and a semantic edge may remain canonical while its textual bridge is removed from an experimental export.

## 9. Acquisition-state deltas

State changes use a closed operation vocabulary. Operations are ordered because later operations in one accepted delta may depend on earlier ones.

Each operation records its target and evidence-bearing references. A `change_claim_stance` operation records both previous and new stance. A competence update cites at least one accepted evidence node. A source encounter identifies exact immutable segments.

Every delta declares:

- triggering node;
- pre-state hash;
- ordered operations;
- expected post-state hash;
- validation and review decisions.

The validator applies the operations and rejects the delta unless its computed post-state hash matches.

## 10. State snapshots

Snapshots are deterministic projections, not psychological profiles. They track only registered, experiment-relevant state:

- claim availability, stance, confidence category, acquisition modes, and evidence;
- concept exposure and demonstrated competence;
- source segment encounters and exposure counts;
- known or uncertain entity properties;
- open, resolved, reframed, or abandoned questions.

Map keys are canonical IDs. The validator checks that each key resolves and that each `last_changed_by` node is at or before the snapshot position.

## 11. Canonical stream

Canonical stream ordinals are unique and contiguous within a release candidate. Hard relation constraints must be satisfied by their order.

For a state-changing item:

```text
prior state_after_hash == current state_before_hash
apply referenced node delta
computed state hash == current state_after_hash
```

For a non-mutating item, state-before equals state-after. A metadata-only boundary cannot mutate state without an explicit delta.

## 12. Operational acceptance and release records

An artifact record is the canonical boundary for code, tables, measurements, logs, datasets, and other non-source objects. A payload-bearing artifact declares repo or authorized-local storage, raw and normalized hashes, training eligibility, and redistribution eligibility. Metadata-only artifacts are never training- or redistribution-approved by implication. Externally authored artifacts must link to at least one source record; their local eligibility fields cannot bypass that source's rights decision.

Acceptance is atomic. An acceptance receipt binds the reviewed record bundle, prior and new canonical heads, exact state transition, validation report, reviewer evidence, and transaction identity. A partly written bundle has no canonical effect.

Released records are immutable. A correction appends a replacement record naming the old and new identities, reason, affected releases, effective release, and migration guidance. It never rewrites the historical record.

A release manifest freezes the complete record and stream inventories, schema and policy hashes, source/rights snapshot, state endpoints, graph summary, payload inventory, warning dispositions, dataset card, and validator identity. `accepted_at` is mandatory for an accepted release and absent for a draft.

## 13. Glass-box and compiler records

Tokenizer manifests record the algorithm at the level needed for an independent implementation: byte alphabet, pretokenizer, target and achieved vocabulary, pair counting, tie breaking, merge replacement order, normalization, exact training corpus, vocabulary hashes, special tokens, two implementation identities, tests, metrics, parameter costs, decision, and validation report. A byte-only tokenizer is constrained to 256 lexical tokens and zero merges.

Decision records preserve alternatives as well as conclusions. Dependency-boundary records make every borrowed primitive inspectable by declaring inputs, outputs, determinism, defaults, limitations, scientific effects, ownership, and tests.

The compiler emits three JSONL record streams before opaque arrays:

- token spans bind each normalized payload component to its stream item, node, source/segment if any, exact token count, boundary tokens, exposure index, and hashes;
- packing groups bind intact spans into fixed-capacity, condition-independent physical groups;
- update-schedule items bind those groups to epochs, optimizer positions, batches, slots, exposures, and deterministic shuffle keys.

Token, attention, position, and loss layouts are described as hashed tensor artifacts with explicit encoding, semantics version, dtype, shape, and endianness. Their human-readable JSONL parents remain available for inspection.

## 14. Export manifests

Every training export is reproducible from one accepted release plus a manifest. The manifest distinguishes:

- canonical selection from derived payloads;
- physical packing from attention visibility;
- canonical, shuffled, or declared custom whole-group update order;
- unique payload tokens from repeated exposures, boundaries, padding, and excluded payloads;
- declared condition factors from the identities of materialized arrays and schedules.

The four primary condition names are schema-bound to their exact factor values. A manifest called `relational_ordered`, for example, cannot declare blocked cross-node attention or shuffled packing-group updates.

The manifest references the complete token-span and packing-plan audit trail rather than duplicating it. Every array and JSONL file is content-addressed, typed, counted, and schema-identified where applicable. Cross-record validation recomputes shapes, totals, hashes, schedule legality, and equality of all controlled variables across matched conditions.

## 15. Cross-record invariants

JSON Schema cannot establish all required properties. The deterministic validator must additionally enforce:

- every reference exists and has the declared record kind;
- identifiers are globally unique and never reused;
- accepted hard-order edges are acyclic;
- stream ordinals satisfy hard constraints;
- deltas form one valid state-hash chain;
- acquisition precedes use unless explicitly marked as hypothesis or prior assumption;
- competence changes cite accepted evidence;
- source-segment hashes match stored payloads;
- source inclusion satisfies rights and storage policy;
- accepted and released payload hashes match normalized content;
- acceptance receipts refer only to one completely validated, reviewed transaction;
- replacement records preserve type identity and do not create replacement cycles;
- released records are immutable;
- release inventories, state endpoints, policy identities, and payload accounting reproduce exactly;
- tokenizer totals, merge counts, special-token IDs, and artifacts agree;
- packing counts sum to capacity and tensor shapes agree with the packing plan;
- schedule entries cover the declared exposure multiset exactly;
- export token counts, array semantics, order, and hashes reproduce exactly;
- matched conditions differ only in declared attention layout and whole-group update schedule.

## 16. Example fixture

The `examples/` directory contains one small, non-fictional measurement chain:

1. a registered instrument entity;
2. a controlled claim about measurement loading;
3. a concept with a prerequisite;
4. a project-authored source record whose segment is rights-approved;
5. a source-encounter node;
6. an acquisition edge;
7. a delta that makes the claim available and records the source encounter;
8. the resulting state snapshot;
9. a canonical stream item;
10. a project-authored artifact;
11. an explicit replacement record;
12. a deterministic validation report and atomic acceptance receipt;
13. an immutable release manifest;
14. a glass-box tokenizer manifest, decision record, and dependency boundary;
15. an atomic token span, packing group, and update-schedule item;
16. an exact export manifest referencing all compiled artifacts.

The examples demonstrate shape, not scientific evidence. Their hashes are syntactically valid fixture identities and must never be mistaken for computed production hashes.

`examples/schema-fixtures.json` is the executable fixture index. Positive cases map each example to its schema. Each negative case derives from one valid example through exactly one JSON-Pointer mutation and declares the expected failing keyword. Materializing mutations in memory keeps valid/invalid pairs synchronized and proves that only one fact changed.

## 17. D2 migration

The former `episode` and `reading_event` schemas are withdrawn.

- An episode becomes one or more typed nodes.
- A reading event becomes a `source_encounter` node plus explicit source segments, edges, and any justified state delta.
- A narrator knowledge block becomes a state snapshot or delta.
- Episode class and narrator voice are optional authoring concerns outside canonical identity.

Migration is explicit; old records do not become D3-valid merely by renaming fields.

## 18. Completion criteria

This schema layer is ready for implementation when:

- every schema parses under draft 2020-12;
- every example validates against its named schema;
- every declared one-fact negative mutation fails on the expected keyword;
- all external references resolve locally without network access;
- the example chain has internally resolvable IDs;
- no schema requires a fictional person, setting, age, or narrator;
- external source prose cannot be silently stored as inline project-authored text;
- deterministic invariants not expressible in JSON Schema are enumerated for the validation layer.
