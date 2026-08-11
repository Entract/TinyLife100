# 08 — Corpus Format, Canonical Stream, and Versioning (v2)

## 1. Source of truth

The canonical corpus is **structured records plus an ordered stream manifest**, not a giant text file.

Recommended storage:

- JSONL for immutable records;
- YAML/JSON/SQLite for ledgers;
- content-addressed source segments or references;
- manifests with hashes;
- generated plain-text/tokenized training views.

The public Git repository may contain metadata for sources whose full text cannot be redistributed.

---

## 2. Directory convention

```text
data/
  sources/
    registry/
    fulltext/          # only where policy permits
    segments/
  readings/
  artifacts/
  drafts/
  canon/
    episodes/
    reading_events/
    stream/
    ledgers/
    manifests/
  exports/
    life_ordered/
    life_local_shuffle/
    global_shuffle/
    decontextualized/
    mixture_controls/
    replay/
  evals/
```

Do not commit large full-text/source/tokenized shards without a deliberate storage strategy.

---

## 3. Canonical record types

### Episode
Narrator-authored Life prose. See `episode.schema.json`.

### Source
External source metadata, rights status, stable segment identities. See `source.schema.json`.

### Reading event
Why/when/how source material is encountered. See `reading_event.schema.json`.

### Stream item
Exact canonical ordering envelope. See `stream_item.schema.json`.

### Artifact
Optional structured record for code/logs/config/tables/specifications when format matters.

---

## 4. Canonical stream

Canonical order is defined by stream-item ordinal, not episode ID alone.

Example:

```text
00000041  episode        ep_00000041
00000042  reading_start  read_00000003
00000043  source_segment source_motor_01/seg_ratings
00000044  reading_end    read_00000003
00000045  episode        ep_00000042
```

Reading start/end can be metadata-only. The training compiler decides whether any boundary tokens appear.

A canonical stream item never changes position inside a released version.

---

## 5. Source storage modes

A source record must specify storage mode:

- `repo_fulltext`
- `local_fulltext`
- `metadata_only`
- `grounding_excerpt_only`
- `blocked`

The corpus compiler must refuse any explicit-reading segment whose `training_use_status` is not approved for the intended export.

The repository should never assume that “available online” means “redistributable.”

---

## 6. Release manifest

A release manifest should include:

- corpus version;
- schema versions;
- ledger versions/hashes;
- ordered stream-item IDs/hashes;
- episode IDs/hashes;
- source records and segment hashes;
- reading-event IDs;
- total unique text tokens under reference tokenizer;
- tokens by material class/origin/era;
- source registry version;
- generation pipeline version;
- voice reference version;
- rights-policy version;
- known exclusions/limitations.

---

## 7. Training exports

Each export gets an exact manifest.

Example:

```yaml
export_id: exp_v2_life_ordered_001
corpus_version: v2.0.0
tokenizer_version: tok_003
ordering: life_ordered
material_policy:
  include:
    - LIFE_NATIVE
    - HUMAN_READING
    - TECHNICAL_ARTIFACT
mixture_realized:
  LIFE_NATIVE: 0.51
  HUMAN_READING: 0.35
  TECHNICAL_ARTIFACT: 0.14
separator_policy: natural_boundaries_v2
replay: none
seed: 12345
unique_text_tokens: ...
training_exposure_tokens: ...
sha256: ...
```

For shuffled views store exact permutation/seed.

For decontextualized views store exactly which bridge items were removed/replaced.

For mixture controls store selection algorithm and source/episode subsets.

---

## 8. Unique data versus exposures

Track separately:

- unique Life-native tokens;
- unique source tokens;
- unique artifact tokens;
- compiled unique text tokens;
- repeated source references/rereadings;
- total training exposures.

If one source chapter is encountered twice, it remains one unique source segment but contributes two exposures when compiled twice.

---

## 9. Token counting

Use one stabilized reference tokenizer for corpus milestones.

Before stabilization report words/characters and clearly labeled approximate tokens.

Report source-unit token counts and Life-native token counts separately.

---

## 10. Versioning

Use semantic-style versions:

- **major** — world/curriculum/source-policy/prose-contract break or material replacement;
- **minor** — substantial new accepted content;
- **patch** — metadata/annotation corrections that do not change compiled text.

If training text or ordering changes, create a new export manifest even if canonical content does not.

---

## 11. Provenance

Generated episodes record:

- planner/writer/critic model versions;
- prompt/config hashes;
- grounding sources;
- explicit-reading links;
- revision count;
- human review state;
- content hash.

External source segments record:

- creator/title/version;
- retrieval/acquisition metadata;
- license/rights fields;
- segment locator;
- source hash and segment hash;
- whether full text is stored or referenced;
- allowed roles.

---

## 12. Dataset cards

Every release should state:

- purpose;
- construction method;
- model target;
- total token count;
- material mixture;
- source-origin distribution;
- world/voice description;
- source policy;
- generation systems;
- rights/redistribution limitations;
- known narrowness and biases;
- evaluation results;
- prohibited interpretations.

Explicitly state that the first-person Life is synthetic and is not a real person's biography.
