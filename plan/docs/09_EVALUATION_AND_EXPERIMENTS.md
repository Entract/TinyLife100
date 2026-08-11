# 09 — Evaluation and Experiments (v2)

## 1. Evaluation philosophy

TL100 should be judged as a **data-structure experiment**, not by whether a few generations sound charming.

Evaluate:

- language modeling;
- technical competence;
- world consistency;
- temporal/epistemic knowledge;
- transfer;
- conversational behavior;
- narrator consistency;
- source comprehension/use;
- out-of-distribution behavior;
- mixture effects;
- matched ablations;
- mechanistic changes across training.

---

## 2. Core ordering experiment

Train matched models with equal selected text and equal token exposures.

### O — LIFE-ORDERED

Canonical progression with readings at designed moments and configured replay.

### S — GLOBAL-SHUFFLE

Same selected Life episodes, source segments, and artifacts, randomized globally.

This isolates organization/order while holding content constant as closely as possible.

---

## 3. Contextualization experiment

### C — CONTEXTUALIZED

A source is preceded by the Life problem/curiosity that motivates it and followed by its natural response/application/callback structure.

### D — DECONTEXTUALIZED

Same source text and matched Life-native token budget, but source placement is separated from its designed trigger/bridges where possible.

Key question:

> Does a textbook chapter learned because the amplifier oscillated behave differently from the same chapter inserted as ordinary corpus text?

---

## 4. Mixture experiments

Treat mixture as an empirical variable.

Initial candidates:

| Condition | Life-native | Human reading | Artifact/other |
|---|---:|---:|---:|
| P | 100% | 0% | 0% |
| L | 70% | 20% | 10% |
| B | 50% | 35% | 15% |
| R | 30% | 55% | 15% |

These are experimental starting points, not final doctrine.

Measure whether increasing human-authored input changes:

- held-out loss;
- lexical/style breadth;
- technical transfer;
- narrator consistency;
- world memory;
- OOD robustness;
- hallucination/uncertainty behavior.

---

## 5. Additional ablations

### F — Flat textbook

Convert matched conceptual Life-native content into independent textbook-like passages.

### V — Multi-voice Life

Rewrite matched Life-native content across independent narrators/formats.

### N — Recurrence removed

Replace recurring entities/projects with semantically equivalent one-offs.

### E — Error-free

Remove mistakes/corrections and present polished correct explanations.

### H — Human-source fragmentation

Preserve the same selected human-source text but fragment/shuffle coherent source units.

### G — Grounding-only

Use external sources only backstage; exclude explicit human reading text from the training stream while preserving similar Life curriculum.

These are expensive; run them first on small subsets/models.

---

## 6. Evaluation families

### A. Language modeling

- held-out loss/perplexity;
- by material class;
- by origin;
- by era;
- by cognitive mode;
- on unseen human prose;
- on unseen Life-like prose.

### B. Canonical world consistency

Probe:

- machine history;
- relationships;
- project outcomes;
- place layouts;
- stable preferences;
- unresolved questions;
- source/read history.

Separate directly repeated facts from relational inference.

### C. Temporal and epistemic knowledge

Can the model distinguish:

- what Alex knew at time T;
- what Alex had read by time T;
- what Alex merely suspected;
- later corrected beliefs;
- source claims versus experimental evidence;
- sequence of events.

### D. Concept understanding

- definitions;
- worked examples;
- boundary cases;
- error diagnosis;
- explanation at multiple levels.

### E. Transfer

Use novel projects/surface forms requiring known mechanisms.

Example: learn feedback from temperature control; test on tank level or motor speed.

### F. Reading/source integration

Test whether the model can:

- use ideas from a source in a novel Life problem;
- reconcile a source with experimental evidence;
- distinguish which source introduced a concept;
- avoid attributing external prose to Alex;
- generalize source concepts without reproducing source wording.

### G. Conversational behavior

- clarification;
- uncertainty;
- correction handling;
- concise vs deep explanation;
- maintaining context;
- resisting invented facts.

### H. Narrator consistency

Blind raters compare generated Life-native passages to voice references.

### I. Narrowness / OOD

Probe intentionally absent topics and unfamiliar human prose.

Characterize:

- hallucination;
- linguistic generalization;
- uncertainty;
- transfer despite missing facts.

### J. Mechanistic inspection

At smaller checkpoints inspect:

- attention patterns;
- embedding neighborhoods;
- activation probes;
- representational change before/after major reading events;
- concept/source associations;
- recurrence effects.

---

## 7. Evaluation split design

Do not rely on random episode withholding.

Use:

### Chronological holdout
Entire future arcs withheld.

### Project holdout
Novel project requiring known principles.

### Source holdout
Withhold particular books/authors while testing the same concepts in new formulations.

### Surface-transfer set
Novel names/objects but same mechanisms.

### Concept-composition set
Requires combining concepts never jointly rehearsed.

### Counterfactual set
Changes a world parameter and tests reasoning from supplied facts.

### Unanswerable set
Asks for facts Alex could not know.

### Voice challenge set
Prompts likely to trigger generic assistant prose.

### Reading-transfer set
Uses concepts from readings in new applications without source wording.

---

## 8. Training checkpoints

Save:

- initialization;
- early token milestones;
- before/after important curriculum phases;
- before/after selected reading-heavy blocks;
- fixed token milestones;
- final.

Run compact evals at each checkpoint.

This lets us ask **when** source-derived knowledge, narrator habits, and transfer emerge or disappear.

---

## 9. Data scaling study

Before v4 compare selected points across:

- 1M;
- 5M;
- 25M;
- 100M;
- 250M tokens.

Diagnostic model sizes may include:

- ~1M;
- ~10M;
- ~30M;
- ~100M parameters.

Do not fully cross every combination. Use pilot curves to choose informative runs.

---

## 10. Memorization versus generalization

Distinguish:

- **world memory** — canonical facts;
- **source memory** — knowledge tied to readings;
- **concept memorization** — repeated explanation;
- **verbatim source memorization** — reproducing human text;
- **structural transfer** — solving a novel problem.

Verbatim memorization should be measured especially for repeated readings and small source pools.

---

## 11. Success criteria before expensive final training

Do not rent substantial compute for the final v4 100M run until:

- small models learn nontrivially from v1/v2;
- source inclusion pipeline is provenance/rights clean;
- no severe Life/source copying pathology is present;
- at least one ordering/context/mixture result is interesting enough to scale, or the null result itself is scientifically worth confirming;
- voice/continuity metrics are stable;
- technical error rate is acceptable;
- source concentration is controlled;
- pipeline cost per accepted token is understood;
- held-out transfer improves with corpus growth;
- monotony and source-fragmentation problems are under control.

---

## 12. Interpretation discipline

Possible outcomes are all informative:

- chronology matters;
- chronology does not matter;
- human readings improve breadth but hurt Life consistency;
- Life-heavy data improves target behavior but narrows language;
- source contextualization matters more than mixture;
- coherent source units matter but Life bridges do not;
- recurring mistakes improve diagnosis;
- 100M parameters are too small to exploit the structure;
- benefits appear only at particular data/model ratios.

The repository must preserve enough exact data provenance that results cannot be dismissed as “we do not know what the model actually saw.”
