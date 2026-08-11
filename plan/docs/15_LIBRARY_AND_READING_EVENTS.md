# 15 — Library and Reading Events

## 1. Purpose

The TL100 narrator should not learn everything from generated prose.

A real technical life contains encounters with recorded human knowledge: books, textbooks, manuals, datasheets, papers, essays, literature, standards, code, documentation, notebooks, diagrams, and other artifacts.

TL100 treats these encounters as **first-class events in the canonical life**.

The central rule is:

> **No external source enters the training stream merely because it is “good data.” It enters because the Life has a reason, time, and context for encountering it.**

---

## 2. Why readings matter

Readings serve several distinct purposes:

1. **Technical authority** — provide accurate knowledge beyond generator-model latent memory.
2. **Linguistic breadth** — expose the model to human-authored styles outside the canonical narrator voice.
3. **Conceptual compression** — textbooks can present dense, structured knowledge efficiently.
4. **Alternative viewpoints** — multiple authors can frame the same topic differently.
5. **Long-form coherence** — complete chapters/works provide structure that isolated snippets lack.
6. **Epistemic training** — the narrator can distinguish what was observed, read, told, or inferred.
7. **Cultural/conversational breadth** — literature and essays can broaden language, interpersonal inference, metaphor, humor, and ambiguity.
8. **Causal integration** — a source can be sought because a project exposes a knowledge gap, then applied and remembered later.

---

## 3. Source classes

Every external source has a `source_type`.

Suggested classes:

- `textbook`
- `technical_book`
- `manual`
- `datasheet`
- `standard_or_specification`
- `research_paper`
- `technical_article`
- `documentation`
- `code_repository_or_excerpt`
- `essay`
- `literature`
- `reference_work`
- `course_material`
- `historical_primary_source`
- `other`

Source type does not determine quality. Selection criteria do.

---

## 4. Source roles

A source can have one or both roles:

### `grounding_only`

Used backstage to verify/generate Life-native prose. Its text is not included in training exports.

### `explicit_reading`

A selected portion or full work is intentionally included as part of the narrator's encountered material.

A source may begin as grounding-only and later be approved for explicit reading.

---

## 5. Reading-event lifecycle

A reading event should normally follow this conceptual sequence:

```text
life problem / curiosity / recommendation
                |
                v
         source selection
                |
                v
      knowledge-state snapshot
                |
                v
          reading begins
                |
                v
       source text encountered
                |
      +---------+---------+
      |                   |
      v                   v
understood             misunderstood/
partially               unresolved
      |                   |
      +---------+---------+
                v
       reflection / notes
                |
                v
       application / test
                |
                v
       later callback / transfer
```

Not every reading needs all stages immediately. Some may remain unresolved for months or years.

---

## 6. Reading-event record

A reading event should include:

```yaml
reading_event_id: read_00000217
source_id: source_0047
segment_ids:
  - seg_ch07_feedback
  - seg_ch08_stability

trigger:
  episode_id: ep_00018341
  reason: amplifier oscillation

knowledge_before:
  knows:
    - concept_gain
    - concept_basic_feedback
  uncertain:
    - concept_phase
  does_not_know:
    - concept_stability_margin

intended_roles:
  - first_exposure
  - vocabulary_acquisition
  - problem_resolution

expected_effects:
  - introduce phase-dependent feedback
  - weaken naive "negative feedback always stabilizes" belief
  - seed later control-system transfer

reflection_episode_ids:
  - ep_00018342

application_episode_ids:
  - ep_00018347

later_callbacks:
  - project_motor_controller_02
  - project_heater_control_01
  - project_robot_steering_01
```

This is design metadata. It need not appear in training prose.

---

## 7. Source selection criteria

A source is selected because it contributes something the corpus needs.

Evaluate:

### Technical correctness / authority

- Is it authoritative enough for its intended role?
- Is the version/date appropriate?
- Are known limitations recorded?

### Pedagogical fit

- Does it meet the narrator at the right prerequisite level?
- Is the source unusually clear, rigorous, visual, practical, or historically important?
- Does it complement rather than merely duplicate existing material?

### Linguistic value

- Does it add genuinely different human language or structure?
- Does it avoid overconcentrating one author/style/publisher?

### Life relevance

- Why does Alex encounter it *now*?
- What question, project, recommendation, interest, or need triggers it?

### Recurrence value

- Will ideas from it be used later?
- Does it create vocabulary, analogies, disagreements, or memories worth carrying forward?

### Rights/provenance

- Can the project store it?
- Can it redistribute it?
- Can it include it in the intended training experiment under the project's legal/rights policy?
- Is a metadata-only reference required instead?

Sources failing provenance/rights requirements must not enter compiled training data.

---

## 8. Preserve source integrity

When an external work is included as an explicit reading, default to preserving its actual authorship rather than rewriting it into Alex's voice.

Possible inclusion units:

- entire short work;
- full chapter;
- coherent section;
- contiguous selected pages/paragraphs;
- code/documentation segment;
- complete manual section.

Avoid arbitrary sentence-level chopping solely to hit token quotas.

A source's internal order should be preserved unless an experiment explicitly studies fragmentation.

---

## 9. The narrator does not need to “explain the lesson” after every reading

Over-pedagogizing the Life would destroy its realism and narrow the data.

Allowed outcomes include:

- immediate application;
- brief note;
- confusion;
- disagreement;
- no explicit reaction;
- abandoned reading;
- return to the same book later;
- later spontaneous use;
- changed vocabulary without conscious commentary;
- enjoyment with no technical purpose.

The corpus should contain both **instrumental reading** and **ordinary reading**.

---

## 10. Literature and nontechnical reading

Literature can be useful even in a technically focused Life.

Potential contributions:

- dialogue;
- character reasoning;
- ambiguity;
- long-range causality;
- description;
- humor;
- metaphor;
- emotional vocabulary;
- nontechnical human situations;
- stylistic diversity.

Do not force literature to become a technical lesson.

Selection should remain bounded because TL100's model capacity is limited. A small number of carefully selected works encountered naturally is preferable to a random general-literature dump.

---

## 11. Source diversity without source chaos

The external library should be broader than the Life voice but still curated.

Track distributions by:

- author;
- era;
- source type;
- domain;
- reading difficulty;
- prose style;
- publisher/organization;
- geographic/cultural origin where relevant;
- technical vs nontechnical;
- theoretical vs practical;
- primary vs secondary source.

The goal is not quota-driven demographic balancing for its own sake. The goal is to detect accidental monoculture.

---

## 12. Rights and repository policy

Every source record must have explicit fields such as:

- `rights_status`
- `redistribution_status`
- `training_use_status`
- `storage_mode`
- `license_identifier`
- `rights_notes`

Suggested storage modes:

- `repo_fulltext` — permitted to store and redistribute in the project;
- `local_fulltext` — available to the experiment but not committed publicly;
- `metadata_only` — registry metadata and hashes/identifiers only;
- `grounding_excerpt_only` — limited internal substrate where permitted;
- `blocked` — not eligible.

Do not infer legal permission from public accessibility.

This project design is not legal advice. Before using non-redistributable or copyrighted works for training, the project should establish an explicit rights/legal policy applicable to the actual jurisdiction and use case.

---

## 13. Source segment identity

Every includable segment should have a stable ID and content hash.

Example:

```yaml
source_id: source_0047
segment_id: seg_0047_ch07
sequence_in_source: 7
start_locator: chapter_7_start
end_locator: chapter_7_end
content_hash: sha256:...
approx_tokens: 6842
```

This allows experiments to use the exact same source text under different ordering/context conditions.

---

## 14. Reading recurrence

A source can recur.

Examples:

- Alex reads a beginner chapter, returns to advanced chapters years later;
- a manual is consulted repeatedly during maintenance;
- a novel is reread much later;
- a paper first seems opaque, then becomes understandable after prerequisites accumulate;
- a datasheet becomes a familiar working reference.

Track both **first encounter** and **subsequent rereading/reference**.

---

## 15. Reading failure modes

Reject or revise patterns such as:

- source inserted because “the curriculum needs 5k more tokens”;
- Alex reads advanced material before plausible prerequisites;
- every source perfectly answers the current problem;
- every reading is followed by a synthetic five-point summary;
- source voice leaks into later Life prose wholesale;
- Life prose reproduces large phrases from source unintentionally;
- repeated sources dominate lexical distribution;
- reading becomes a hidden textbook dump;
- characters recommend sources only to advance the curriculum;
- external text contradicts world/technical facts without the contradiction being modeled.

---

## 16. Pilot source strategy

For the 50k–250k pilot:

- use a **small source library**, perhaps 10–30 sources;
- favor short, inspectable, rights-clear/open/public-domain/locally approved material;
- include only a handful of explicit readings;
- use more sources backstage than in training;
- manually inspect every explicit source inclusion and surrounding Life context;
- test whether human-authored material feels like an experience rather than an interruption.

Do not optimize source volume yet.

---

## 17. Open research question

TL100 does **not** assume that a particular percentage of human-authored data is optimal.

The project should instead ask:

> **How much external human-written experience does a highly structured synthetic life need, and does contextual placement change what a small model learns from it?**

That question belongs in the experiment design, not in an untested corpus rule.
