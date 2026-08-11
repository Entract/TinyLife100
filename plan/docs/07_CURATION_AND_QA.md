---
category: feature
---

# TL100 Deterministic Validation, Rights, and Review Gates (Design v3)

> Status: binding Design v3 validation policy.
>
> This document replaces the Design v2 life-prose QA checklist.

## 1. Purpose

TL100 must be able to distinguish:

- structurally valid records;
- internally consistent canon;
- legally and operationally eligible source payloads;
- reproducible training exports;
- scientifically matched experimental conditions;
- interpretive quality that still requires human judgment.

A validator should reject a malformed corpus without asking a language model. A language model or human may help assess meaning, but neither may waive a hard integrity failure.

## 2. Validation principles

### 2.1 Fail closed

Missing evidence, unknown rights, unresolved references, unknown schema versions, hash mismatches, and ambiguous compilation settings block acceptance or export.

### 2.2 Deterministic before interpretive

Run cheap, deterministic checks before technical review, similarity analysis, model critics, or human review. Interpretive work should not be spent on a candidate that already fails identity or chronology.

### 2.3 No scalar quality score

TL100 does not collapse correctness, rights, provenance, relational quality, and prose quality into one score. Hard failures and review judgments remain separate dimensions.

### 2.4 No silent waiver

A hard error cannot be waived inside a record. If a rule is wrong, change the versioned policy, revalidate, and create a new release candidate. Historical reports remain immutable.

### 2.5 Validate the requested artifact

Canonical validation and export validation answer different questions. Canonical validity does not guarantee that a particular export is rights-eligible, reproducible, or experimentally matched.

## 3. Validation outputs

Every run emits a machine-readable report containing at minimum:

- report ID;
- validator name, version, and git commit;
- validation-policy version;
- schema-suite hash;
- input release or candidate ID;
- input manifest hash where applicable;
- start and finish timestamps;
- deterministic configuration hash;
- ordered findings;
- counts by severity and code;
- pass/fail decision for each gate;
- overall result;
- report content hash.

Each finding records:

- stable error or warning code;
- severity;
- record ID and source path;
- JSON Pointer or byte/token range where available;
- related record IDs;
- concise observed value;
- expected invariant;
- deterministic evidence;
- suggested remediation class.

Reports must sort findings by gate, record kind, record ID, field path, and code so identical inputs produce byte-identical reports after timestamps are excluded from the report identity calculation.

## 4. Severity model

### Error

An invariant is false or required evidence is absent. Errors block the relevant phase gate.

### Warning

A measurable risk or review trigger exists, but deterministic evidence does not establish invalidity. Warnings require disposition before release.

### Information

A metric or trace useful for audit, without an implied defect.

Warnings never become errors merely because their count is inconvenient. Thresholds must be versioned, justified, and tied to a concrete risk.

## 5. Stable code namespaces

Codes use `TL100-<DOMAIN>-<NNN>`.

| Domain | Meaning |
|---|---|
| `FMT` | File, serialization, or schema failure |
| `ID` | Identifier uniqueness or namespace failure |
| `REF` | Missing or wrong-kind reference |
| `CAN` | Canonical status, replacement, or immutability failure |
| `HASH` | Content, state, manifest, or output identity failure |
| `GRAPH` | Edge endpoint, cycle, or relationship failure |
| `TIME` | Stream ordinal or chronology failure |
| `STATE` | Invalid delta or snapshot transition |
| `EPI` | Acquisition-path or epistemic-state failure |
| `SRC` | Source identity, segment, or provenance failure |
| `RIGHTS` | Rights, storage, training-use, or redistribution failure |
| `DUP` | Unaccounted duplication or copying signal |
| `EXP` | Export selection, compilation, token, or output failure |
| `MATCH` | Experimental-control mismatch |
| `REV` | Required review absent or inconsistent |

Codes are append-only within a policy major version. A code's meaning cannot be repurposed.

## 6. Gate order

The validator runs these gates in order:

1. file discovery and serialization;
2. schema validation;
3. identity and referential integrity;
4. canonical lifecycle and immutability;
5. content identity and hash policy;
6. graph and chronology;
7. acquisition-state reconstruction;
8. source provenance and rights;
9. duplication and source leakage;
10. export reproduction;
11. matched-condition audit;
12. interpretive and human-review disposition.

A gate may stop after a failure if later results would be misleading. The report records skipped gates explicitly.

## 7. File and schema gate

### 7.1 Deterministic checks

- Every discovered structured file decodes as UTF-8 without replacement characters.
- JSON parses without duplicate object keys.
- Record-to-schema routing is unambiguous.
- The declared schema version is supported.
- The correct draft-2020-12 schema validates the complete record.
- All local `$ref` targets resolve without network access.
- No unregistered schema file changes the active suite hash.
- JSONL files contain exactly one complete JSON object per non-empty line.

### 7.2 Core failures

| Code | Condition |
|---|---|
| `TL100-FMT-001` | Invalid UTF-8 |
| `TL100-FMT-002` | Invalid JSON or JSONL framing |
| `TL100-FMT-003` | Duplicate JSON object key |
| `TL100-FMT-004` | Unsupported or absent schema version |
| `TL100-FMT-005` | JSON Schema validation failure |
| `TL100-FMT-006` | Unresolvable or network-dependent schema reference |
| `TL100-FMT-007` | Record kind cannot be routed to one schema |

## 8. Identity and reference gate

The validator builds immutable indexes before resolving relationships.

Checks include:

- project-wide ID uniqueness;
- prefix matches record kind;
- no ID reuse after rejection, withdrawal, supersession, or release;
- every reference resolves;
- referenced record kind matches the field and declared endpoint kind;
- source-segment IDs are unique project-wide, not only within one source;
- ordered lists do not contain duplicate IDs unless the field explicitly models exposure;
- self-reference is rejected except where a schema and policy explicitly permit it.

| Code | Condition |
|---|---|
| `TL100-ID-001` | Duplicate project identifier |
| `TL100-ID-002` | Identifier prefix does not match record kind |
| `TL100-ID-003` | Retired identifier reused |
| `TL100-REF-001` | Referenced ID does not exist |
| `TL100-REF-002` | Referenced ID has the wrong record kind |
| `TL100-REF-003` | Prohibited self-reference |
| `TL100-REF-004` | Duplicate reference where uniqueness is required |

## 9. Canonical lifecycle gate

### 9.1 Status consistency

- `accepted` canonical records have an accepted review and decision timestamp.
- `draft` and `under_review` records cannot enter a release.
- `rejected` or `withdrawn_before_release` records cannot be referenced by accepted stream items.
- `superseded` records remain resolvable but cannot enter a new export unless the manifest explicitly targets a historical release that contained them.

### 9.2 Release immutability

For every released record, compare the record-envelope hash and payload hashes with the release manifest. Any byte-affecting change is rejected. Corrections require new records and an explicit replacement path.

| Code | Condition |
|---|---|
| `TL100-CAN-001` | Canonical status conflicts with review decision |
| `TL100-CAN-002` | Non-accepted record included in release candidate |
| `TL100-CAN-003` | Superseded or withdrawn record used as current canon |
| `TL100-CAN-004` | Released record changed in place |
| `TL100-CAN-005` | Replacement history is missing, cyclic, or unresolved |

## 10. Hash and normalization gate

### 10.1 Hash domains

TL100 uses distinct SHA-256 identities for:

- raw stored bytes;
- normalized training payload;
- canonical record envelope;
- state snapshot;
- selected-record set;
- compiler configuration;
- tokenized output;
- export manifest;
- validation report.

Each hash calculation uses an explicit domain prefix and policy version so equal bytes in different domains are not treated as the same object identity.

### 10.2 Text normalization v1

For normalized text payloads:

1. decode UTF-8 strictly;
2. remove a leading UTF-8 byte-order mark if present and report it;
3. normalize Unicode to NFC;
4. convert CRLF and bare CR to LF;
5. preserve all other whitespace, including final newlines;
6. encode as UTF-8 without a byte-order mark.

No case folding, trimming, punctuation rewriting, comment removal, or source cleaning occurs implicitly. Artifact-specific canonicalization requires a different named policy.

### 10.3 Record envelopes

Record envelopes use RFC 8785 JSON canonicalization after excluding the envelope's own `content_hash` field. State, manifest, and report identities similarly exclude only their own identity field. The policy forbids non-finite numbers.

| Code | Condition |
|---|---|
| `TL100-HASH-001` | Raw payload hash mismatch |
| `TL100-HASH-002` | Normalized payload hash mismatch |
| `TL100-HASH-003` | Record-envelope hash mismatch |
| `TL100-HASH-004` | State hash mismatch |
| `TL100-HASH-005` | Manifest hash mismatch |
| `TL100-HASH-006` | Export output hash mismatch |
| `TL100-HASH-007` | Unsupported or inconsistent normalization policy |

## 11. Graph gate

### 11.1 Endpoint matrix

The validator maintains a versioned allowed endpoint matrix. At minimum:

- temporal, causal, recurrence, continuation, application, callback, and correction edges connect valid information-bearing records;
- prerequisite edges originate from claims or concepts and target claims, concepts, nodes, or assessments as declared by policy;
- acquisition edges originate from a node or source segment and target a node, claim, concept, or delta-compatible acquisition point;
- belief-support and belief-conflict edges target a tracked claim or stance-bearing node;
- source-application edges have an earlier accepted source encounter;
- analogy/transfer edges include all four transfer fields.

### 11.2 Ordering graph

Build a graph from `strict_before`, `not_after` where inequality becomes strict between distinct groups, and derived hard constraints. Reject hard cycles. Semantic cycles are permitted only when they do not imply an impossible order.

| Code | Condition |
|---|---|
| `TL100-GRAPH-001` | Edge type uses a prohibited endpoint combination |
| `TL100-GRAPH-002` | Hard ordering constraints contain a cycle |
| `TL100-GRAPH-003` | Required edge rationale or evidence is empty |
| `TL100-GRAPH-004` | Transfer edge lacks a meaningful transfer specification |
| `TL100-GRAPH-005` | Source application has no valid prior encounter path |

## 12. Chronology gate

- Stream item IDs and ordinals are unique.
- Ordinals are contiguous from zero within a release candidate.
- Every stream item references one accepted node.
- Every accepted state-changing node appears exactly once in the canonical stream unless replay is modeled by a distinct encounter node.
- Stream order satisfies all hard graph constraints.
- Same-group items agree on a simultaneous group and do not contain internal strict-before conflicts.
- Evidence nodes and assessments occur no later than the transition they support.
- Metadata-only nodes cannot silently change state.

| Code | Condition |
|---|---|
| `TL100-TIME-001` | Duplicate or non-contiguous ordinal |
| `TL100-TIME-002` | Stream order violates a hard edge |
| `TL100-TIME-003` | Invalid simultaneous group |
| `TL100-TIME-004` | Evidence appears after the transition it supports |
| `TL100-TIME-005` | State-changing accepted node has invalid stream multiplicity |

## 13. Acquisition-state gate

### 13.1 Reconstruction

Starting from the declared genesis state, process stream items in canonical order:

1. compare the item's `state_before_hash` with current state;
2. load the node's referenced delta if present;
3. compare the delta pre-state hash with current state;
4. apply operations in listed order;
5. enforce operation-specific transition rules;
6. canonicalize and hash the computed state;
7. compare with both delta expected post-state and stream item state-after;
8. checkpoint when a snapshot is declared;
9. reconstruct checkpoints independently and compare full state, not only hashes.

### 13.2 Transition rules

- A claim cannot move from `unavailable` to a stance other than `no_recorded_stance` without first becoming available in the same or an earlier delta.
- `change_claim_stance` previous stance must equal reconstructed state.
- Supporting and conflicting evidence nodes must be accepted and no later than the trigger.
- A superseding claim must exist and the supersession relation must be explicit.
- Concept exposure does not imply competence.
- A competence transition requires accepted assessment or application evidence.
- `transferred` requires a valid analogy/transfer edge and evidence node.
- Source encounters reference exact eligible segments and increment exposure count once per encounter operation.
- An entity update may change only a registered stateful property unless a new entity version is accepted.
- Questions follow legal status transitions and cannot resolve without resolution evidence.
- Numeric confidence is rejected unless a versioned method and evidence record authorize it; Design v3 schemas use categorical confidence.

### 13.3 Epistemic-use checks

Claims, concepts, source information, and entity properties used by a node must have one of:

- a valid earlier acquisition path;
- a same-node operation ordered before use in a composite payload;
- explicit `prior_assumption` provenance;
- explicit hypothesis/guess semantics with no false claim of knowledge.

These checks use structured claim and concept references. Free-text discovery can only raise a warning until a reviewed semantic reference exists.

| Code | Condition |
|---|---|
| `TL100-STATE-001` | State-before chain mismatch |
| `TL100-STATE-002` | Delta pre-state mismatch |
| `TL100-STATE-003` | Illegal operation transition |
| `TL100-STATE-004` | Computed post-state mismatch |
| `TL100-STATE-005` | Snapshot differs from reconstructed state |
| `TL100-STATE-006` | Competence transition lacks valid evidence |
| `TL100-EPI-001` | Tracked information used before availability |
| `TL100-EPI-002` | Stance recorded for unavailable claim |
| `TL100-EPI-003` | Source-derived information used before encounter |
| `TL100-EPI-004` | Exposure incorrectly treated as competence |

## 14. Source provenance gate

For each source and segment:

- bibliographic locator is non-empty and version/date is recorded where version matters;
- acquisition method and acquisition timestamp are recorded;
- creator and organization identity are not silently inferred;
- raw and normalized hashes match available payloads;
- segment locators are coherent, ordered, and non-overlapping unless overlap is declared;
- each payload locator resolves only within its permitted storage boundary;
- source text remains external to inline project-authored node fields;
- an encounter references the same source and segment identities used by compilation.

| Code | Condition |
|---|---|
| `TL100-SRC-001` | Source identity or provenance incomplete |
| `TL100-SRC-002` | Segment locator missing, invalid, or inconsistent |
| `TL100-SRC-003` | Payload locator violates storage boundary |
| `TL100-SRC-004` | Encounter/source/segment identity mismatch |
| `TL100-SRC-005` | External payload embedded as project-authored inline text |

## 15. Rights and storage gate

This gate enforces project decisions; it does not make legal judgments.

### 15.1 Training eligibility

An external source segment may emit tokens into any training export only when all are true:

- source role includes `explicit_encounter`;
- source `training_use_status` is `approved`;
- segment `training_eligibility` is `approved`;
- storage mode is `repo_fulltext` or `local_fulltext`;
- the payload is available in the authorized storage boundary;
- the source and exact segment appear in the manifest decision log;
- the encounter node and canonical stream item are accepted.

`conditional` is fail-closed in the first implementation. It becomes eligible only after a future versioned condition-decision record exists and the compiler can verify every condition.

### 15.2 Redistribution eligibility

A public corpus or payload export additionally requires:

- source `redistribution_status` is `approved`;
- segment `redistribution_eligibility` is `approved`;
- storage mode is `repo_fulltext`;
- license or permission evidence locator is present;
- attribution or notice obligations, if any, are fulfilled by a validated release artifact.

Model weights and non-public training runs are not automatically exempt. Their policy classification must be explicit before compilation.

### 15.3 Storage matrix

| Storage mode | Grounding use | Training payload | Public payload redistribution |
|---|---:|---:|---:|
| `repo_fulltext` | policy-dependent | only with approved training decision | only with approved redistribution decision |
| `local_fulltext` | policy-dependent | only with approved training decision | no |
| `metadata_only` | metadata only | no | metadata only |
| `grounding_excerpt_only` | only within approved grounding policy | no | no |
| `blocked` | no | no | no |

### 15.4 Rights failures

| Code | Condition |
|---|---|
| `TL100-RIGHTS-001` | Training status is unknown, conditional, review-required, or not approved |
| `TL100-RIGHTS-002` | Redistribution status does not permit requested public output |
| `TL100-RIGHTS-003` | Storage mode cannot supply the requested payload |
| `TL100-RIGHTS-004` | Segment eligibility conflicts with source decision |
| `TL100-RIGHTS-005` | Required license, permission, attribution, or decision evidence is absent |
| `TL100-RIGHTS-006` | Source payload included without an accepted encounter |

## 16. Duplication and source-leakage gate

### 16.1 Hard checks

- Equal normalized payload hashes are either one immutable payload referenced repeatedly or an explicitly declared duplicate.
- Every repeated exposure increments manifest exposure accounting.
- A project-authored inline payload cannot equal a registered external segment while claiming independent origin.
- Declared quotations reference exact source segments and rights decisions.
- Derived payloads identify all parents and transformation provenance.

### 16.2 Review triggers

The validator reports, without automatically claiming plagiarism:

- long exact substring overlap;
- rare n-gram overlap;
- high sequence-similarity regions;
- concentrated reuse from one source or creator;
- near-duplicate project-authored payloads;
- repeated templates and boilerplate;
- unusually high exposure concentration.

Semantic similarity and paraphrase-leakage detectors are advisory. Their model, threshold, calibration set, and false-positive analysis must be versioned.

| Code | Condition |
|---|---|
| `TL100-DUP-001` | Duplicate payload is not identity-linked or declared |
| `TL100-DUP-002` | Repeated exposure is absent from accounting |
| `TL100-DUP-003` | External payload hash is misrepresented as project-authored |
| `TL100-DUP-004` | Derived payload lacks complete parent provenance |
| `TL100-DUP-101` | Exact-overlap review trigger |
| `TL100-DUP-102` | Near-duplicate or paraphrase review trigger |

Codes numbered 100 and above in this domain are warnings unless a later deterministic fact establishes a hard violation.

## 17. Export gate

The export validator independently recompiles from the accepted release and manifest.

It checks:

- compiler, configuration, normalization policy, tokenizer, and vocabulary identities;
- selected stream items exist, are accepted, and match the declared release;
- selected and derived payload hashes resolve;
- source decisions allow every emitted source span;
- context groups and attention boundaries implement the declared policy;
- update order is deterministic from the mode, algorithm, and seed;
- within-context ordering obeys the manifest;
- each item token count equals `token_end - token_start`;
- token ranges are valid, non-overlapping in output order, and reproduce output tokens;
- unique payload and exposure counts are independently recomputed;
- material-class counts sum to emitted tokens;
- output bytes, tokens, and manifest identities match.

| Code | Condition |
|---|---|
| `TL100-EXP-001` | Compiler or tokenizer identity is incomplete or unavailable |
| `TL100-EXP-002` | Selected record is absent, ineligible, or outside the release |
| `TL100-EXP-003` | Context grouping or attention mask differs from policy |
| `TL100-EXP-004` | Update order cannot be reproduced |
| `TL100-EXP-005` | Token range or count mismatch |
| `TL100-EXP-006` | Unique/exposure/material accounting mismatch |
| `TL100-EXP-007` | Recompiled output differs from declared output |
| `TL100-EXP-008` | Export transformation mutates canonical storage |

## 18. Matched-condition gate

The primary 2x2 experiment varies:

- whether related items can share local attention context;
- whether context groups reach optimizer updates in canonical or shuffled order.

For all four cells, the auditor requires equality of:

- selected canonical stream-item multiset;
- unique normalized payload-hash multiset;
- payload exposure multiset;
- tokenizer and vocabulary;
- loss-bearing token multiset;
- total loss-bearing token exposures;
- derived-payload set, normally empty in the primary 2x2;
- exclusion policy;
- model architecture and initialization seed per matched run;
- optimizer configuration and planned update count.

Only declared factor fields may differ. Boundary tokens must either be identical across cells or excluded from loss and separately accounted. Update-order shuffling operates on complete context groups and preserves token order within each group.

For relational-versus-delinked experiments, exact token equality may be impossible because content is rewritten. Those comparisons require a separate residual-confound report covering token count, length distribution, vocabulary, topic/claim coverage, difficulty, source contribution, and semantic-equivalence review. They must not be described as same-token ordering experiments.

| Code | Condition |
|---|---|
| `TL100-MATCH-001` | Selected item multiset differs unexpectedly |
| `TL100-MATCH-002` | Unique payload or exposure multiset differs unexpectedly |
| `TL100-MATCH-003` | Tokenizer, vocabulary, or loss-bearing token multiset differs |
| `TL100-MATCH-004` | More than the declared factor fields differ |
| `TL100-MATCH-005` | Shuffle changes order inside a context group |
| `TL100-MATCH-006` | Model/training configuration differs within a matched run |
| `TL100-MATCH-007` | Rewritten control lacks residual-confound report |

## 19. Interpretive review

Deterministic validity does not establish scientific or editorial quality.

Human review at phase gates assesses:

- whether relationships are genuine rather than metadata decoration;
- whether encounters and source use are causally motivated;
- whether claims and technical content are correct for their scope;
- whether alternative explanations and uncertainty are represented honestly;
- whether recurrence produces meaningful later use rather than repeated wording;
- whether source selection introduces monoculture or hidden curricular bias;
- whether prose is readable and non-monotonous when prose exists;
- whether source wording has leaked through paraphrase despite passing exact checks;
- whether the data still represents one situated acquisition path rather than a disguised topic anthology.

Review decisions cite record IDs and evidence. “Feels good” is not an auditable acceptance rationale.

| Code | Condition |
|---|---|
| `TL100-REV-001` | Required human review is absent |
| `TL100-REV-002` | Review decision lacks reviewer identity or evidence |
| `TL100-REV-003` | Conflicting review decisions are unresolved |
| `TL100-REV-004` | Required technical or source-specialist review is absent |

## 20. Phase gates

### Gate A: structurally reviewable

Requires file/schema, identity/reference, and hash checks to pass for the candidate records.

### Gate B: canonical acceptance

Requires graph, chronology, state reconstruction, source provenance, relevant rights checks, and required human review to pass. Acceptance of a metadata-only source record does not imply payload eligibility.

### Gate C: release candidate

Requires a complete canonical stream, full state reconstruction, no unresolved hard errors, warning dispositions, immutable record hashes, and a release manifest.

### Gate D: training export

Requires export reproduction, training-use eligibility, exact token accounting, and the requested experiment audit.

### Gate E: public payload release

Adds redistribution, attribution/notice, privacy, and repository-storage requirements.

### Gate F: scale decision

Requires manual inspection of the 100k–250k-token pilot, successful small-model runs across multiple seeds, predeclared evaluation, and evidence that the pipeline—not merely the prose generator—is reliable. It does not authorize a 100M model automatically.

## 21. Test fixture requirements

The validator implementation must include:

- the valid end-to-end example chain in `examples/`;
- one minimal invalid fixture for every hard error code exercised by the implemented milestone;
- paired fixtures differing by exactly one invalid fact;
- a hard-order cycle;
- a future-knowledge use;
- a stance transition with the wrong previous value;
- a state-hash mismatch;
- a rights-blocked segment requested for training;
- a metadata-only payload requested for emission;
- an unaccounted repeated exposure;
- a same-token experimental pair with one illicit difference;
- golden validation reports whose ordering is deterministic.

Fixtures contain no third-party source text unless redistribution is explicitly approved.

## 22. Initial implementation boundary

The first validator must implement:

- offline schema resolution;
- duplicate-key detection;
- global ID and reference indexes;
- endpoint and hard-order checks;
- canonical stream checks;
- deterministic state reconstruction;
- hash-policy v1;
- source/storage/rights gates;
- exact duplicate and exposure accounting;
- export manifest and matched-condition audits;
- stable reports and error codes.

Learned similarity detectors, prose critics, dashboards, and a graph database are later additions. They cannot substitute for the initial deterministic core.
