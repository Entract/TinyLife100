# TinyLife100 (TL100)

**Life-Structured Relational Pretraining for Small Language Models**

TinyLife100 is a dataset-first research project studying whether a small, conventional language model learns differently when its training data preserves explicit relationships among information encounters.

The central question is:

> Holding content, token exposure, architecture, tokenizer, and optimization as constant as possible, does preserving causal, temporal, referential, epistemic, and prerequisite structure change what a small language model learns?

## What “life” means

TL100 does not simulate a human biography.

It organizes data around one **situated learner**: an epistemic reference point whose information has a traceable acquisition path. Canon records what became available, how it became available, what prior information existed, what was believed or misunderstood, and which later items apply or correct it.

The canonical scientific object is:

- a graph of corpus items and typed relationships;
- one reviewed canonical stream order;
- exact training exports that preserve or disrupt selected relationships.

“Experience” is an operational data property, not a claim of consciousness, personhood, or human cognition.

## Primary experiment

The first exact-token experiment separates two mechanisms:

1. whether related items share an attention context;
2. whether training windows reach the optimizer in canonical acquisition order.

This produces four matched conditions:

| Condition | Related items share context | Update order |
|---|---:|---|
| relational ordered | yes | canonical |
| local coherence only | yes | shuffled |
| global chronology only | no | canonical |
| fully disrupted | no | shuffled |

Content, token exposure, architecture, optimizer, and evaluation cadence must remain matched.

## Research stance

TL100 is designed to distinguish:

- local relational context from global chronology;
- relational construction from ordinary curriculum learning;
- transfer from recurring-world memorization;
- useful bounded specialization from damaging narrowness;
- unique accepted tokens from repeated training exposures.

A null result, a local-only effect, or a curriculum-only explanation is scientifically valid.

## Repository map

Current Design v3 foundations:

- plan/docs/00_PROJECT_DESIGN.md — canonical project definition, hypotheses, experimental factors, and scale gates
- plan/docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md — primary-source evidence map, counterevidence, threats, and open questions
- AGENTS.md — implementation constraints and migration rules
- PROJECT_HANDOFF.md — concise continuity for contributors

Design v3 migration targets:

- plan/docs/01_WORLD_AND_CONTINUITY.md — canonical graph and acquisition state
- plan/docs/05_EPISODE_SPECIFICATION.md — canonical record and schema specification
- plan/docs/07_CURATION_AND_QA.md — deterministic validation and acceptance gates
- plan/docs/08_CORPUS_FORMAT_AND_VERSIONING.md — compilation, exports, and manifests
- plan/docs/06_GENERATION_PIPELINE.md — pipeline stage contracts

All other documents under plan/docs remain Design v2 legacy inputs until explicitly migrated. They may contain useful ideas, but they are not binding Design v3 requirements.

Supporting directories:

- schemas/ — machine-readable record schemas; currently awaiting D3 migration
- examples/ — schema examples; currently awaiting D3 migration
- data/ — canonical, draft, source, export, and evaluation data roots
- config/ — versioned experiment configuration
- prompts/ — future model-assisted authoring contracts
- tests/ — deterministic validation tests

## Current status

**Design v3 migration.**

The core scientific framing and evidence map are complete. The canonical graph, schemas, deterministic validator, compiler, micro-life, and training harness are not yet operational.

Do not begin bulk generation, bulk source ingestion, or 100M-parameter training.

The first implementation program is a deterministic corpus substrate capable of producing and verifying matched experimental exports.
