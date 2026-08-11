# 06 — Generation and Corpus-Construction Pipeline (v2)

## 1. Principle

Frontier models are a **controlled authoring and review team**, not a one-shot dataset generator.

Likewise, external books and documents are **curated inputs**, not a folder dumped into pretraining.

The pipeline must separate:

- world/curriculum planning;
- source discovery/selection;
- encounter planning;
- factual grounding;
- Life prose generation;
- source-text inclusion;
- criticism and revision;
- state mutation;
- canonical placement;
- corpus compilation.

---

## 2. Pipeline overview

```text
WORLD STATE + CURRICULUM + ARC PLAN
                |
                v
        ENCOUNTER SCHEDULER
                |
       +--------+---------+
       |                  |
       v                  v
LIFE EVENT?          KNOWLEDGE GAP /
                   READING OPPORTUNITY?
       |                  |
       |                  v
       |            SOURCE SELECTOR
       |                  |
       |          provenance/rights checks
       |                  |
       |                  v
       |           READING EVENT PLAN
       |                  |
       +--------+---------+
                v
          EPISODE PLANNER
                |
                v
        STRUCTURED PLAN(S)
                |
       deterministic checks
                |
                v
       LIFE PROSE WRITER
                |
                v
             DRAFT
       /        |        \
      v         v         v
 TECHNICAL  CONTINUITY   VOICE/
  CRITIC     CRITIC      COPYING
       \        |        /
        +-------+-------+
                v
        REVISION / EDITOR
                |
                v
        DETERMINISTIC LINTER
                |
                v
          ACCEPT / REJECT
                |
                v
      STATE MUTATION REVIEW
                |
                v
        CANONICAL STREAM
                |
                v
          CORPUS COMPILER
                |
                v
      VERSIONED TRAIN EXPORTS
```

External source text used as explicit reading does **not** pass through the Life prose writer. It passes through source validation, segmentation, placement, and compilation.

---

## 3. Stage 0 — Source/library planning

Before bulk prose generation, build a source registry.

For each candidate source:

- identify creator/title/version;
- classify source type;
- record domain/concepts;
- record difficulty/prerequisites;
- record provenance;
- record rights/licensing/training-use/redistribution status;
- assign allowed role: grounding-only, explicit-reading eligible, or blocked;
- define coherent segments with stable hashes;
- estimate token size under reference tokenizer when available.

Do not ingest full text into the public repo unless policy permits it.

---

## 4. Stage 1 — Curriculum scheduler

Consumes:

- current narrator knowledge state;
- concept dependency graph;
- project arcs;
- recurrence targets;
- unresolved questions;
- reading map;
- material-class budgets;
- previous exposure counts.

Outputs the next **learning/experience objectives**, not prose.

The scheduler can decide that the next useful event is:

- an experience;
- a conversation;
- an experiment;
- a reading;
- a rereading;
- a source conflict;
- an application;
- an ordinary-life connective episode.

---

## 5. Stage 2 — Encounter planner

The encounter planner determines *how information enters the Life*.

Example:

```yaml
objective: understand why the motor driver resets
available_modes:
  - measurement
  - Mara conversation
  - motor datasheet
  - driver datasheet
selected_sequence:
  - wrong firmware hypothesis
  - load measurement
  - datasheet reading
  - revised explanation
```

This stage prevents every concept from becoming “Alex sits down and explains X.”

---

## 6. Stage 3 — Source selector

When a reading/artifact is useful, select the actual source before writing surrounding prose.

Selection must consider:

- correctness/authority;
- prerequisite fit;
- conceptual contribution;
- duplication with prior sources;
- linguistic/style contribution;
- Life plausibility;
- rights/training-use eligibility;
- coherent segment boundaries.

The selector should be able to reject a famous source if it is a poor fit for Alex at that moment.

---

## 7. Stage 4 — Episode planner

Creates structured plans for Life-native material surrounding the encounter.

It receives:

- state before;
- source/reading event if any;
- project and people;
- concept targets;
- acquisition modes;
- narrator belief before;
- planned evidence;
- expected state mutations;
- memory callbacks;
- anti-repetition constraints.

The writer should never invent the source rationale, chronology, or knowledge transition while writing.

---

## 8. Stage 5 — Factual substrate

For generated technical prose, construct a factual substrate from approved sources.

The substrate should contain only what the writer needs:

- definitions;
- equations;
- constraints;
- numerical values where relevant;
- caveats;
- source IDs;
- known ambiguities.

This is separate from an explicit reading. A source can ground an episode without its prose entering training.

---

## 9. Stage 6 — Writer

The Life writer produces only narrator-authored text.

Inputs:

- approved episode plan;
- state before;
- factual substrate;
- voice reference set;
- continuity summaries;
- specific source facts/encounter metadata where relevant;
- negative constraints.

The writer must not:

- invent major canon;
- quote source material beyond allowed/intentional inclusion;
- make Alex omniscient;
- turn every episode into a textbook;
- reveal knowledge not yet acquired;
- imitate the voice of a recent explicit reading too strongly.

---

## 10. Stage 7 — Critics

Use independent roles where practical.

### Technical critic

Checks facts, equations, units, engineering plausibility, and whether conclusions exceed evidence.

### Continuity critic

Checks world state, chronology, entity history, source-read history, narrator knowledge, and impossible callbacks.

### Curriculum critic

Checks prerequisites, learning progression, acquisition-mode variety, recurrence, and source timing.

### Voice critic

Checks Alex's Life-native voice only. It should **not** reject external source text for sounding unlike Alex.

### Source integrity critic

Checks:

- correct source/segment identity;
- no accidental paraphrase copying into Life prose;
- no source truncation that changes meaning;
- no metadata/source mismatch;
- reading context consistent with actual source contents.

### Diversity/monotony critic

Checks scene structure, explanatory templates, dialogue patterns, recurring phrases, and generator-model artifacts.

### Life critic

Asks the holistic question:

> Does this feel like something that happened in a coherent life, or like curriculum content wearing a costume?

---

## 11. Stage 8 — Revision/editor

Revision resolves critic findings without changing unrelated canon.

Important rule:

> **Do not “fix” an external source by rewriting it.**

If the selected source is flawed, too difficult, misleading, or inappropriate, change the source selection or model Alex's disagreement/limitations explicitly.

---

## 12. Stage 9 — Deterministic linting

Automated checks should include:

- schema validity;
- entity existence;
- unique IDs;
- source/segment existence;
- source hash match;
- rights/training-use status;
- chronology monotonicity;
- narrator-read-before-use constraints where modeled;
- concept prerequisite violations;
- content hashes;
- exact/near duplication;
- suspicious source overlap in generated prose;
- token counts;
- material-class accounting;
- export manifest consistency.

Model critics never replace deterministic checks when a deterministic check is possible.

---

## 13. Stage 10 — Canonicalization

Accepted Life episodes, reading events, source references, artifacts, and state mutations become immutable canonical records for that corpus version.

Canonicalization should be append-oriented and produce:

- content hash;
- provenance record;
- state-before/state-after hashes;
- stream ordinal;
- source references;
- material class;
- generation/review metadata.

---

## 14. Stage 11 — Corpus compilation

The compiler transforms canonical records into exact training views.

It must support at least:

- `life_ordered`;
- `life_local_shuffle`;
- `global_shuffle`;
- `decontextualized`;
- `life_only`;
- mixture sweeps;
- curriculum/replay schedules.

Every export has an exact manifest with token counts, source segments, permutations/seeds, exposure counts, and hashes.

See `16_CORPUS_MIXTURE_AND_COMPILATION.md`.

---

## 15. Human phase-gate review

At 50k, 250k, 1M, 5M, 25M, 100M tokens:

- read contiguous chronology;
- inspect every explicit reading in the pilot;
- inspect a complete source-to-application chain;
- inspect one project arc;
- inspect one concept from first exposure to transfer;
- inspect one recurring person/machine;
- sample generated prose for source-copy leakage;
- inspect material mixture statistics;
- train diagnostic models when appropriate.

Isolated random passages are not enough. A dataset can be locally excellent and globally lifeless.

---

## 16. Model diversity

Useful backstage roles may include:

- strong reasoning model: curriculum/encounter planner;
- strong technical model: source mapper/technical critic;
- strong prose model: Life writer;
- independent model family: adversarial critic;
- fixed canonical editor: voice harmonization of Life-native prose only.

Surface authorship of external human works must remain attributable to those works rather than being erased by the editor.

---

## 17. Cost accounting

Track per accepted Life-native token and per compiled token:

- planning tokens;
- source-processing tokens;
- writer tokens;
- critic/revision tokens;
- human review minutes;
- source acquisition/processing cost;
- rejection rate;
- API/compute cost;
- storage cost.

A reading-heavy corpus may reduce generated-token cost but increase source curation and rights overhead. The project should measure rather than assume.
