# AGENTS.md — TinyLife100 implementation handoff (Design v3)

You are working on TinyLife100 (TL100), a dataset-first scientific investigation of relational pretraining for small language models.

Read the Design v3 foundation before changing project behavior.

## Priority order

1. Preserve experimental validity and matched controls.
2. Preserve canonical graph and stream integrity.
3. Preserve acquisition and belief-state correctness.
4. Preserve source provenance, rights, and licensing metadata.
5. Preserve exact token, context-boundary, update-order, and exposure accounting.
6. Prefer deterministic validation over model judgment.
7. Preserve reproducibility, hashes, and immutable release manifests.
8. Automate repeatable validation.
9. Optimize throughput only after the above are reliable.

## Critical conceptual rule

**The situated learner is an acquisition reference point, not a simulated human.**

“Experience” means that an item has a traceable trigger, acquisition mode, pre-state, proposed state change, and later relational uses.

Do not introduce biography, psychology, fictional world detail, or first-person narration unless an approved Design v3 experiment requires it.

## Canonical scientific object

The source of truth is:

- a directed graph of typed corpus nodes and relationships;
- one reviewed canonical stream order;
- immutable accepted payloads;
- exact training-export manifests.

Training views may reorder, mask, or omit relationships. They never overwrite canon.

## Do not do these things

- Do not implement Design v2 fictional-life assumptions as current requirements.
- Do not bulk-generate prose before D3 schemas, validators, compiler behavior, and experimental controls are stable.
- Do not bulk-ingest books or webpages.
- Do not invent a fixed natural/synthetic mixture.
- Do not silently rewrite canonical records.
- Do not let generation invent persistent entities, sources, claims, or graph edges without registration.
- Do not make information available before its acquisition path permits it.
- Do not conflate local attention context with global optimizer update order.
- Do not claim an order effect when exposure, replay, padding, masking, or content differs.
- Do not treat recurring-world recall as transfer.
- Do not place copyrighted or non-redistributable source text in the public repository without explicit permission.
- Do not make legal assumptions about trainability or redistribution.
- Do not use random splits as the only evaluation strategy.
- Do not strip provenance or hashes from canon.
- Do not treat synthetic generation as factual authority.
- Do not train a 100M-parameter model before small matched runs justify it.

## Read first

1. plan/docs/00_PROJECT_DESIGN.md
2. plan/docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md
3. the plan document attached to the active task

Design v3 migration documents, when completed:

- plan/docs/01_WORLD_AND_CONTINUITY.md
- plan/docs/05_EPISODE_SPECIFICATION.md
- plan/docs/07_CURATION_AND_QA.md
- plan/docs/08_CORPUS_FORMAT_AND_VERSIONING.md
- plan/docs/06_GENERATION_PIPELINE.md

Other plan documents remain Design v2 legacy inputs until explicitly migrated. They may be consulted for useful mechanisms, but they are not binding.

## First implementation milestones

1. Validate and version the D3 schema suite.
2. Implement canonical node and typed-edge storage.
3. Implement acquisition-state and belief-state validation.
4. Implement source registry and rights-status hard gates.
5. Implement immutable canonical stream storage.
6. Implement exact export manifests.
7. Implement local-context and global-update-order experimental views.
8. Implement deterministic graph, chronology, hash, duplication, and leakage checks.
9. Build a 100k–250k-token manually inspectable pipeline pilot.
10. Implement a minimal training and evaluation harness.
11. Run small, multi-seed, matched experiments before scaling.

## Canonicality

data/canon/ is append-oriented. Content in a released version is immutable.

Corrections create explicit replacement or migration records in a new version.

External source files are not canonical corpus content merely because they exist. Canonical inclusion requires an accepted source record, eligible rights state, referenced payload hash, accepted graph placement, and export-manifest inclusion.

## Human review

Human review is required at phase gates and should focus on:

- graph-edge validity;
- acquisition paths;
- belief updates and corrections;
- contiguous stream coherence;
- matched-control integrity;
- source appropriateness and rights;
- transfer versus memorization;
- generator artifacts and monotony;
- technical accuracy;
- whether evaluations are graph-separated from training;
- whether a positive result survives external-language controls.

## Scientific interpretation

Preserve null and negative results.

If only local context helps, narrow the project toward context construction.

If curriculum-only matches the full relational stream, attribute the result to curriculum.

If gains reduce to recurring-name recall, do not claim transfer.

If external performance collapses, report the specialization cost.
