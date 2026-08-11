# 11 — World V0 and Narrator

> **Status: concrete proposal for review, not yet immutable canon.**

This document makes the abstract project actionable. It deliberately chooses a world, narrator, cast, and recurring physical substrate so implementation agents do not invent them independently.

---

## 1. Narrator

**Canonical ID:** `person_narrator`  
**Working name:** Alex  
**Starting age:** 15  
**Language:** fluent ordinary English at corpus start  
**Starting technical state:** curious and practically inexperienced; comfortable with ordinary arithmetic, reading, everyday tools, and basic school science, but without formal engineering competence  
**Long-term trajectory:** curious maker -> competent technician/builder -> software/systems engineer -> experimentalist -> machine-learning practitioner -> person capable of designing and explaining AI systems

Alex is a human narrator. LIFE100 does not begin at birth and does not attempt to learn basic English from infant-like input. The "life" begins once ordinary language is already established and concentrates on the formation of technical, conversational, experimental, and systems competence.

The life may eventually span roughly 15–25 fictional years. Exact duration is less important than causal learning order.

---

## 2. Narrator stable traits

At start:
- curious but not precociously expert;
- likes understanding why a thing failed;
- sometimes begins building before defining the problem;
- dislikes pretending to know;
- more comfortable with concrete objects than abstractions;
- remembers mistakes strongly;
- enjoys explaining something once it has become clear;
- can be impatient with vague language but initially uses vague language themselves;
- learns to measure before guessing.

Traits that should emerge rather than exist immediately:
- requirements-first thinking;
- explicit uncertainty;
- systems decomposition;
- preference for observable state;
- deterministic boundaries around probabilistic systems;
- careful distinction between evidence and inference;
- concise technical explanation.

Those later habits should be traceable to events.

---

## 3. World setting

**Place:** Rookfield, a fictional medium-sized contemporary town in an English-speaking country.

Why fictional:
- world geography can remain perfectly consistent;
- no unnecessary geopolitical/factual burden;
- technical facts can still be grounded in real physics, engineering, software, and documentation;
- recurring businesses and institutions can evolve without contradicting real-world history.

Technology level:
- contemporary;
- ordinary internet and smartphones exist;
- microcontrollers, PCs, 3D printers, machine tools, cloud services, modern ML tooling, and GPUs become accessible when appropriate;
- no speculative technology.

The world obeys ordinary real physics.

---

## 4. Anchor places

### `place_home`
Alex's family home. Ordinary kitchen, small storage cupboard, bedroom desk. Early measurements and repairs happen here.

### `place_home_garage`
A cramped garage/work area with old hand tools, timber offcuts, bicycle parts, a vice, a basic drill, and shelves that are never as organized as Alex thinks they are.

### `place_school_lab`
School science/technology laboratory. Basic balances, meters, power supplies, mechanics apparatus, computers.

### `place_foundry`
"The Foundry", a community makerspace introduced early. Workbenches, soldering stations, drill press, small lathe/mill access under supervision, 3D printers, components drawers, test equipment.

### `place_electra_shop`
Small local electronics/component shop. Useful because purchases create constraints, conversations, substitutions, and mistaken assumptions.

### `place_riverside`
Footpath and open area used for bicycle, cart, robot, radio/sensor, weather, and movement tests.

### `place_station_cafe`
Recurring social/conversation location. Not everything technical happens at a bench.

### `place_rookfield_library`
Public library with ordinary fiction/nonfiction, technical books, quiet work tables, and later inter-library/digital access. It gives reading a physical/social place in the Life rather than making all knowledge arrive through an abstract internet. Alex's use of it changes over time.

### `place_north_yard`
Small fabrication/repair business where Alex later gets practical exposure to machining, tolerances, maintenance, and customer constraints.

### `place_vector_lab`
Later small engineering/software company or project lab. Introduced only after sufficient development. Becomes setting for systems, software, instrumentation, ML, deployment, and team work.

### `place_flat_workbench`
Alex's later home workbench/apartment setup. Recurring private experimental space in later eras.

---

## 5. Anchor cast

The cast should accumulate history rather than serve as exposition devices.

### `person_mara` — Mara Chen
Introduced at The Foundry. Electronics mentor, initially in her late 20s/early 30s. Patient but not indulgent. Often asks what was actually measured. Does not always know the answer. Later becomes a peer/friend rather than permanent teacher.

Conceptual roles:
- measurement;
- electronics;
- instrumentation;
- experimental discipline.

### `person_ben` — Ben Hale
Same-age friend. Practical, fast, likes getting a thing moving. Sometimes finds Alex overanalytical; sometimes catches Alex building unnecessary complexity.

Conceptual roles:
- collaboration;
- tradeoffs;
- physical projects;
- disagreement without hierarchy;
- "works in the real world" pressure.

### `person_imani` — Dr. Imani Okafor
School physics/technology teacher. Introduces careful experiments and the difference between a plausible story and evidence.

Conceptual roles:
- hypotheses;
- measurement;
- uncertainty;
- scientific reasoning.

### `person_tomas` — Tomas Varga
Fabricator at North Yard. Strong practical knowledge of fit, tolerance, materials, maintenance, and what drawings omit.

Conceptual roles:
- manufacturing;
- tolerances;
- physical constraints;
- failure from details.

### `person_leila` — Leila Morgan
Introduced through coding/makerspace work. Similar age, stronger at software earlier than Alex. Thinks naturally in explicit state and interfaces.

Conceptual roles:
- programming;
- debugging;
- version control;
- software architecture;
- later collaborative systems work.

### `person_priya` — Priya Rao
Later systems/control engineer at Vector Lab. Strong at requirements, interfaces, testability, and control systems.

Conceptual roles:
- systems engineering;
- control;
- observability;
- deployment judgment.

### `person_hana` — Hana Lewis
Later trainer/technical communicator/customer-facing colleague. Pushes Alex to explain without hiding behind jargon and to identify what another person actually needs.

Conceptual roles:
- teaching;
- conversation;
- requirements discovery;
- communication.

The first 100 episodes should mostly use Alex, Ben, Mara, Dr. Imani, and family references. Later characters should not be forced in early.

---

## 6. Anchor machines and objects — first set

These should persist and accumulate history.

1. `tool_tape_measure_01`
2. `tool_square_01`
3. `tool_hand_saw_01`
4. `tool_drill_01`
5. `tool_vice_01`
6. `tool_calipers_01`
7. `machine_bicycle_01`
8. `project_object_cart_01`
9. `instrument_multimeter_01`
10. `instrument_bench_supply_01`
11. `tool_soldering_iron_01`
12. `machine_dc_motor_01`
13. `machine_motor_driver_01`
14. `instrument_oscilloscope_01`
15. `board_microcontroller_01`
16. `sensor_temperature_01`
17. `sensor_light_01`
18. `sensor_pressure_01`
19. `machine_small_fan_01`
20. `computer_laptop_01`
21. `printer_3d_01`
22. `machine_drill_press_01`
23. `instrument_scale_01`
24. `machine_pump_01`
25. `robot_rover_01`

Later world design can extend toward ~50 anchor objects before v0.

---

## 7. First long-running memories

### Cart pulls left
An early cart veers because of mechanical alignment. Alex initially blames unequal motors/friction without measuring geometry well enough. This becomes a long-term systems/debugging memory.

### The 6 mm mistake
Alex measures from the wrong reference face and makes a part that is consistently wrong despite precise measurements. This introduces the idea that precision cannot rescue a wrong definition.

### Current-limit surprise
A motor collapses a supply rail or triggers current limiting. Alex is focused on nominal voltage and learns that load behavior matters.

### "What did you actually observe?"
Mara challenges a confident causal story that Alex has not measured. The phrase should not become a catchphrase, but the habit recurs.

### Working-but-wrong
A project appears to function but violates a requirement or only works under a narrow condition. Later becomes useful for evaluation/AI thinking.

---

## 8. Reading and library reality

Alex already knows how to read at corpus start, but does **not** begin with a preloaded technical canon. Reading habits develop with the Life.

Early pattern:
- short practical instructions;
- school materials;
- ordinary fiction/nonfiction;
- component labels/manuals;
- books recommended by people Alex trusts.

Later pattern:
- textbooks;
- technical books;
- datasheets/manuals;
- documentation/code;
- papers and standards/specifications;
- selected literature/essays unrelated to immediate projects.

Stable preference should emerge for reading with a question in mind, but Alex should also sometimes read without instrumental purpose. Not every book becomes a lesson.

Source encounters must be tracked in the library/read-event ledger.

---

## 9. Social reality

The narrator should have:
- meals;
- travel across town;
- waiting;
- frustration;
- jokes;
- disagreement;
- mundane errands;
- occasional nontechnical interests;
- changing relationships;
- school/work obligations.

However, LIFE100 is a curated technical life, not a full social novel. Ordinary content exists to make experiences credible and broaden language, not to dominate the corpus.

No person should exist only to teach Alex.

---

## 10. Prose reality

The canonical prose is written retrospectively close to the event: Alex can express a coherent scene but cannot use knowledge from years later unless explicitly framing it as later reflection.

Default tense can vary naturally:
- past tense for lived scenes;
- present tense for explanations/general principles;
- future/modal for plans;
- dialogue in natural tense.

The first-person epistemic boundary remains the governing rule.

---

## 11. Why this world fits the experiment

The same finite environment can support increasing abstraction:

garage alignment problem
-> measurement
-> tolerances
-> electrical diagnostics
-> sensor state
-> software debugging
-> control systems
-> observability
-> ML evaluation
-> AI deployment boundaries

The world therefore provides **conceptual recurrence without artificial repetition**.
