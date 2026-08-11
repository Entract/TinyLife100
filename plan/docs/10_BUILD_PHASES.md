# 10 — Build Phases (v2)

## Phase 0 — Design lock

Do not generate bulk text.

Complete/review:

- world v0;
- narrator voice reference;
- concept graph;
- acquisition-mode taxonomy;
- first project arcs;
- first reading/source map;
- source/rights policy;
- schemas for episodes, sources, reading events, stream items;
- corpus compiler design;
- eval design;
- mixture experiment plan.

Exit criterion: implementation agents can build the system without inventing foundational corpus policy.

---

## Phase 1 — 50k-token pilot

Goal: prove the full Life + reading workflow on an inspectable corpus.

Build:

- 40k–50k Life-native tokens;
- a small rights-clear source library;
- several explicit reading encounters;
- at least one source-to-project-to-later-callback chain;
- canonical stream manifest;
- life-ordered and shuffled exports.

Exact mixture is not important yet; inspectability is.

Human review: **read everything**.

Questions:

- Does Alex feel coherent?
- Do readings feel causally motivated?
- Do external voices enrich rather than rupture the Life?
- Is source provenance exact?
- Does the compiler reproduce exports deterministically?

---

## Phase 2 — 250k-token pilot extension

Goal: stress recurrence and source integration.

Requirements:

- multiple project arcs;
- recurring people/machines;
- 10–30 source records;
- several reading types: datasheet/manual/textbook/ordinary reading;
- at least one rereading;
- at least one source misunderstanding;
- at least one source-vs-experiment reconciliation;
- first mixture-control exports.

Train very small models as pipeline diagnostics.

---

## Phase 3 — 1M-token Corpus v0

Goal: establish whether the corpus is trainable and whether obvious pathologies appear.

Implement:

- source concentration dashboard;
- duplication/source-copy checks;
- concept-acquisition trace reports;
- material-class accounting;
- Life-ordered vs global-shuffle baseline;
- pure-Life vs mixed baseline if affordable.

Train ~1M–10M parameter diagnostics.

Stop if the corpus feels formulaic or source placement is artificial.

---

## Phase 4 — 5M-token Corpus v1

Goal: first meaningful data-design experiments.

Run a subset of:

- pure Life;
- Life-heavy mix;
- balanced mix;
- ordered vs shuffled;
- contextualized vs decontextualized.

Use ~10M–30M models.

Do not scale further unless results or failure analysis justify it.

---

## Phase 5 — 25M-token Corpus v2

Goal: establish whether structure survives at useful scale.

By this point:

- QA must be mostly automated;
- humans inspect contiguous samples and full arcs;
- source registry/rights workflow must be reliable;
- source library should contain meaningful variety;
- material-class and era distributions should be intentionally designed;
- eval suite should include source holdouts and transfer.

This is the first stage where mixture conclusions may become credible enough to guide the 100M-token corpus.

---

## Phase 6 — 100M-token Corpus v3

Goal: train serious ~30M–100M parameter experiments.

Before generation/acquisition begins, lock:

- v3 target mixture(s);
- source pool;
- source concentration limits;
- curriculum/era budgets;
- replay policy;
- exact experimental controls.

Do not author 100M Life tokens simply because 100M is the milestone. The compiled target can include substantial human readings/artifacts.

---

## Phase 7 — 250M-token Corpus v4

Goal: primary 100M-target dataset.

The v4 mixture is chosen from earlier evidence, not from intuition alone.

Requirements:

- stable generation/curation pipeline;
- mature source library;
- explicit rights policy;
- reproducible compilation;
- validated small-model curves;
- strong held-out evals;
- no severe source/Life monoculture;
- known compute budget.

---

## Phase 8 — Final training program

Train the main ~100M model and matched controls.

Priority controls:

1. LIFE-ORDERED;
2. GLOBAL-SHUFFLE;
3. best alternative mixture;
4. decontextualized or Life-only control depending on earlier results.

Save checkpoints frequently enough to inspect developmental differences.

---

## Immediate implementation tasks

1. Implement source registry and `source.schema.json`.
2. Implement reading events and `reading_event.schema.json`.
3. Implement canonical `stream_item` ordering.
4. Implement concept acquisition-mode fields.
5. Implement rights/training-use hard gate in compiler.
6. Implement exact source segment hashing.
7. Implement Life/source mixture accounting.
8. Build the first 10–30 source candidate registry entries **without** bulk text inclusion.
9. Revise first 100 episodes with deliberately placed reading encounters.
10. Generate only enough prose to test the full pipeline.
