---
category: feature
---

# TinyLife100 (TL100) — Project Design (Design v3)

> Status: foundational Design v3 specification.
>
> Design v3 supersedes the fictional-human framing of Design v2. A situated learner and its acquisition history are research abstractions, not claims of personhood, consciousness, human cognition, or simulated biography.

## 1. Project identity

**Project name:** TinyLife100

**Short name:** TL100

**Working subtitle:** Life-Structured Relational Pretraining for Small Language Models

TL100 is a dataset-first research project for studying whether small, conventional language models learn differently when their training data preserves explicit relationships among information encounters.

The primary research artifact is the corpus, its relational metadata, its controlled transformations, and the exact manifests describing what each model saw.

The project does not depend on a novel neural architecture.

## 2. Central research question

Most language-model pretraining corpora contain useful local documents but weak global organization. Documents from unrelated authors, domains, times, and purposes are sampled into training contexts with little attempt to preserve causal or developmental relationships between them.

TL100 asks:

> Holding content, token exposure, architecture, tokenizer, and optimization as constant as possible, does preserving causal, temporal, referential, epistemic, and prerequisite structure in a training stream change what a small language model learns?

The strongest version of the hypothesis is not that coherent prose is pleasant, nor that a model trained on a story becomes human-like.

The testable claim is:

> A model may learn some relationships more efficiently, transfer them more reliably, or represent them differently when the corpus makes those relationships repeatedly available in a controlled acquisition structure.

## 3. The situated learner

TL100 organizes information around one **situated learner**.

The situated learner is an epistemic reference point used to answer:

- What information was available?
- In what order did it become available?
- Through which source or interaction?
- What prior information could support understanding?
- What was believed, uncertain, or misunderstood afterward?
- What later observation corrected or reused it?

The learner does not need:

- a human childhood;
- a fictional hometown;
- a dramatic biography;
- a fixed age, gender, personality, or social identity;
- claims of inner experience;
- continuous first-person prose;
- psychologically realistic human development.

The learner may be represented through scenes, observations, dialogues, notebooks, measurements, artifacts, source readings, plans, explanations, and reflections. These are data forms attached to one acquisition history.

“Life” remains a compact project metaphor for this persistent acquisition history. In technical specifications, prefer **situated learner**, **relational stream**, and **acquisition state**.

## 4. What “experienced” means

In TL100, “experienced” is an operational data property.

An item is experienced when the canonical records state:

1. why it became available;
2. what acquisition mode exposed it;
3. what the learner state was before it;
4. what state changes it proposed;
5. which later items depend on, revisit, test, correct, or apply it.

Experience is therefore not a metaphysical claim. It is a provenance-rich relationship between a learner state and a corpus item.

## 5. The relational stream graph

The canonical scientific object is a directed, typed graph plus one canonical stream order.

### 5.1 Node classes

Initial node classes:

- **encounter** — a bounded event in which information becomes available;
- **observation** — recorded evidence from an environment or artifact;
- **action** — an attempted intervention or procedure;
- **conversation** — information exchanged among identified participants;
- **source segment** — external text with provenance and rights metadata;
- **artifact** — code, log, table, diagram, specification, configuration, or other structured object;
- **reflection** — an interpretation, comparison, plan, explanation, or belief update;
- **assessment** — a probe, test, or task used to evaluate current competence.

Node types may be refined after schema prototyping. They must not be multiplied merely to encode prose genres.

### 5.2 Edge classes

Every important relationship must be explicit and independently addressable.

- **temporal** — A occurred before B;
- **causal** — A caused or materially contributed to B;
- **prerequisite** — understanding A is expected to support B;
- **entity recurrence** — A and B concern the same persistent entity;
- **project continuation** — B continues an objective or constraint established in A;
- **acquisition** — A made a claim, term, procedure, or observation available;
- **belief support** — A increased support for a belief;
- **belief conflict** — A conflicted with a current belief;
- **correction** — A revised or invalidated an earlier belief;
- **source application** — B applies information encountered in source A;
- **memory or callback** — B reuses an earlier event after a meaningful interval;
- **analogy or transfer** — B applies a structure learned in A to a different surface domain.

Each accepted edge should include:

- stable edge ID;
- edge type;
- source node;
- target node;
- design rationale;
- confidence or review state where appropriate;
- whether the edge is visible in text, metadata only, or both.

### 5.3 Canonical order

The canonical stream is a reviewed linearization of the graph. It must respect hard temporal and acquisition constraints.

Canonical order is immutable within a release.

Training exports may reorder or mask relationships, but they never overwrite canon.

## 6. Experimental factors

Design v3 separates factors that Design v2 often bundled together.

### 6.1 Local relational context

Are causally or referentially connected items visible together inside the model’s attention context?

### 6.2 Global update order

Are training windows presented to the optimizer in canonical acquisition order or a controlled shuffle?

This is distinct from local context. A standard transformer does not carry an activation state across independent batches; global chronology can influence later learning only through parameter updates and the training schedule.

### 6.3 Prerequisite curriculum

Are prerequisite concepts introduced before dependent uses?

Curriculum order can help even without a persistent learner. It therefore requires a separate control.

### 6.4 Relational construction

Does the text itself contain recurring entities, causal bridges, source-to-application links, and belief revision, or is equivalent content presented as independent material?

This factor requires content-matched rewriting and is less perfectly controlled than order-only experiments.

### 6.5 Stable epistemic center

Does one acquisition history improve temporal belief tracking, source attribution, correction behavior, or recurring-entity knowledge?

### 6.6 Material mixture

What proportion of the stream is project-authored narrative or explanation, external human-authored text, and structured artifacts?

Mixture is a later factor. It must not be conflated with the first ordering and relational experiments.

## 7. Hypothesis hierarchy

### H1 — Local relational availability

For the same text and exposure count, placing related items in the same attention context improves performance on tasks requiring those relationships.

### H2 — Global acquisition order

After controlling for local context, presenting training windows in acquisition order changes sample efficiency, retention, or transfer relative to shuffled update order.

### H3 — Relational construction

Content organized around recurring entities, causal consequences, source application, and belief revision produces stronger relational transfer than content-matched standalone passages.

### H4 — Epistemic-center effects

A stable acquisition history improves temporal knowledge, source attribution, uncertainty, and obsolete-belief rejection.

### H5 — Bounded-distribution efficiency

A small model may achieve unusually dense competence inside a bounded relational domain, at the cost of some linguistic or out-of-distribution breadth.

### H6 — Human-source contribution

Human-authored sources may protect linguistic breadth and add useful alternative structures, but the useful mixture depends on model size, data budget, source selection, and experimental objective.

### H0 — Null

Once text, exposure, local context, curriculum, and optimization are controlled, relational stream structure produces no reliable advantage beyond memorizing its own recurring world.

The null is a valid and informative outcome.

## 8. Minimum exact-token experiment

The first scientific experiment uses the same accepted text units and exposure counts under four conditions.

| Condition | Related neighboring items share attention context | Training-window update order |
|---|---:|---|
| relational ordered | yes | canonical |
| local coherence only | yes | shuffled |
| global chronology only | no; cross-item attention is masked or reset | canonical |
| fully disrupted | no; cross-item attention is masked or reset | shuffled |

The compiler must hold constant:

- selected text units;
- tokenized text;
- total token exposures;
- tokenizer;
- model architecture;
- optimizer and schedule;
- number of updates;
- padding and loss masking as closely as possible;
- checkpoint and evaluation cadence;
- separator policy;
- random seeds where the comparison permits.

Any unavoidable difference must be declared in the export manifest.

### 8.1 Why this experiment comes first

It separates information that is available directly to attention from information that can affect learning only through weight updates.

It does not require rewriting the corpus, so the token content can remain exactly matched.

### 8.2 Second experiment: relational versus delinked

If the exact-token experiment shows a signal, build a content-matched control that removes or replaces:

- persistent identities;
- explicit callbacks;
- causal bridges;
- acquisition framing;
- belief history;
- source-to-application links.

This experiment tests relational construction rather than ordering. Because rewriting changes surface text, it requires stronger matching, independent review, and explicit caveats.

### 8.3 Curriculum control

A curriculum-only condition should preserve prerequisite tiers while removing fine-grained acquisition chronology. This tests whether any TL100 benefit is simply ordinary curriculum learning.

## 9. Minimum corpus

The first corpus should be a **micro-life**, not a simulated lifetime.

Recommended scope for the first manually inspectable corpus:

- one situated learner;
- three to six recurring entities;
- two or three bounded technical domains;
- four to eight project or investigation arcs;
- twenty to sixty explicitly tracked concepts;
- several plausible errors and corrections;
- several delayed callbacks;
- at least two cross-domain transfer targets;
- a small, fixed, rights-clear source set if external readings are used.

The corpus should be large enough to express relationships and small enough that a human can inspect every node, edge, and transition.

The learner’s biography is deliberately underspecified unless a field is required for continuity or an experiment.

## 10. Acquisition and knowledge state

Important information changes must record an acquisition mode:

- observed;
- measured;
- read;
- told;
- inferred;
- tested;
- taught or explained;
- believed without sufficient support;
- corrected.

World or task truth and learner state are separate.

For any important claim at stream position T, the system should be able to answer:

- Is the claim true in the controlled environment?
- Was it available by T?
- Through what path?
- Was it believed, doubted, or misunderstood?
- What later event changed that state?

This enables deterministic detection of information appearing before acquisition and evaluation of obsolete-belief behavior.

## 11. Sources and rights

External sources are optional inputs, not corpus filler.

Every source requires:

- stable identity and version;
- provenance;
- selected segment identity and hash;
- storage mode;
- redistribution status;
- training-use status under project policy;
- role in the experiment;
- acquisition placement if included in the canonical stream.

Public accessibility does not imply redistribution or training permission.

For the first order experiment, use either no external text or a small rights-clear set held identical across all conditions. Mixture experiments come later.

## 12. Canon, content pool, and training exports

TL100 separates:

1. **canonical graph and stream** — what became available and how nodes relate;
2. **content pool** — exact text and artifact payloads eligible for compilation;
3. **training export** — exact token sequence, attention-boundary policy, ordering, sampling schedule, and exposures used for one run.

Every export must be reproducible from versioned inputs and an exact manifest.

The canonical graph is never shuffled or rewritten in place.

## 13. Evaluation

### 13.1 Primary outcomes

- sample efficiency on held-out relational tasks;
- transfer to new surface forms or projects;
- temporal and epistemic accuracy;
- rejection of corrected or obsolete beliefs;
- source-to-application transfer where sources are present.

### 13.2 Secondary outcomes

- held-out language-model loss by material class;
- recurring-entity consistency;
- causal and prerequisite reasoning;
- calibration and uncertainty;
- learning-curve shape;
- retention after later curriculum stages.

### 13.3 Required negative and external controls

- unrelated human prose;
- novel names and objects using known mechanisms;
- questions whose answers were never available;
- source holdouts;
- content-composition tasks not rehearsed directly;
- verbatim memorization probes;
- stylistic-diversity and monotony measures.

World recall alone is not evidence for the central hypothesis.

### 13.4 Experimental discipline

- use multiple training seeds;
- predeclare primary metrics and comparisons;
- evaluate checkpoints throughout training;
- report confidence intervals and run variance;
- preserve failed and null runs;
- do not choose the best condition after inspecting the test set.

## 14. Success, null, failure, and stop conditions

### Proceed

Proceed to larger data or models only when a structural condition produces a repeatable improvement in transfer, epistemic behavior, or sample efficiency across seeds without an unacceptable external-language penalty.

### Interesting null

If exact-token order has no effect but local context does, TL100 should narrow toward context construction rather than global chronology.

If curriculum-only matches the full stream, the useful mechanism is curriculum and the persistent learner should not be credited.

### Failure

Treat the initial thesis as unsupported if apparent gains reduce to:

- memorization of recurring names;
- easier or cleaner prose;
- extra token exposure;
- more replay;
- source-quality differences;
- evaluation leakage;
- one favorable seed;
- worse external transfer hidden by in-world tests.

### Stop

Do not scale corpus generation when:

- schemas or manifests cannot reproduce exact exports;
- rights status is incomplete;
- corpus transformations cannot be matched;
- critic scores replace deterministic validation;
- small-model learning curves show no interpretable signal;
- generator artifacts dominate the text distribution.

## 15. Scale strategy

Model size and corpus size are experimental axes, not project identity.

### Pipeline pilot

Approximately 100k–250k accepted tokens.

Purpose:

- validate schemas;
- validate relation edges and acquisition state;
- compile exact experimental views;
- inspect every item manually;
- run smoke-training only.

### First scientific corpus

Provisional range: 5M–20M unique accepted tokens.

Use several small model sizes, likely spanning roughly 3M–30M parameters, and multiple seeds. Final choices must follow compute estimates and pilot learning curves.

### Intermediate scaling

Scale toward 25M–100M tokens only after the minimum experiment is reproducible and evaluable.

### 100M-parameter target

A conventional model near 100M parameters remains a useful eventual target because it is large enough to exhibit nontrivial language behavior and small enough to train and inspect comparatively.

It is not a commitment to a 250M-token corpus or a claim of compute-optimal general-language training. Unique tokens, repeated exposures, and total training tokens must be reported separately.

## 16. Architecture stance

The primary model family is a conventional decoder-only transformer.

Architecture experiments are allowed for learning purposes, but the central relational-data comparisons must first hold architecture constant.

Smaller diagnostic models are scientific instruments, not merely prototypes.

## 17. Pipeline priority

The first implementation program is a deterministic corpus substrate:

1. validate and version schemas;
2. implement graph nodes, typed edges, and acquisition-state records;
3. implement source provenance and rights gates;
4. implement immutable canonical stream storage;
5. implement exact compilation and manifests;
6. implement the four minimum experimental views;
7. implement deterministic validation and leakage checks;
8. author and inspect the micro-life;
9. implement a minimal training and evaluation harness;
10. run small matched experiments.

Model-assisted generation stages come only after the deterministic substrate can reject invalid output.

## 18. Non-goals

TL100 does not aim to:

- simulate a human being;
- claim that transformers learn like humans;
- imply consciousness or subjective experience;
- write a technical coming-of-age novel;
- maximize broad benchmark scores;
- prove chronological order is universally beneficial;
- replace human-authored text with generated imitation;
- lock an optimal synthetic/human mixture in advance;
- build a novel transformer before testing the data hypothesis;
- scale to hundreds of millions of tokens before small falsification attempts;
- treat a pleasing narrative sample as scientific evidence.

## 19. Principal threats to validity

- **Bundled variables:** coherence, curriculum, style, source quality, and recurrence change together.
- **Training-order ambiguity:** canonical file order has no effect if the sampler globally shuffles it.
- **Context leakage:** one condition exposes related items inside a context while another changes token or padding budgets.
- **Generator signature:** a model learns the authoring model’s style rather than relational structure.
- **Domain narrowness:** in-world improvement masks external degradation.
- **Evaluation leakage:** tests restate training facts or surface forms.
- **Replay imbalance:** ordered conditions receive different effective exposure.
- **Seed variance:** a subtle result is reported from one run.
- **Capacity mismatch:** the tested model is too small or too large for the selected dependencies.
- **Anthropomorphic interpretation:** acquisition metadata is mistaken for human experience.

Every experiment must state which threats it controls and which remain.

## 20. Design v2 migration status

Design v3 retains these principles from v2:

- dataset-first research;
- conventional model architecture;
- one traceable acquisition history;
- explicit provenance and rights metadata;
- separation of canonical records from training views;
- immutable releases and exact manifests;
- deterministic validation;
- matched controls;
- small-model experiments before scale;
- human review of contiguous data;
- external sources retaining their actual authorship when intentionally included.

Design v3 discards or withdraws as assumptions:

- Alex as a canonical narrator;
- Rookfield and its fictional cast;
- a simulated 15–25-year human life;
- biography as the primary organizing object;
- first-person prose as the dominant or required format;
- the first 30 project arcs as a committed backbone;
- the first 100 episode plan as a committed chronology;
- 250M unique tokens as a settled target;
- any predetermined material mixture.

Until individually migrated, plan documents 01 through 16 and the current schemas/examples are **Design v2 legacy inputs**, not binding Design v3 specifications. They may contain useful mechanisms, but implementations must not infer D3 requirements from them without explicit migration.

The evidence map in 17_RESEARCH_RATIONALE_AND_OPEN_QUESTIONS.md is part of Design v3.

## 21. Naming convention

Use:

- **TinyLife100** for the project;
- **TL100** as the short form;
- **relational stream** for the ordered corpus abstraction;
- **situated learner** for the acquisition reference point;
- **acquisition state** for what is available, believed, uncertain, or corrected;
- **canonical graph** for nodes and typed relationships;
- **training export** for one exact compiled condition.

Do not use the former all-caps project name as current terminology.

## 22. Immediate next design slices

After this foundation:

1. normalize project naming and plan/docs references;
2. replace the world/continuity specification with the canonical graph and acquisition-state specification;
3. replace the curriculum specification with relation and prerequisite schemas;
4. redesign canonical node, edge, source, stream, and export schemas;
5. specify deterministic compiler and validator behavior;
6. specify the micro-life and evaluation protocol;
7. decompose the operational pipeline into shippable implementation tasks.

No bulk data generation begins during these migrations.
