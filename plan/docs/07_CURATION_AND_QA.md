# 07 — Curation and Quality Assurance (v2)

## 1. Quality dimensions

Every release should be evaluated across at least:

- technical correctness;
- world continuity;
- epistemic correctness;
- chronology;
- curriculum/prerequisites;
- acquisition-mode diversity;
- narrator voice consistency;
- external-source integrity;
- provenance/rights completeness;
- linguistic diversity;
- recurrence quality;
- duplication/copying;
- mixture balance;
- Life realism;
- transfer density.

A passage can be excellent prose and still be invalid corpus data.

---

## 2. Failure taxonomy

### Factual fabrication
Generated claim is unsupported or false.

### Continuity contradiction
Entity/world/source history conflicts with canon.

### Epistemic leak
Alex uses knowledge before observing, being told, reading, measuring, or inferring it.

### Curriculum jump
Material assumes prerequisites that have not plausibly been acquired.

### Retcon
Later prose silently changes earlier canonical facts.

### Voice drift
Life-native prose stops sounding like Alex.

### Source-voice erasure
External material is unnecessarily rewritten into Alex's style, defeating one purpose of explicit reading.

### Source leakage
Generated Life prose reproduces source wording/structure beyond intended quotation or synthesis.

### Reading dump
A source is inserted because it is useful text, not because it belongs causally in the Life.

### Perfect-book syndrome
Every reading immediately and perfectly solves the current problem.

### Textbook disguise
Life-native prose is a generic tutorial with a few first-person decorations.

### Dialogue puppet
Characters exist only to feed exposition.

### Synthetic repetition
Repeated sentence shapes, morals, transitions, or lesson templates.

### Overcoherence
The world becomes implausibly arranged so every ordinary event teaches exactly the next concept.

### Undercoherence
Episodes are locally fine but recurring entities/knowledge do not accumulate meaningfully.

### Concept starvation
Important concepts appear too rarely to consolidate.

### Concept saturation
One concept is repeated so heavily that apparent competence is memorization.

### Tail collapse
Language/style/world become too narrow and predictable.

### Source monoculture
One author/publisher/source type dominates human-written material.

### Rights ambiguity
Source is included without explicit permitted status under project policy.

### Hidden repetition
Same source segment or paraphrase appears repeatedly without exposure accounting.

---

## 3. Quantitative dashboards

Track at release level:

### Corpus composition
- tokens by material class;
- tokens by origin;
- Life-native vs human-reading vs artifact share;
- source count and concentration;
- tokens by era/domain/cognitive mode;
- explicit rereading/replay exposures.

### Continuity
- entity recurrence intervals;
- unresolved-question age;
- concept recurrence intervals;
- source callback rate;
- contradictions found per million tokens.

### Language
- n-gram/semantic duplication;
- repeated openings/endings;
- dialogue proportion;
- sentence-length distribution;
- narrator lexical drift;
- source-vs-Life style separation.

### Quality
- critic scores;
- rejection/revision rate;
- technical issues per sampled 10k tokens;
- provenance completeness;
- rights-status completeness;
- source-copy overlap flags.

Dashboards diagnose; they do not replace reading.

---

## 4. Technical validation

Technical generated content should trace to an approved substrate/source set.

Checks include:

- equations/units;
- realistic component behavior;
- numerical consistency;
- safety framing where required;
- version-sensitive software/API claims if included;
- distinction between source claim and narrator inference.

For explicit readings, technical QA asks whether the selected source is fit for purpose and whether surrounding Life prose represents it accurately, not whether the project should silently rewrite the source.

---

## 5. Continuity and epistemic validation

For each candidate episode/reading transition ask:

- Can Alex know this yet?
- If yes, how?
- Has the relevant source actually been encountered?
- Is this a remembered detail or a newly inferred one?
- Does the source contradict Alex's current belief, and is that modeled?
- Are people/machines/places in plausible states?
- Are old mistakes reused naturally rather than quoted ritualistically?

Important concepts should retain an acquisition trace.

---

## 6. Source QA

Every explicit source inclusion must pass:

1. source identity verified;
2. selected segment boundaries verified;
3. content hash recorded;
4. provenance recorded;
5. rights/training-use status approved;
6. Life trigger plausible;
7. prerequisite fit acceptable;
8. contribution distinct enough to justify tokens;
9. source concentration checked;
10. later integration plan present where appropriate.

For pilot data, a human should inspect every explicit reading.

---

## 7. Voice diversity paradox

LIFE100 wants both:

- a stable narrator voice;
- broader linguistic exposure.

Design v2 resolves this by separating **Life-native voice** from **external source voices**.

QA should therefore test two things independently:

### Narrator stability
Does Alex remain recognizable across eras and writer models?

### Corpus linguistic breadth
Does the overall training stream contain enough human-authored stylistic/structural variety to avoid a synthetic monoculture?

Do not "harmonize" the entire corpus into one voice.

---

## 8. Human review protocol

At phase gates, reviewers should run these tests.

### Life test
Does a contiguous run feel causally connected rather than assembled?

### Person test
Do recurring people have history, independent competence, and non-expository roles?

### Memory test
Do old experiences change later behavior naturally?

### World test
Do places and machines feel persistent?

### Learning test
Can we explain why Alex knows each important thing now?

### Reading test
Does each explicit source feel like something Alex plausibly encountered for a reason?

### Source test
Are sources correctly represented, not copied into narrator prose, and rights/provenance complete?

### Teaching test
Do explanations emerge from genuine need rather than compulsory mini-lectures?

### Synthetic test
Can a reviewer detect repeated frontier-model habits/templates?

### Density test
Does an episode reinforce multiple useful structures without becoming overloaded?

### Normality test
Does enough ordinary life remain to stop the world becoming an educational theme park?

---

## 9. Red-team corpus creation

Build adversarial probes for the dataset itself:

- ask generation model to introduce a source Alex has not read;
- tempt it to quote a recent source verbatim;
- place a difficult textbook too early;
- contradict a machine spec;
- give Alex knowledge from a future era;
- repeat a familiar lesson with new nouns;
- insert an attractive but rights-blocked source;
- create a human-reading-heavy section that erases narrator continuity;
- create a Life-heavy section with extreme style monotony.

The pipeline should fail safely.

---

## 10. Acceptance thresholds

Do not define one scalar “quality score.”

Use hard gates for:

- schema;
- provenance;
- rights status;
- known continuity contradictions;
- epistemic leaks;
- source identity/hash mismatch;
- severe technical errors;
- severe source-copy leakage.

Use scored/soft gates for:

- voice;
- monotony;
- Life plausibility;
- pedagogical value;
- recurrence density;
- source contribution.

---

## 11. Corpus pruning

Canonical releases are immutable, but later releases may supersede records.

Prune from future compilations when material is:

- technically wrong;
- redundant;
- source-ineligible;
- overly copied;
- stylistically damaging;
- chronologically implausible;
- pedagogically low-value;
- shown experimentally to cause pathological overconcentration.

Never silently delete from historical manifests. Record exclusions/migrations explicitly.
