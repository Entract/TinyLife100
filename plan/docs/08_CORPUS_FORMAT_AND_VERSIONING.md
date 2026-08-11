---
category: feature
---

# TL100 Canonical Storage, Compilation, and Versioning (Design v3)

> Status: binding Design v3 storage and compiler specification.

## 1. Purpose

TL100 separates four artifacts:

1. the canonical graph and acquisition stream;
2. immutable payloads and source metadata;
3. a released corpus inventory;
4. an exact training export with masks and update schedule.

None of these is “the text file.” A plain-text concatenation may be a convenient derivative, but it is not sufficient to reconstruct the experiment.

## 2. Source of truth

The authoritative corpus consists of:

- schema-valid canonical records;
- their envelope and payload hashes;
- an ordered canonical stream;
- a reconstructable acquisition-state chain;
- accepted source and rights decisions;
- replacement history;
- immutable release manifests.

Directory order, filename order, database row order, and Git history do not define canonical chronology.

## 3. Storage layout

The initial implementation should support this logical layout:

```text
data/
  registry/
    entities.jsonl
    claims.jsonl
    concepts.jsonl
    sources.jsonl
  payloads/
    project/
    artifacts/
    sources-public/
  canon/
    nodes.jsonl
    edges.jsonl
    state-deltas.jsonl
    state-snapshots.jsonl
    stream-items.jsonl
    replacements.jsonl
    acceptance-receipts.jsonl
    releases/
  private/
    sources-local/          # never assumed safe for Git
    decision-evidence/      # access-controlled where necessary
  derived/
    payloads/
    control-reports/
  exports/
    <release-id>/
      <export-id>/
  evals/
```

Physical paths may change, but record identities and manifest contracts may not depend on machine-specific absolute paths.

The public repository can contain metadata and hashes for non-redistributable sources. It must not contain their payloads or sensitive rights evidence.

## 4. Canonical serialization

### 4.1 Records

- Canonical registries and append logs use UTF-8 JSONL.
- Each non-empty line contains one complete JSON object.
- JSON object-key order is not semantic.
- Envelope identities use the hash policy in `07_CURATION_AND_QA.md`.
- Blank lines and comments are prohibited in canonical JSONL.
- Human-friendly YAML is permitted only for drafts or configuration and never as the sole released representation.

### 4.2 Ordering

Registry records may be indexed by ID in any physical order. Canonical stream order is the numeric `ordinal` in accepted stream items and is frozen by the release manifest.

### 4.3 Indexes

SQLite, key-value stores, adjacency indexes, and caches are rebuildable derivatives. Their hashes may be reported for performance debugging, but they are not independent canon.

## 5. Append-only canonical behavior

Before release, drafts may be revised outside `data/canon/`. Atomic acceptance appends immutable accepted records.

After release:

- an existing record ID and envelope hash remain resolvable forever;
- payload bytes do not change;
- stream ordinals in that release do not move;
- a correction creates a new record and replacement record;
- a later release selects the corrected record;
- historical releases and exports reproduce unchanged.

Compaction may rewrite physical files only if every logical record, byte identity, ordering fact, and historical locator remains verifiably equivalent.

## 6. Release manifest contract

A release manifest records at minimum:

- release ID and semantic corpus version;
- parent release IDs;
- creation and acceptance timestamps;
- schema-suite and validation-policy hashes;
- canonicalization and normalization policy versions;
- validator identity and accepted report hash;
- ordered record inventories by kind with envelope hashes;
- ordered stream-item IDs, ordinals, node IDs, and hashes;
- payload inventory with raw and normalized hashes;
- source-registry snapshot and rights-decision hashes;
- replacement and exclusion records;
- genesis and terminal state hashes;
- canonical graph summary and hard-edge inventory hash;
- unique normalized payload counts and approximate/reference-token counts;
- known limitations and unresolved warnings;
- dataset-card identity;
- manifest hash and signing information when introduced.

The manifest records payload eligibility status but does not grant new permission.

## 7. Versioning

### 7.1 Corpus versions

Use semantic-style `major.minor.patch` versions.

- **Major:** schema semantics, canonical graph semantics, acquisition-state semantics, rights-policy interpretation, or incompatible migration changes.
- **Minor:** new accepted nodes, sources, relationships, state transitions, or substantive replacements.
- **Patch:** metadata corrections that do not alter training payload bytes, canonical order, graph semantics, state reconstruction, or eligibility.

Because releases are immutable, even a patch is a new release manifest.

### 7.2 Export versions

Every change to selection, tokenizer, normalization, packing, boundaries, attention masks, position IDs, loss mask, exposure schedule, update order, padding, or output format creates a new export ID and manifest.

Two byte-identical output token files may still be different exports if their attention masks or update schedules differ.

### 7.3 Tool versions

Schemas, validators, canonicalizers, compilers, tokenizers, loaders, training code, and evaluation code are versioned independently. Git commits alone are useful but insufficient when environment or configuration affects output.

## 8. Compiler inputs

The compiler accepts only:

- one accepted release manifest;
- one export configuration conforming to a supported interface version;
- accessible payload stores authorized for the requested output class;
- one exact tokenizer package and configuration;
- one compilation policy version;
- deterministic seeds where the policy requires them.

It rejects mutable directory scans, wildcard-selected content, unversioned tokenizer aliases, and implicit default shuffling.

## 9. Compiler outputs

One export directory contains at minimum:

```text
export-manifest.json
selection.json
packing-plan.jsonl
token-spans.jsonl
tokens.bin              # or another declared token format
attention-layout.bin    # exact boundary/mask representation
position-layout.bin     # when not derivable bit-for-bit
loss-mask.bin
update-schedule.jsonl
source-decisions.jsonl
validation-report.json
```

Optional human-readable text and statistics are derivatives and carry their own hashes.

The current `export_manifest.schema.json` is the first manifest boundary. Before training implementation, it must be extended to identify the exact packing-plan, attention, position, loss-mask, batch-slot, and schedule artifacts described here.

## 10. Compilation phases

### Phase 1 — Resolve and validate release

- load the exact release manifest;
- verify schema, policy, record, payload, graph, stream, and terminal-state identities;
- refuse unresolved hard errors;
- classify requested output as private experiment, public metadata, public payload, or another approved policy class.

### Phase 2 — Select canonical items

- apply an explicit allowlist or deterministic selection rule;
- resolve every selected stream item and node;
- record excluded items and reasons;
- preserve selection as an ordered ID list and unordered multiset hash;
- reject selections that break required hard predecessors unless the export is an explicit ablation with a report.

### Phase 3 — Resolve payloads

- materialize inline, artifact, source-segment, metadata-only, and composite modes according to policy;
- preserve component boundaries;
- enforce source/storage/rights decisions before reading payload bytes into an output;
- record payload origin and material class;
- reject missing or mismatched bytes.

### Phase 4 — Normalize once

Apply the declared normalization policy once to each unique payload. Cache by raw hash, policy version, and normalized hash. Never normalize differently by experimental condition.

### Phase 5 — Tokenize once

Tokenize each unique normalized payload and each declared boundary token once with the frozen tokenizer. Store token IDs and offsets. Every primary-condition export reuses these exact tokenized units.

### Phase 6 — Construct atomic spans

An atomic span identifies:

- parent stream item and node;
- payload or component identity;
- material class and source identity where applicable;
- canonical ordinal;
- token start and length;
- boundary-token policy;
- exposure index;
- relation and state references needed for audit.

Primary-pilot nodes must fit within the maximum model context after boundary overhead. Oversized payloads are rejected during pilot curation rather than silently truncated or condition-specifically split.

### Phase 7 — Build one packing plan

Build a condition-independent ordered list of fixed-capacity packing groups. The same packing groups are used in all four primary conditions.

The initial deterministic policy:

1. visit selected spans in canonical ordinal order;
2. keep node spans intact;
3. prefer a boundary after a weak relational cut and avoid a boundary across declared immediate, source-application, correction, or local causal links;
4. never exceed maximum context capacity;
5. break ties by canonical ordinal and stable ID;
6. insert the same declared boundary tokens in every condition;
7. pad to the same capacity with non-loss tokens where fixed shapes are required.

The exact edge weights, tie rules, maximum length, boundary IDs, and padding policy are configuration, not hidden heuristics. The resulting packing plan is stored and hashed.

### Phase 8 — Apply local-context condition

Use the same physical token order, boundaries, position IDs, padding, and loss-bearing tokens in both local-context levels.

For **related context**:

- ordinary causal attention may cross node boundaries inside one packing group;
- no attention crosses packing-group boundaries.

For **isolated context**:

- causal attention resets at every node boundary;
- tokens cannot attend to tokens from an earlier node in the same packing group;
- position IDs remain identical to the related-context condition unless a separately named experiment changes them;
- loss masks remain identical.

Thus the intended difference is cross-node information availability, not token content, physical packing, positions, padding, or prediction targets.

### Phase 9 — Apply update-order condition

The update-order factor permutes complete packing groups. It never reorders tokens inside a group.

For **canonical order**, sort groups by their first canonical ordinal and stable group ID.

For **shuffled order**, derive a portable key for each group and epoch:

```text
SHA256(
  "TL100-SHUFFLE-v1" || NUL ||
  decimal_seed || NUL ||
  decimal_epoch || NUL ||
  packing_group_id
)
```

Sort ascending by the 32-byte key, breaking an impossible hash tie by packing-group ID. This avoids language-specific pseudo-random-number behavior.

Every exposure is explicit. For multiple epochs, the schedule records epoch, exposure index, batch index, and slot. No loader-level shuffle follows.

### Phase 10 — Batch schedule

- consume packing groups in declared update order;
- fill batch slots without length sorting or opportunistic repacking;
- use identical batch size, gradient accumulation, padding, and planned update count across matched conditions;
- identify incomplete final batches and apply one predeclared policy identically;
- record every group-to-batch mapping.

### Phase 11 — Emit and self-validate

- emit tokens and all layout/schedule artifacts;
- recompute counts and hashes from emitted files;
- reconstruct each manifest item from byte/token ranges;
- compare primary conditions with the matched-condition gate;
- quarantine incomplete output;
- accept the manifest only after independent reproduction passes.

## 11. Primary exact-token condition matrix

Names follow `00_PROJECT_DESIGN.md`.

| Condition | Cross-node attention inside packing group | Packing-group update order |
|---|---:|---|
| `relational_ordered` | allowed | canonical |
| `local_coherence_only` | allowed | shuffled |
| `global_chronology_only` | blocked at every node boundary | canonical |
| `fully_disrupted` | blocked at every node boundary | shuffled |

The four manifests share one release, selection, normalized payload set, tokenizer, atomic spans, packing plan, boundary tokens, position IDs, loss mask, exposure counts, and training configuration. Only attention-layout identity and update-schedule identity may vary as declared by the matrix.

## 12. What exact-token matching means

For the primary matrix, all conditions have identical:

- unique normalized payload-hash multiset;
- tokenized representation of every payload;
- boundary-token multiset and positions inside each packing group;
- packing-group content and internal order;
- padding layout;
- position IDs;
- loss-bearing token IDs and loss-mask positions;
- number of exposures per payload and group;
- total loss-bearing and padding tokens;
- planned optimizer steps and batch shape.

Shuffled conditions have a different global sequence of complete groups by design. “Same tokens” therefore means the same tokenized units and exposures, not the same global concatenation order.

Any other difference fails the matched-condition audit.

## 13. Attention and position artifacts

Do not rely on prose labels such as `isolated` to reproduce model inputs.

The export records either:

- a complete attention-layout artifact; or
- a compact boundary representation plus an algorithm/version proven to reproduce the exact mask.

Likewise, position IDs must be emitted or exactly derivable. Model-specific implementations record how causal masking, boundary masks, padding masks, rotary positions, and fused-attention kernels combine.

An implementation incapable of enforcing cross-node isolation cannot claim to run the no-local-context conditions.

## 14. Loss accounting

Report separately:

- unique payload tokens;
- boundary tokens;
- padding tokens;
- loss-bearing tokens;
- non-loss input tokens;
- repeated exposure tokens;
- tokens by material class and origin;
- tokens by source, creator, concept, and canonical phase where available.

`token_count` is not interchangeable with `loss-bearing token count`. Padding and masked targets do not disappear from compute accounting.

## 15. Source compilation

For every emitted source span, record:

- source and segment IDs;
- raw and normalized hashes;
- encounter node and stream item;
- occurrence/exposure index;
- training-use decision identity;
- redistribution decision identity when relevant;
- storage class used by the compiler;
- output token ranges.

A grounding-only source never emits source text. A metadata-only encounter may influence canonical structure but contributes no tokens. A rereading creates another explicit exposure of the same immutable segment.

Public metadata exports omit protected payload locators and bytes while preserving non-sensitive provenance and hashes according to policy.

## 16. Repetition and replay

Repetition is modeled, never accidental.

- Canonical rereading uses a distinct encounter node and stream item referencing an existing segment.
- Compiler replay uses a declared exposure schedule without pretending a new canonical encounter occurred.
- Unique payload counts deduplicate by normalized payload identity.
- Exposure counts include every training presentation.
- Replay policy is held constant in the primary 2x2.

Source concentration and payload repetition reports accompany every release and export.

## 17. Later experimental views

These are not part of the first exact-token matrix.

### Relational versus delinked

Derived payloads remove or replace persistent identity, causal bridges, callbacks, acquisition framing, belief history, or source-application links. Because text changes, this view requires parent provenance and a residual-confound report. It cannot support an exact-token ordering claim.

### Curriculum-only

Preserve prerequisite tiers but remove fine-grained acquisition chronology. The manifest records tier assignments, within-tier ordering, and all retained relations.

### Mixture controls

Vary project-authored, external-source, and artifact selection only after the first ordering/context experiment. Every mixture condition gets an exact selection and exposure manifest. No “natural/synthetic” ratio is treated as intrinsically correct.

### Replay schedules

Explicitly vary repeated exposures after a baseline with equal replay. Replay is not hidden inside sampling probability.

## 18. Export manifest requirements

In addition to the current schema boundary, the operational manifest must identify:

- release and protocol IDs;
- compiler and environment lock identities;
- tokenizer package, configuration, vocabulary, and special-token map;
- selection and exclusion artifacts;
- normalized payload inventory;
- atomic token spans;
- packing plan;
- boundary-token layout;
- attention and position layout;
- loss mask;
- update and batch schedule;
- source decision log;
- unique, exposure, padding, and loss-bearing counts;
- material/source/concept distributions;
- every deterministic seed and algorithm;
- output shards and indexes;
- validation and matched-condition reports;
- known deviations;
- manifest identity.

Manifests use relative content-addressed locators, never workstation-specific absolute paths.

## 19. Training-loader contract

The loader is part of the experiment and must be tested against the manifest.

It must:

- read groups in schedule order;
- preserve batch slot assignments;
- use emitted or reproducibly derived masks and positions;
- disable framework defaults that shuffle or repack;
- reject missing, extra, or duplicate groups;
- record resumed-run position exactly;
- maintain exposure counts across checkpoint resume;
- report the consumed schedule hash at every checkpoint.

For a dry run, hash each consumed batch descriptor and compare the resulting sequence with the manifest before model training begins.

## 20. Reproducibility levels

### Corpus reproducibility

The same release manifest resolves identical records, payload identities, graph, stream, and state.

### Export reproducibility

The same release, compiler, configuration, tokenizer, and authorized payload store produce identical output artifacts and manifests, excluding declared run timestamps.

### Loader reproducibility

The same export produces the same ordered batch descriptors and masks.

### Training reproducibility

The project records software, hardware, deterministic settings, and known nondeterminism. Bitwise-identical weights may not be feasible across hardware, so scientific claims rely on multiple seeds and predeclared statistics rather than one nominally deterministic run.

## 21. Dataset cards and prohibited interpretations

Every corpus release and experimental bundle states:

- research purpose and protocol;
- construction and review process;
- bounded domain and acquisition-path design;
- token and material distributions;
- source provenance and rights limitations;
- generator/tool contribution;
- known biases and narrowness;
- relationship and state coverage;
- validation results;
- intended and excluded uses;
- privacy and safety considerations;
- evaluation results when available.

It must explicitly state that acquisition state is experimental metadata. It is not evidence that the corpus, model, or situated learner is conscious, human, autobiographical, or psychologically realistic.

## 22. Pilot completion criteria

The storage and compiler layer is ready for scientific use when:

- one 100k–250k-token release reconstructs from genesis to terminal state;
- every selected payload and source decision verifies;
- all four primary conditions compile from one packing plan;
- matched-condition validation confirms only the two intended factor fields differ;
- the loader dry run consumes exact schedules without hidden shuffle;
- every emitted span can be traced to one canonical node and payload identity;
- a clean checkout plus authorized private inputs reproduces every permitted artifact;
- a human has inspected the complete pilot and its compiled boundaries;
- at least one very small multi-seed training run completes before any scale-up.
