# 05 — Episode and Encounter Specification (v2)

## 1. Episode definition

An **episode** is the smallest canonical unit of narrator-authored Life material that:

- has a coherent local purpose/event;
- can update world or knowledge state;
- can be reviewed independently;
- occupies one exact place in chronology.

An episode is **not** the only kind of canonical timeline item. External source segments and technical artifacts can also be encountered through `reading_event` / `stream_item` records.

Episodes are not necessarily training chunks. Exporters may concatenate or split material while retaining source boundaries in manifests.

## 2. Recommended length

Suggested starting distribution for narrator episodes:

- short: 250–700 tokens;
- typical: 700–1,800;
- long: 1,800–4,000;
- exceptional: up to ~8,000.

External reading units follow their natural coherent boundaries rather than these episode lengths.

## 3. Episode classes

- `scene`
- `project_work`
- `conversation`
- `lesson`
- `experiment`
- `debugging`
- `reflection`
- `postmortem`
- `planning`
- `documentation`
- `reading_preparation`
- `reading_response`
- `practice`
- `assessment`
- `transition`
- `mixed`

A prior `reading_and_response` class is split so the external source itself can exist independently from Alex's response.

## 4. Required episode-plan fields

Before prose exists, specify at minimum:

```yaml
episode_id: ep_00001234
era_id: era_2
date_index: 213
episode_class: debugging
location_ids: [place_foundry]
people_present: [person_narrator, person_mara]
project_ids: [project_motor_controller_01]
concept_targets: [concept_stall_current, concept_supply_droop]
concept_prerequisites: [concept_voltage, concept_current]
acquisition_modes: [experience, experiment, artifact, reading]
memory_callbacks: [memory_cart_alignment_01]
open_questions_before: [question_motor_driver_reset_01]
objective: >
  Discover that motor startup/stall current and supply droop explain the reset.
narrator_belief_before: >
  I think the controller reset is probably a firmware timing problem.
planned_evidence:
  - observe reset at motor start
  - measure supply rail under load
triggered_reading_event_ids:
  - read_00000217
source_ids:
  - source_motor_datasheet_01
state_changes_expected:
  - misconception_motor_reset_software corrected
  - question_motor_driver_reset_01 resolved
```

The writer must not invent the curriculum/world/source structure while composing prose.

## 5. Canonical record types

TL100 v2 uses separate records:

- `episode` — narrator-authored prose;
- `source` — external source metadata and segments;
- `reading_event` — why/when/how a source is encountered;
- `stream_item` — exact canonical timeline placement;
- `artifact` — optional structured document/code/log record.

See `schemas/`.

## 6. Educational event types

Annotate meaningful learning events:

- `first_exposure`
- `term_introduction`
- `intuitive_use`
- `formalization`
- `practice`
- `misconception`
- `correction`
- `source_encounter`
- `source_reconciliation`
- `explanation_to_other`
- `transfer`
- `integration`
- `assessment`
- `spaced_recall`
- `rereading`

## 7. Acquisition provenance

For important concept changes, record one or more acquisition modes:

- `experience`
- `conversation`
- `reading`
- `artifact`
- `experiment`
- `inference`
- `teaching`

This enables later tests of whether source type or learning context matters.

## 8. Mistakes

Mistakes must be plausible, consequential enough to matter, and consistent with current knowledge.

Good examples:

- wrong subsystem blamed first;
- unit/reference-frame error;
- misunderstanding a source;
- overgeneralizing a textbook rule;
- trusting unloaded voltage;
- ignoring a requirement;
- overfitting an ML model;
- using retrieval without authority filtering.

Bad examples:

- absurd errors inserted only to manufacture a correction;
- dangerous negligence treated casually;
- characters hiding obvious facts to prolong a lesson;
- repetitive scripted mistakes.

## 9. Completion criteria

An episode can enter canon only if:

- schema valid;
- plan approved;
- world preconditions valid;
- knowledge state valid;
- curriculum prerequisites valid or intentionally previewed;
- triggered source/read events exist and are rights/provenance valid;
- technical claims pass verification;
- narrator perspective and voice pass;
- duplication/copying checks pass;
- state mutations are explicit;
- provenance complete.

A source segment can enter a training export only if its source record, selected segment, reading/encounter placement, and rights/training-use status all permit inclusion.

## 10. Training boundaries

Canonical metadata is not automatically training text.

Exporters may experiment with:

- episode separators;
- source/work boundary markers;
- natural chapter headings;
- no explicit metadata;
- reading boundaries that are metadata-only;
- selected natural notebook/date headings when genuinely part of the Life.

The flagship corpus should feel like encountered text, not serialized JSON.
