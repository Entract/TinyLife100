# 12 — Corpus Token Budget and Content Shape (v2)

## 1. Mature target

Provisional mature compiled corpus:

> **~250 million unique accepted training tokens**

This is a target for a future ~100M-parameter model experiment, not a requirement to generate 250M tokens of synthetic prose.

---

## 2. Two orthogonal budgets

LIFE100 must budget data along **two independent axes**.

### Axis A — developmental/curriculum era

What stage of the Life is represented?

### Axis B — material class/origin

What kind of text is it?

- Life-native narrator prose;
- human-authored reading;
- technical artifact/document/code;
- other approved material.

A mature corpus plan is a matrix, not one list of episode counts.

---

## 3. Provisional era allocation

Keep the original 250M developmental envelope as a planning guide:

| Era | Dominant focus | Compiled tokens |
|---|---|---:|
| 0 | orientation, causality, ordinary reasoning | 10M |
| 1 | measurement, tools, making, mechanics | 25M |
| 2 | electricity, electronics, instrumentation | 30M |
| 3 | software, state, debugging, computation | 40M |
| 4 | systems, networks, interfaces, control | 35M |
| 5 | experimental reasoning and technical judgment | 25M |
| 6 | machine learning foundations | 25M |
| 7 | language models, retrieval, agents, evals | 35M |
| 8 | integrated deployment/teaching/projects | 25M |
| **Total** |  | **250M** |

These are broad allocation targets, not evidence-based optima.

The material-class mixture can vary strongly by era.

---

## 4. Do not lock the global mixture yet

The project currently assumes **no optimal Life/human ratio**.

Infrastructure should support a planning envelope of roughly:

- 30–70% Life-native;
- 20–60% human reading;
- 5–20% technical artifacts/other.

These ranges are operational, not prescriptive.

The final v4 mixture must be selected from 5M/25M experiments.

---

## 5. Example mature compilations

All of these are plausible *experimental* 250M-token shapes:

### Life-heavy

- 175M Life-native
- 50M human reading
- 25M artifact/other

### Balanced

- 125M Life-native
- 87.5M human reading
- 37.5M artifact/other

### Reading-heavy

- 75M Life-native
- 137.5M human reading
- 37.5M artifact/other

These are examples for planning storage/source needs, not recommendations.

---

## 6. Material mixture should evolve by era

A realistic developmental shape may look like:

### Early Life

Mostly experience, conversation, short manuals/handouts, simple technical references, ordinary reading.

### Mid technical Life

Increasing textbook chapters, manuals, datasheets, documentation, code, and longer technical books.

### Later technical Life

More papers, standards/specifications, implementation docs, codebases, system documents, and specialized books.

### Throughout

Bounded literature/essays/ordinary nontechnical reading to preserve linguistic and human breadth.

The Life should not begin with an adult engineer's library dumped into Era 0.

---

## 7. Life-native cognitive-mode targets

Within Life-native material, continue to measure approximately:

| Mode | Rough planning share of LIFE_NATIVE | Notes |
|---|---:|---|
| practical project/action | 25% | build, use, test, repair |
| technical explanation/learning | 15% | lower than v1 because readings carry some exposition |
| debugging/mistake/postmortem | 18% | high-value recurrence |
| conversation/collaboration | 15% | natural social learning |
| planning/design/requirements | 10% | grows later |
| reflection/memory/transfer | 10% | source integration and recurrence |
| ordinary connective life | 7% | linguistic/world realism |

Do not force exact per-episode quotas.

---

## 8. External-reading budget dimensions

For `HUMAN_READING`, track more than tokens:

- source count;
- author count;
- median/longest source share;
- technical/nontechnical split;
- textbook/manual/paper/literature distribution;
- coherent-unit lengths;
- rereading frequency;
- source difficulty by era;
- source concentration.

A 100M-token reading pool dominated by three authors is not equivalent to a 100M-token diverse library.

---

## 9. Episode volume

Life-native episodes remain hierarchical:

- micro-scene: 200–600 tokens;
- episode: 800–4,000 tokens;
- session/chapter: 5k–20k tokens;
- arc: 30k–500k+ tokens;
- era: millions of tokens.

External source segments should retain coherent native boundaries and should not be forced into episode-size chunks.

At 250M compiled tokens, Life-native token share determines episode count. This is another reason not to equate corpus size with number of generated episodes.

---

## 10. Unique data versus exposures

Track separately:

- unique Life-native tokens;
- unique external-source tokens;
- unique artifact tokens;
- compiled unique tokens;
- reread/replay exposures;
- total training exposures.

Example:

> A 10k-token textbook chapter read twice contributes 10k unique source tokens and 20k training exposure tokens if both encounters are compiled.

Never conflate these.

---

## 11. Release strategy

### Pilot: 50k–250k

Read everything. Use a tiny source library and only a handful of explicit readings.

### v0: 1M

Still small enough for heavy human inspection. Establish mixture dashboards.

### v1: 5M

First meaningful mixture/order/context tests.

### v2: 25M

Select likely promising mixture directions.

### v3: 100M

Production-like corpus construction.

### v4: 250M

Only after training curves and source/Life QA justify scale.

---

## 12. What we are optimizing

Not:

> maximum facts per token

and not:

> maximum amount of prestigious human text

Instead:

> **maximum learnable, reusable, causally integrated structure per token for a small model.**

A motor problem can connect:

- physical load;
- measurement;
- a datasheet reading;
- current/power;
- a mistaken firmware hypothesis;
- Mara's questioning style;
- an old cart memory;
- a later pump failure;
- systems debugging habits.

A source becomes valuable not only because of what it says, but because of **what the Life does with it**.
