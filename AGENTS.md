# AGENTS.md — LIFE100 implementation handoff (Design v2)

You are working on LIFE100, a dataset-first research project. Read the design documents before writing generation code.

## Priority order

1. Preserve canonical chronology and corpus integrity.
2. Preserve world continuity and narrator epistemic state.
3. Preserve source provenance and rights/licensing metadata.
4. Preserve curriculum dependencies and acquisition history.
5. Preserve narrator voice for narrator-authored material.
6. Preserve external source voice when a source is intentionally included as a reading.
7. Preserve technical correctness.
8. Automate repeatable validation.
9. Optimize throughput only after the above are reliable.

## Critical conceptual rule

**The Life is the organizing structure of the data. It is not a requirement that all training text be rewritten into the narrator's voice.**

A human-authored source may appear in the compiled training stream only through an explicit source record and reading/encounter plan. Do not silently blend external prose into generated Life prose.

## Do not do these things

- Do not bulk-generate Life prose before the world bible, curriculum graph, episode schema, source schema, reading-event schema, and stream-item schema are stable.
- Do not bulk-ingest books or webpages merely because they look educational.
- Do not invent a fixed natural/synthetic mixture percentage.
- Do not silently rewrite canonical records.
- Do not let a generation model invent canonical people, places, machines, sources, or major facts without registration.
- Do not let the narrator know source content before the relevant encounter.
- Do not rewrite external reading text into Alex's voice when the design says the original source itself is the experience.
- Do not place copyrighted/non-redistributable source text in the public repository unless explicit rights allow it.
- Do not make legal assumptions about trainability or redistribution; record rights status and require project approval.
- Do not use random train/test splitting as the only evaluation strategy.
- Do not strip provenance from canon.
- Do not make the narrator omniscient.
- Do not optimize for broad trivia coverage.
- Do not treat synthetic generation as permission to fabricate technical facts.
- Do not train the final 100M model until small-model experiments validate the data pipeline.

## First implementation milestones

1. Validate all schemas in `schemas/`.
2. Define machine-readable ledgers for people, places, machines, projects, concepts, memories, vocabulary, preferences, unresolved questions, mistakes, and discoveries.
3. Implement source registry and rights-status checks.
4. Implement reading-event planning and before/after knowledge-state links.
5. Implement canonical stream items that can reference Life episodes, source segments, conversations/artifacts, and reflections.
6. Implement deterministic corpus/source linting.
7. Implement separate episode plans and prose records.
8. Implement generation stage interfaces:
   scheduler -> encounter planner -> source selector -> episode planner -> writer -> critics -> editor -> acceptance.
9. Implement corpus compiler and exact manifests.
10. Build a 50k–250k-token pilot with full manual inspection.
11. Export LIFE-ORDERED, GLOBAL-SHUFFLE, and at least one mixture-control view.
12. Train a very small baseline model before scaling data production.

## Canonicality

`data/canon/` is append-oriented. Once a release is tagged, content from that release is immutable. Corrections create a new corpus version with explicit replacement/migration records.

External source files are *not* automatically canonical corpus content. Canonicality comes from a source record plus an accepted stream inclusion/reading event plus an export manifest.

## Human review

The corpus can be largely model-assisted, but human review is required at phase gates. Human review should focus on:

- contiguous chronology;
- source appropriateness;
- whether reading events feel causally motivated;
- concept arcs;
- recurring entities;
- prose monotony;
- source/Life mixture effects;
- suspicious copying or paraphrase leakage;
- technical accuracy;
- whether the Life still feels like a life rather than a curriculum disguised as fiction.

## Read first

- `docs/00_PROJECT_DESIGN.md`
- `docs/15_LIBRARY_AND_READING_EVENTS.md`
- `docs/16_CORPUS_MIXTURE_AND_COMPILATION.md`
- `docs/01_WORLD_AND_CONTINUITY.md`
- `docs/02_CURRICULUM_ARCHITECTURE.md`
- `docs/05_EPISODE_SPECIFICATION.md`
- `docs/06_GENERATION_PIPELINE.md`
