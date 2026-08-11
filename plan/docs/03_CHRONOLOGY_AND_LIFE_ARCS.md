# 03 — Chronology and Life Arcs

## 1. Purpose

Chronology is not decorative metadata. It is the mechanism through which knowledge, relationships, preferences, and memories gain causality.

The corpus must answer:
> Why does the narrator know this *now*?

and:
> What earlier experience made this later thought possible?

---

## 2. Time model

Use **eras** for broad curriculum stages, **seasons/periods** for medium structure, and **episode ordinals** for exact canonical order.

Avoid literal biological-age simulation unless the world design later chooses it. The narrator's "life" can begin as a technically naive but linguistically functional person. This avoids spending millions of tokens simulating infant language acquisition unless that itself becomes an experiment.

Recommended starting assumption:

> The narrator begins with ordinary language and everyday world knowledge, but minimal formal technical knowledge, then develops through sustained making, study, work, and collaboration.

This keeps the experiment focused on coherent technical/cognitive development.

---

## 3. Arc classes

### Project arcs
A goal unfolds across multiple episodes:
- idea;
- requirements;
- design;
- build;
- failure;
- diagnosis;
- iteration;
- completion;
- retrospective;
- later reuse.

### Relationship arcs
Recurring people change the narrator's experience:
- meeting;
- trust;
- disagreement;
- collaboration;
- teaching in both directions;
- shared references;
- changed roles.

### Concept arcs
A concept progresses from observation to mastery.

### Mystery/problem arcs
A question remains unresolved:
- anomaly;
- initial hypotheses;
- partial tests;
- dormant period;
- new clue;
- resolution.

### Preference arcs
A stable design or conversational preference emerges through repeated consequences.

### Tool/machine arcs
A physical object changes:
- acquisition;
- first use;
- misuse;
- maintenance;
- modification;
- failure;
- replacement or continued familiarity.

### Reading/source arcs
A source can have a history rather than a single insertion:
- recommendation/discovery;
- reason for reading;
- first attempt;
- partial comprehension;
- note/question;
- application;
- disagreement with evidence or another person;
- return/rereading;
- later transfer or semanticized memory.

A book or manual can therefore recur like a machine or person.

---

## 4. Recurrence budget

A coherent life requires deliberate recurrence.

For each major anchor entity, plan a recurrence profile.

Example:

```yaml
machine: bench_supply_01
introduced: era_2
recurrence:
  era_2: high
  era_3: medium
  era_4: medium
  era_5: low
callbacks:
  - first_current_limit_mistake
  - motor_driver_debug
  - sensor_noise_test
state_changes:
  - fuse_replaced
  - output_knob_marks_added
```

Not every object needs this. Disposable objects should remain disposable.

---

## 5. Memory design

Later episodes should refer to earlier experiences naturally.

There are several memory types:
- **episodic:** "I remembered the cart pulling left..."
- **semanticized:** earlier event becomes a general principle;
- **procedural:** narrator now does something without re-explaining it;
- **social:** shared joke or remembered conversation;
- **error memory:** narrator recognizes a pattern that previously caused failure;
- **false/partial memory:** permitted only if explicitly designed and later reconciled.

Avoid excessive explicit "I remembered..." callbacks. Mature knowledge often appears simply as changed behavior.

---

## 6. Knowledge latency

Do not resolve everything immediately.

A realistic educational rhythm includes:
- questions answered in the same episode;
- questions answered after several episodes;
- questions that remain open for an era;
- questions revised rather than cleanly solved.

A backlog of unresolved questions should be part of the state ledger.

---

## 7. Example multi-era recurrence

### Early
The narrator builds a small cart. It veers left. They initially suspect the motor.

### Later
They learn alignment, friction, and measurement, discovering the axle geometry was responsible.

### Later
They encounter electrical losses and use the old cart as an analogy: energy can disappear into mechanisms one failed to model.

### Later
They debug a robot and avoid blaming software prematurely because the cart taught them to inspect mechanics.

### Much later
They discuss AI system failures and reflect on the same general habit: avoid collapsing a system-level symptom into the most fashionable subsystem.

This is the desired density: one experience contributes to multiple later concepts without copy-pasting the same lesson.

---

## 8. Life arc planning horizon

Before pilot generation:
- fully outline first ~100 episodes;
- outline next ~500 at medium resolution;
- maintain long-range anchor arcs for the first several eras.

Before 25M tokens:
- macro-plan the complete life/curriculum;
- avoid exact scripting of every episode;
- preserve room for discoveries from generated material.

The world can grow, but growth must be deliberate and registered.

---

## 9. Episode adjacency

Canonical neighboring episodes should usually have some relationship:
- continuation;
- consequence;
- time transition;
- thematic bridge;
- project alternation;
- social return.

Avoid a dataset that is technically chronological but feels like randomly ordered essays with dates attached.

---

## 10. Training chronology

Canonical chronology and model-training curriculum are related but not identical.

Potential schedule:
1. train on Era 0;
2. introduce Era 1 while replaying a sample of Era 0;
3. introduce Era 2 with spaced replay of earlier anchors;
4. continue progressively.

A control run shuffles the same episodes across the same total token exposures.

This should be implemented as export manifests so training experiments remain reproducible.
## 11. Canonical stream items

Chronology is now defined over **stream items**, not episodes alone. The timeline may interleave:

- narrator-authored episodes;
- reading-event boundaries;
- source segments;
- technical artifacts;
- reflection/application episodes;
- transitions.

Example:

```text
ep_0041  motor fails under load
read_start_001  Alex seeks the motor datasheet
source_segment  motor datasheet: electrical characteristics
read_end_001
ep_0042  Alex compares stall current to the supply
...
ep_0158  same idea transfers to a pump startup problem
```

The source text can be stored outside the public repository; its canonical placement is represented by immutable IDs/hashes and manifests.

## 12. Reading placement rule

A reading should normally answer at least one of:

- What prompted it?
- Why this source?
- Why now?
- What did Alex already know?
- What changed afterward?

Not every reading needs an immediate explicit reflection, but unexplained source insertion is not valid Life chronology.

