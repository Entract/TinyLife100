# 00 — Project Design (v2)

## 1. Project name

**LIFE100**

Working subtitle:

> **A life-structured corpus for studying data organization in a ~100M-parameter language model.**

The name is deliberately about the dataset and target scale, not a novel model architecture.

---

## 2. Central research question

Most language-model pretraining corpora are mixtures of many authors, eras, genres, intentions, domains, viewpoints, reliability levels, duplicated explanations, and unrelated documents.

LIFE100 asks a deliberately different question:

> **What happens when essentially everything a small language model has ever "seen" belongs to one intentionally constructed, internally consistent stream of experience?**

### The v2 definition of “Life”

The Life is **not** merely a very long synthetic autobiography.

The Life is the **causal, chronological, epistemic, and curricular structure that gives every piece of training data a place**.

The narrator:

- experiences events;
- builds and repairs things;
- talks with recurring people;
- makes mistakes;
- conducts experiments;
- reads books, textbooks, manuals, papers, essays, literature, code, and technical artifacts;
- learns some things from other people;
- infers other things from evidence;
- misunderstands some of what is encountered;
- revises beliefs;
- reuses old knowledge in new settings;
- accumulates preferences, vocabulary, memories, unresolved questions, and technical judgment.

Narrator-authored prose remains one persistent first-person voice. External human-authored material may retain its original voice when deliberately included as an experience.

The model therefore does **not** receive one authorial voice. It receives **one point of reception**.

That distinction is fundamental.

---

## 3. Why this is a data experiment

The target model is intentionally conventional. The project does not depend on inventing a new attention mechanism, optimizer, or transformer block.

The experimental object is the corpus:

- what information is included;
- when it appears;
- what prerequisites existed beforehand;
- why the narrator encounters it;
- whether it is experienced, told, read, measured, inferred, or taught;
- how often it recurs;
- what else shares the same context;
- what mistakes mediate learning;
- how human-authored and synthetic material are mixed;
- whether coherent organization changes learning relative to the same tokens shuffled or decontextualized.

The project should therefore spend disproportionate effort on **world design, curriculum design, source curation, chronology, provenance, corpus QA, and experimental controls**.

---

## 4. Research hypotheses

All hypotheses are empirical. The implementation must preserve enough metadata and matched controls to falsify them.

### H1 — Coherent-distribution efficiency

For a fixed small model size and token budget, a tightly coherent corpus may produce unusually strong competence inside its intended world and technical domains relative to a heterogeneous corpus of comparable quality.

### H2 — Curriculum and chronology

Ordering material approximately according to conceptual prerequisites and causal life history may change sample efficiency, retention, transfer, or world consistency relative to globally shuffling the same material.

### H3 — Contextualized external knowledge

Human-authored material may be learned differently when it is encountered at a meaningful point in a life — prompted by a problem, surrounded by prior knowledge and later application — than when the same material is inserted without those bridges.

### H4 — Recurrence creates dense representations

Repeated encounters with the same people, places, machines, projects, concepts, and mistakes across changing contexts may make limited model capacity more useful than equivalent token volume spent on unrelated examples.

### H5 — Stable identity creates behavioral consistency

A persistent narrator may make explanatory habits, uncertainty behavior, conversational style, preferences, and autobiographical/world consistency easier for a small model to learn.

### H6 — Human-authored variation protects linguistic breadth

External books, manuals, literature, papers, and other selected human-authored material may reduce stylistic narrowing and generator-model artifacts while preserving the Life's organizational coherence.

### H7 — Productive imperfection matters

Mistakes, uncertainty, failed hypotheses, corrections, delayed resolution, and conflicting evidence may teach stronger debugging and reasoning behavior than a corpus containing only polished answers.

### H8 — Mixture has an optimum, not a dogma

The useful proportion of Life-native synthetic material versus human-authored reading and technical artifacts is unknown and may vary by capability. It should be treated as an experimental variable rather than fixed from prior synthetic-data studies.

### H9 — Structure can help or hurt

Too much coherence may cause narrowness, memorization, stylistic collapse, weak out-of-distribution behavior, or overdependence on the fictional world. LIFE100 should explicitly measure these failure modes.

---

## 5. Non-goals

LIFE100 is not intended to:

- reproduce frontier-model breadth or capability;
- claim that language models learn like humans;
- create a psychologically realistic human childhood;
- imply subjective experience or consciousness;
- maximize arbitrary benchmark performance;
- optimize broad trivia coverage;
- replace human technical source material with generated imitation;
- invent a novel transformer architecture;
- conceal model narrowness with in-distribution tests;
- assume synthetic data is intrinsically better than natural data;
- assume human-authored data is intrinsically better than carefully designed synthetic data;
- make legal claims about the permissibility of training on particular copyrighted works.

The Life metaphor is a **data-organization principle**.

---

## 6. Model target

Primary target: a conventional decoder-only transformer of approximately **100 million trainable parameters**.

Representative architecture class:

- 8–12 transformer blocks;
- residual width roughly 512–768;
- 8–12 attention heads;
- conventional or gated MLP;
- RMSNorm;
- RoPE or comparable positional method;
- tied embedding/output weights where useful;
- context initially 512–2048 tokens, selected experimentally.

Smaller models (~1M, ~10M, ~30M) are diagnostic instruments and should be trained repeatedly during corpus development.

The final 100M model should not be trained until small-model results justify the data-production cost.

---

## 7. Corpus target

The mature planning target remains approximately **250M unique accepted training tokens**.

That total now includes multiple material classes:

- Life-native narrator prose;
- external human-authored readings;
- technical artifacts/documents/code where intentionally included;
- dialogue or quoted material that naturally belongs to Life episodes;
- derived reflection/application material.

No final percentage is locked.

Recommended releases:

| Release | Compiled unique tokens | Purpose |
|---|---:|---|
| Pilot | 50k–250k | prove schemas, chronology, source encounters, voice, compilation |
| v0 | 1M | train tiny diagnostic models |
| v1 | 5M | validate recurring world + reading integration + curriculum |
| v2 | 25M | first serious mixture/order experiments |
| v3 | 100M | 30M–100M model experiments |
| v4 | 250M | primary 100M-target corpus |
| v5+ | 500M+ | only if results justify |

At each release report:

1. unique compiled tokens;
2. training token exposures;
3. material-class composition;
4. source-origin composition;
5. era/curriculum composition;
6. recurrence and duplication statistics.

---

## 8. The unit of design is not the token

Design at nested scales:

1. **World** — stable reality and constraints
2. **Life** — narrator trajectory and identity
3. **Curriculum** — concept dependency graph
4. **Library** — selected external knowledge sources
5. **Era** — broad developmental stage
6. **Arc** — project, relationship, concept, question, machine, or reading arc
7. **Encounter** — event through which information becomes available
8. **Episode** — narrator-authored coherent event/reflection
9. **Source segment** — external text deliberately encountered
10. **Stream item** — canonical timeline unit pointing to episode/source/artifact
11. **Training passage** — compiled text unit
12. **Token** — tokenizer unit

Bulk generation must never begin at level 12.

---

## 9. What “one life” means

There is one persistent narrator and one canonical timeline.

Every meaningful input to the narrator has an acquisition path.

The project distinguishes:

### Experienced

> I saw the wheel rub the frame.

### Told

> Mara said the startup current could be much higher than the running current.

### Read

> The motor datasheet listed a stall current well above what I had expected.

### Measured

> I measured the rail falling from 5.0 V to 4.1 V during startup.

### Inferred

> I concluded the reset was probably a supply problem rather than a timing bug.

### Believed but wrong

> I was still convinced the firmware was at fault.

These distinctions are metadata and should often be visible naturally in prose.

---

## 10. External knowledge inside the Life

External sources are not random corpus filler.

A source may enter the training stream only through an intentional encounter with metadata such as:

- source ID;
- selected segment/work;
- trigger for reading;
- narrator knowledge before;
- intended curriculum role;
- expected misunderstanding or uncertainty if any;
- rights/licensing status;
- later applications/callbacks.

The source may retain its original voice.

The Life prose around it may include:

- why it was sought;
- anticipation;
- notes;
- questions;
- partial understanding;
- disagreement;
- application;
- later semanticized memory.

Not every reading needs an explicit lesson or reflection. Realistic reading also includes curiosity, pleasure, incomplete attention, and later indirect influence.

See `15_LIBRARY_AND_READING_EVENTS.md`.

---

## 11. Intended cognitive distribution

One identity must not become one rhetorical template.

Deliberately include:

- observation;
- procedural action;
- measurement;
- causal reasoning;
- quantitative calculation;
- comparison;
- hypothesis formation;
- experimental design;
- debugging;
- planning;
- design review;
- dialogue;
- negotiation;
- explanation;
- teaching;
- uncertainty;
- disagreement;
- postmortem;
- memory;
- transfer;
- reading comprehension;
- note-taking;
- source criticism;
- reconciliation of source vs experiment;
- ordinary nontechnical life.

Measure release-level distributions.

---

## 12. Technical subject scope

The life should develop a **deep but bounded technical worldview**.

### Foundations
- objects/properties/categories;
- space/geometry;
- time/sequence;
- number/arithmetic;
- units/measurement;
- uncertainty/estimation;
- observation/evidence/inference.

### Practical making
- hand tools;
- materials;
- fasteners/joints;
- mechanisms;
- friction/force/torque/energy;
- fabrication/tolerances;
- safety.

### Electricity, electronics, instrumentation
- voltage/current/resistance/power;
- circuits;
- motors;
- sensors;
- measurement loading;
- signals/noise;
- oscilloscopes/meters/power supplies;
- calibration.

### Software and computation
- variables/state/control flow;
- functions/abstraction;
- files/parsing;
- testing/debugging;
- version control;
- data structures;
- APIs/databases/networks;
- observability.

### Systems and control
- requirements;
- interfaces;
- feedback;
- setpoint/error;
- stability intuition;
- latency/throughput;
- queues;
- failure modes;
- state estimation;
- redundancy.

### Experimental reasoning
- hypotheses;
- controls;
- confounders;
- uncertainty;
- repeatability;
- calibration/validation;
- evidence quality;
- belief revision.

### Machine learning and language models
- train/validation/test;
- loss/gradient intuition;
- overfitting/generalization;
- representation;
- precision/recall;
- tokenization;
- embeddings;
- transformers/attention/MLPs;
- pretraining/inference;
- KV cache;
- quantization;
- fine-tuning/LoRA/distillation;
- retrieval/RAG;
- agents/tools;
- evaluation.

### Technical judgment and deployment
- problem discovery;
- when not to use AI;
- deterministic/probabilistic boundaries;
- privacy/security/data residency;
- permissions;
- observability;
- acceptance criteria;
- staged deployment;
- cost per task;
- human oversight.

---

## 13. Source grounding and source inclusion

Two distinct source modes exist.

### Mode A — Backstage grounding

Authoritative source material is used to build factual substrates and verify generated Life prose. The source itself does not enter training text.

### Mode B — Explicit reading

A selected source or source segment itself becomes part of the compiled training stream because the narrator encounters it at a designed point in the Life.

Both modes require a source registry.

For every technical unit:

1. identify authoritative or otherwise purposeful sources;
2. record provenance and rights status;
3. map sources to concepts and prerequisites;
4. decide whether the source is grounding-only or eligible for explicit reading;
5. plan encounter timing;
6. validate the narrator's later use of the source;
7. preserve source identity in manifests.

---

## 14. Canonical data versus training views

There is exactly one canonical life timeline.

The source of truth is a sequence of **stream items**, not a single flat text file.

A stream item may reference:

- narrator episode;
- reading-event boundary;
- selected source segment;
- technical artifact;
- reflection/application episode;
- transition marker.

The canonical timeline is never shuffled.

Training exports can then produce:

- `life_ordered`;
- `life_local_shuffle`;
- `global_shuffle`;
- `decontextualized`;
- `curriculum_replay`;
- mixture-controlled exports;
- source-removed or Life-removed ablations.

The same source segment may be **referenced** in multiple experiments, but token exposure must be explicitly tracked.

---

## 15. Fundamental experiments

### Experiment O — Ordered Life

Same architecture/tokenizer/optimizer/token budget. Material occurs in designed Life order, including readings at the moments they are encountered.

### Experiment S — Global Shuffle

Exact same selected training material, randomized globally.

Tests order while holding content constant.

### Experiment D — Decontextualized

Same Life-native prose and same readings, but reading rationale/bridges and later callback structure are removed or minimized while preserving token budget as closely as possible.

Tests whether contextual placement contributes beyond content.

### Experiment M — Mixture sweep

Matched training runs with different proportions of:

- Life-native material;
- human-authored readings;
- technical artifacts/other.

No ratio is assumed optimal in advance.

### Experiment V — Multi-voice Life

Matched Life-native content rewritten across multiple independent narrators/styles.

Tests stable-identity effects.

### Experiment R — Recurrence removed

Recurring objects/people/projects are replaced by one-off equivalents while preserving conceptual content.

Tests recurrence.

### Experiment E — Error-free

Mistakes/corrections are replaced with polished correct exposition where possible.

Tests productive imperfection.

---

## 16. What success would look like

Success is not merely “the model sounds good.”

Success means we can make statements such as:

- contextualized reading improved transfer relative to the same readings shuffled;
- chronology reduced exposures needed for a concept;
- human-authored reading improved linguistic breadth without destroying narrator consistency;
- recurrence improved world memory or cross-domain analogy;
- the Life-heavy mixture improved target-domain behavior but harmed OOD performance;
- a reading-heavy mixture improved language modeling but weakened autobiographical/world consistency;
- mistakes improved fault diagnosis;
- the result was null, and the matched controls show structure did not matter at this scale.

Negative results are valuable if the dataset and controls are auditable.

---

## 17. Development philosophy

Treat the corpus as software and as a scientific instrument:

- schemas;
- tests;
- provenance;
- rights metadata;
- immutable releases;
- diffs;
- source hashes;
- deterministic compilation;
- reproducible manifests;
- matched experiments;
- phase gates;
- small-model diagnostics.

Treat frontier models as contributors, not authorities.

The project's most expensive failure would be generating or acquiring hundreds of millions of tokens before discovering that the ontology, source strategy, voice contract, chronology, mixture, or evaluation design is wrong.
