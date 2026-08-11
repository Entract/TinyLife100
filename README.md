# LIFE100 — A Coherent Life-Structured Corpus for a ~100M-Parameter Language Model

LIFE100 is a dataset-first language-model research project.

The central question is:

> **What happens when essentially everything a small language model has ever seen belongs to one intentionally constructed, internally consistent stream of experience?**

The important refinement is that **the Life is the organizing structure of the dataset, not a requirement that every token be synthetic first-person prose**.

The canonical life has one persistent narrator, one world, one chronology, one accumulating knowledge state, recurring people/places/machines/projects/mistakes/memories, and a prerequisite-aware curriculum. But the narrator also encounters external human knowledge at meaningful times: books, textbook chapters, manuals, papers, essays, literature, code, technical artifacts, and documents.

Those external works retain their own authorship and voice. They become experiences *inside* the life: encountered for a reason, at a time, against a prior knowledge state, followed by reflection, application, misunderstanding, correction, or later recall.

The model architecture is intentionally conventional. The primary research artifact is the **data and its structure**.

## Core principles

1. **One persistent first-person narrator, but not one universal authorial voice.**
2. **One canonical world with explicit continuity.**
3. **One immutable chronological life stream.**
4. **Knowledge enters through identifiable acquisition events: experience, people, reading, artifacts, experimentation, and inference.**
5. **Human-authored sources can appear as first-class experiences rather than random corpus filler.**
6. **Concepts are introduced in prerequisite-aware order and recur across different contexts.**
7. **Mistakes, uncertainty, revision, delayed understanding, and conflicting evidence are part of the life.**
8. **The same people, places, machines, projects, questions, discoveries, vocabulary, and memories recur over time.**
9. **Every external source has provenance and rights/licensing metadata before it can enter a compiled corpus.**
10. **Canonical order is preserved forever; training order and mixture are experimental variables.**
11. **Frontier models are authoring/critic tools, never authorities.**
12. **No fixed natural/synthetic percentage is assumed in advance. Mixture composition is measured experimentally.**
13. **No attempt is made to imitate frontier-model breadth. Density, coherence, transfer, and learnability per parameter are the objective.**

## Repository map

- `docs/00_PROJECT_DESIGN.md` — overall research design and revised definition of “Life”
- `docs/01_WORLD_AND_CONTINUITY.md` — persistent entities, knowledge state, source/read-state continuity
- `docs/02_CURRICULUM_ARCHITECTURE.md` — concept graph and acquisition modes
- `docs/03_CHRONOLOGY_AND_LIFE_ARCS.md` — chronology, arcs, reading encounters, recurrence
- `docs/04_VOICE_AND_PERSPECTIVE.md` — narrator voice and boundaries around external authorship
- `docs/05_EPISODE_SPECIFICATION.md` — episode records and their relation to timeline items
- `docs/06_GENERATION_PIPELINE.md` — planning/writing/criticism plus source-selection workflow
- `docs/07_CURATION_AND_QA.md` — technical, continuity, source, mixture, and stylistic QA
- `docs/08_CORPUS_FORMAT_AND_VERSIONING.md` — canonical stream, source store, compilation, manifests
- `docs/09_EVALUATION_AND_EXPERIMENTS.md` — chronology, mixture, contextualization, and ablation experiments
- `docs/10_BUILD_PHASES.md` — staged path from pilot to 250M-token target
- `docs/11_WORLD_V0_AND_NARRATOR.md` — concrete narrator, town, cast, places, recurring objects
- `docs/12_CORPUS_TOKEN_BUDGET.md` — total-token target plus material-class mixture strategy
- `docs/13_FIRST_30_PROJECT_ARCS.md` — concrete project backbone
- `docs/14_FIRST_100_EPISODES.md` — pilot chronology plus deliberately placed reading encounters
- `docs/15_LIBRARY_AND_READING_EVENTS.md` — source selection, reading-event lifecycle, provenance and rights
- `docs/16_CORPUS_MIXTURE_AND_COMPILATION.md` — content classes, mixture experiments, compilation views
- `docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md` — prior-work rationale, caveats, and falsifiable questions
- `schemas/episode.schema.json` — narrator-authored episode record
- `schemas/source.schema.json` — external source registry record
- `schemas/reading_event.schema.json` — encounter with an external source
- `schemas/stream_item.schema.json` — canonical timeline item envelope
- `examples/` — example plans and records
- `AGENTS.md` — implementation handoff rules

## Recommended target

The target model is a conventional ~100M-parameter decoder-only transformer.

The provisional mature-corpus target remains **~250M unique accepted training tokens**, but that total now means the compiled corpus, not 250M tokens of synthetic autobiography.

Scale only through validated releases:

- **Pilot:** 50k–250k compiled tokens
- **v0:** 1M
- **v1:** 5M
- **v2:** 25M
- **v3:** 100M
- **v4 target:** 250M
- **v5+:** only if experiments justify expansion

At every stage, report both:
- material composition (Life-native / human reading / artifact / other), and
- training exposure count separately from unique corpus size.

## Status

**Design v2.**

The project is ready for implementation of ledgers, source registry, reading-event records, chronology store, validation, and corpus compilation. It is **not** ready for bulk prose generation or bulk source ingestion.
