# TinyLife100 (TL100) — Project Handoff (Design v3)

## What this repository is

TinyLife100 is a dataset-first scientific investigation into relational pretraining for small language models.

It asks whether preserving causal, temporal, referential, epistemic, and prerequisite relationships in a training stream changes learning relative to matched disruption.

The architecture is intentionally conventional. The experimental object is the data structure, compiler, manifests, and controlled training views.

## Foundational Design v3 decision

TL100 does not construct a fake human life.

It uses one **situated learner** as an acquisition reference point. Records track:

- what information became available;
- why and how it became available;
- what prior information existed;
- what was believed, uncertain, or misunderstood;
- which later items reused, tested, contradicted, or corrected it.

The learner is not a claim of personhood, consciousness, human cognition, or psychological realism.

## Read first

1. plan/docs/00_PROJECT_DESIGN.md
2. plan/docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md
3. AGENTS.md

Then read only the Design v3 document attached to the task being implemented.

Documents 01 through 16 remain legacy Design v2 inputs until their migration is explicit. Do not implement a legacy assumption merely because it appears detailed.

## Current scientific design

The canonical object is a directed graph plus one immutable stream order.

Important edge classes include:

- temporal;
- causal;
- prerequisite;
- entity recurrence;
- project continuation;
- acquisition;
- belief support or conflict;
- correction;
- source application;
- callback;
- analogy or transfer.

The first experiment uses identical text and exposure counts while independently varying:

- whether related items share an attention context;
- whether training windows are presented in canonical or shuffled update order.

A later content-matched experiment can remove recurring identities, callbacks, belief history, and source-to-application bridges.

## Current migration state

Design v3:

- plan/docs/00_PROJECT_DESIGN.md
- plan/docs/17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md
- README.md
- PROJECT_HANDOFF.md
- AGENTS.md

Awaiting D3 migration:

- canonical graph and acquisition-state specification;
- record schemas and examples;
- deterministic QA and rights gates;
- compiler, export, and manifest specification;
- pipeline stage contracts;
- evaluation protocol;
- micro-life content plan;
- implementation.

## Immediate sequence

1. Normalize naming and plan/docs references.
2. Specify the canonical graph and acquisition state.
3. Redesign schemas and examples.
4. Specify deterministic validation and rights gates.
5. Specify compilation and exact export manifests.
6. Derive granular implementation tasks.

No bulk data generation occurs during this sequence.

## Non-negotiable engineering rules

- Canon is append-oriented and immutable within a release.
- Canon and training exports are separate.
- Same-token comparisons require exact exposure manifests.
- World or task truth and learner state are separate.
- Source provenance and rights status are hard gates.
- Model critics never replace deterministic checks.
- Small matched experiments precede scale.
- Null and negative results are retained.

## Naming

Use **TinyLife100** or **TL100** for the current project.

Use **situated learner**, **relational stream**, **acquisition state**, **canonical graph**, and **training export** for the main technical abstractions.
