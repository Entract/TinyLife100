# LIFE100 — Project Handoff (Design v2)

## What this repository is

LIFE100 is a dataset-first experiment targeting a conventional ~100M-parameter decoder-only language model.

The model is intentionally ordinary. The unusual object is the corpus.

The corpus is organized as one deliberately constructed life: chronological, internally consistent, curriculum-aware, recurrent, and epistemically tracked. The same people, places, machines, projects, mistakes, concepts, preferences, questions, discoveries, vocabulary, and memories recur over time.

### Critical v2 definition

**The Life is the organizing structure of the dataset, not a claim that every training token is synthetic first-person prose.**

The narrator can encounter human-authored books, textbook sections, manuals, papers, essays, literature, code, and technical artifacts at specific moments for specific reasons. These materials retain their own authorship and voice. The life records why they were encountered, what the narrator knew beforehand, what was understood, what was misunderstood, how the knowledge was applied, and when it recurred later.

The central research question remains:

> **What happens when essentially everything a small language model has ever seen belongs to one intentionally constructed, internally consistent stream of experience?**

But “seen” now includes both lived/generated experience and deliberately situated external knowledge.

## Read in this order

1. `docs/00_PROJECT_DESIGN.md`
2. `docs/15_LIBRARY_AND_READING_EVENTS.md`
3. `docs/16_CORPUS_MIXTURE_AND_COMPILATION.md`
4. `docs/11_WORLD_V0_AND_NARRATOR.md`
5. `docs/02_CURRICULUM_ARCHITECTURE.md`
6. `docs/03_CHRONOLOGY_AND_LIFE_ARCS.md`
7. `docs/04_VOICE_AND_PERSPECTIVE.md`
8. `docs/13_FIRST_30_PROJECT_ARCS.md`
9. `docs/14_FIRST_100_EPISODES.md`
10. `docs/01_WORLD_AND_CONTINUITY.md`
11. `docs/05_EPISODE_SPECIFICATION.md`
12. `docs/06_GENERATION_PIPELINE.md`
13. `docs/07_CURATION_AND_QA.md`
14. `docs/08_CORPUS_FORMAT_AND_VERSIONING.md`
15. `docs/09_EVALUATION_AND_EXPERIMENTS.md`
16. `docs/12_CORPUS_TOKEN_BUDGET.md`
17. `docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md`
18. `docs/10_BUILD_PHASES.md`
19. `AGENTS.md`

## Most important implementation instruction

**Do not start bulk generation or bulk book ingestion.**

First build the machine-readable substrate:

- world/entity ledgers;
- concept dependency graph;
- narrator knowledge/belief state;
- source registry with provenance and rights status;
- reading-event records;
- canonical stream-item store;
- state transition validation;
- deterministic linter;
- corpus compiler;
- export manifests.

The first corpus goal remains only 50k–250k tokens, and the entire pilot should be read in chronological order by a human before scaling.

## What changed from design v1

Design v1 treated external source material primarily as factual substrate used backstage to generate one-voice Life prose.

Design v2 keeps that mode but adds a second, crucial mode:

> **Some external works may themselves enter the training stream as explicit reading experiences.**

Therefore:

- narrator-authored Life prose remains first-person and voice-controlled;
- external readings retain their native voice;
- the canonical life timeline contains typed stream items, not only episodes;
- reading events have before/after knowledge state and later callbacks;
- source mixture becomes an experimental variable;
- the same compiled token set can be compared in contextualized-life order versus shuffled/decontextualized forms.

## Design choices that are proposals, not locked canon

Current v0 proposes:

- narrator working name: Alex;
- start at age 15 with fluent ordinary English but little formal technical competence;
- fictional contemporary town: Rookfield;
- recurring makerspace: The Foundry;
- initial cast: Mara, Ben, Dr. Imani, Tomas, Leila, Priya, Hana;
- development from making/measurement through electronics, software, systems, ML, LLMs, and deployment;
- mature compiled-corpus target: ~250M unique accepted tokens.

No final Life-vs-reading mixture is locked.

## First code milestone

Create:

1. entity ledger schemas;
2. concept graph schema;
3. episode-plan schema;
4. `source.schema.json` support;
5. `reading_event.schema.json` support;
6. `stream_item.schema.json` support;
7. state transition engine;
8. deterministic corpus/source linter;
9. canonical chronological store;
10. corpus compiler supporting multiple material classes;
11. export generator for chronological, local-shuffle, global-shuffle, and decontextualized views.

Only then implement model-backed planner/writer/critic stages.

## Core scientific controls

Never store only a shuffled corpus. The canonical life remains ordered forever.

At minimum preserve the ability to compare:

- **LIFE-ORDERED:** life-native material and readings encountered in designed chronology;
- **LIFE-LOCAL-SHUFFLE:** broad developmental phase retained, local order randomized;
- **GLOBAL-SHUFFLE:** exactly the same selected material globally randomized;
- **DECONTEXTUALIZED:** same Life prose and readings but contextual bridges/reading rationale removed where possible;
- **MIXTURE A/B/C:** matched total-token runs with different material-class proportions.

These controls let us test whether chronology, contextual placement, recurrence, voice concentration, and human-written input each contribute independently.
