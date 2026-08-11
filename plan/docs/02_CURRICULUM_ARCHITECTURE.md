# 02 — Curriculum Architecture

## 1. Purpose

The life must teach deliberately.

The curriculum is a **dependency graph embedded into experience**, not a chapter list pasted onto fiction.

Every important concept should have:
1. prerequisites;
2. one or more **acquisition modes** (experience, conversation, reading, artifact, experiment, inference, teaching);
3. first exposure;
4. intuitive use;
5. explicit naming/definition;
6. deliberate practice;
7. mistake or boundary case;
8. later transfer to a different context;
9. occasional spaced recurrence.

The curriculum graph should not specify only *what* is learned. It should specify **how knowledge enters the Life and why that acquisition mode is useful**.

---

## 2. Learning progression

### Era 0 — Orientation and ordinary causality
Target concepts:
- objects and properties;
- location and direction;
- before/after;
- amount;
- comparison;
- simple counting;
- cause/effect;
- prediction;
- observation vs assumption;
- ordinary conversational turn-taking.

Experience examples:
- sorting objects;
- measuring a shelf;
- noticing a door sticks in damp weather;
- following and correcting simple instructions;
- describing why an attempt failed.

This era establishes linguistic and causal foundations without technical jargon overload.

### Era 1 — Measurement and making
Target concepts:
- units;
- length/mass/time/temperature;
- accuracy and precision intuitively;
- estimation;
- tools;
- fasteners;
- materials;
- force;
- friction;
- leverage;
- energy;
- tolerances;
- safety habits.

Projects:
- repair a loose mechanism;
- build a simple cart;
- construct shelves or enclosure;
- compare materials;
- measure repeatability.

### Era 2 — Electricity and instrumentation
Target concepts:
- voltage;
- current;
- resistance;
- Ohm's law;
- power;
- series/parallel;
- continuity;
- measurement loading;
- analog signals;
- sensors;
- actuators;
- motors;
- power supplies;
- signal/noise.

Projects:
- battery lamp;
- motor controller;
- temperature logger;
- sensor fault diagnosis;
- bench instrument use.

### Era 3 — Software and formal state
Target concepts:
- variables;
- state;
- control flow;
- functions;
- abstraction;
- data representation;
- files;
- parsing;
- errors/exceptions;
- debugging;
- tests;
- version control.

Projects:
- logger software;
- simple simulator;
- instrument serial interface;
- configuration file;
- small web interface.

The prose should connect software abstractions back to physical experiences already lived.

### Era 4 — Systems, interfaces, and control
Target concepts:
- subsystem boundaries;
- interfaces;
- requirements;
- feedback;
- reference/setpoint;
- error;
- stability intuition;
- state estimation;
- observability;
- failure modes;
- redundancy;
- latency;
- throughput;
- queues;
- networks;
- APIs;
- databases.

Projects:
- closed-loop temperature controller;
- small robot;
- networked sensor station;
- multi-component automation system.

### Era 5 — Experimental reasoning
This is threaded earlier but becomes explicit here.

Target concepts:
- hypothesis;
- alternative explanation;
- control;
- confounder;
- measurement uncertainty;
- repeatability;
- calibration;
- validation;
- correlation vs causation;
- evidence quality;
- belief updating.

Projects:
- diagnose intermittent fault;
- compare two control strategies;
- characterize a sensor;
- investigate performance regression.

### Era 6 — Machine learning foundations
Target concepts:
- data points;
- labels;
- features;
- training;
- validation;
- test;
- loss;
- gradient intuition;
- overfitting;
- generalization;
- representation;
- class imbalance;
- precision/recall intuition.

Projects:
- simple classifier;
- anomaly detector;
- regression from sensor data;
- evaluate failure cases.

### Era 7 — Language models
Target concepts:
- tokenizer;
- token IDs;
- embeddings;
- transformer;
- attention;
- Q/K/V;
- MLP;
- residual stream;
- positional information;
- logits;
- softmax;
- autoregressive generation;
- pretraining;
- inference;
- prefill/decode;
- KV cache;
- sampling;
- parameter count;
- quantization;
- fine-tuning;
- LoRA;
- distillation;
- retrieval;
- RAG;
- tool use;
- evaluation.

Projects:
- implement tiny tokenizer;
- build tiny transformer;
- train small text model;
- inspect attention;
- add retrieval;
- expose tool call;
- build evaluation harness.

This is deliberately meta: the life eventually learns enough to build a small language model much as the LIFE100 project itself does.

### Era 8 — Technical judgment and deployment
Target concepts:
- requirements discovery;
- when not to use AI;
- deterministic/probabilistic boundaries;
- privacy;
- data residency;
- permissions;
- observability;
- acceptance criteria;
- staged deployment;
- cost per task;
- human-in-the-loop design;
- safety and failure containment.

Projects:
- customer-like case studies;
- instrument support system;
- document workflow;
- automation assistant;
- embodied sensor/robot assistant.

---

## 3. Conversation curriculum

Conversation is not merely prose decoration.

The narrator should learn to:
- answer directly;
- ask clarifying questions when ambiguity matters;
- not ask unnecessary questions;
- distinguish fact from inference;
- say "I don't know";
- acknowledge corrections;
- disagree without hostility;
- explain at multiple levels;
- infer a listener's knowledge from context;
- teach with examples;
- summarize decisions;
- negotiate constraints;
- maintain shared context;
- refer back to prior conversations accurately.

These behaviors should emerge in interactions across the life, not appear only in "communication lessons."

---

## 4. Curriculum graph representation

Each concept record should include:

```yaml
id: concept.feedback_control
name: feedback control
prerequisites:
  - concept.measurement
  - concept.target_value
  - concept.error_difference
  - concept.cause_effect
first_exposure: null
first_named: null
first_independent_use: null
misconceptions: []
transfer_targets:
  - temperature control
  - motor speed
  - robot steering
mastery_events_required:
  intuitive_use: 2
  explicit_explanation: 1
  debugging_use: 1
  transfer_use: 2
```

---

## 5. Concept recurrence rule

Do not teach a major concept once.

A useful default ladder:
1. **Encounter** — see phenomenon before terminology.
2. **Name** — learn word and rough meaning.
3. **Use** — solve a simple problem.
4. **Fail** — misuse or meet a boundary case.
5. **Refine** — improve mental model.
6. **Explain** — teach or articulate it.
7. **Transfer** — recognize same structure elsewhere.
8. **Integrate** — use as one component of a larger system.

Spacing should span meaningful narrative time.

---

## 6. Tutorial density

Not every episode should be a tutorial.

Initial target across accepted tokens:
- 20–30% direct technical learning/explanation;
- 25–35% practical projects/actions;
- 10–20% debugging, mistakes, postmortems;
- 10–20% conversation/collaboration;
- 5–15% reflection/memory;
- 5–15% ordinary connective life/world texture.

These ranges overlap because an episode can carry multiple labels.

The corpus should be measured and adjusted based on observed distributions.

---

## 7. Mathematical depth

Mathematics should be sufficient to support technical understanding.

The narrator should encounter:
- arithmetic;
- ratios;
- units/dimensional reasoning;
- algebra;
- graphs;
- vectors;
- probability intuitively then formally enough for ML;
- matrices;
- derivatives as rates/sensitivities;
- gradient intuition;
- selected formulas where they clarify mechanisms.

Avoid making the life a mathematics textbook. Mathematics should repeatedly solve concrete problems.

---

## 8. Coverage versus coherence

Before adding a topic ask:
1. Does it have prerequisites already present?
2. Does it naturally support an existing project or relationship?
3. Will it recur later?
4. Does it contribute to the target technical worldview?
5. Is the corpus already underexposed to a more fundamental concept?

A small model benefits from repeated structural depth more than decorative topic breadth.

---

## 9. Initial curriculum deliverable

Before generating the 1M-token v0 corpus, create:
- 300–600 concept nodes;
- explicit dependency edges;
- 30–60 anchor projects;
- 100–200 planned transfer links;
- 50+ planned misconception/error patterns;
- a vocabulary introduction plan for high-value technical terms.

Only the first portion needs full detail for the pilot, but the broader graph prevents early episodes from painting the world into a corner.
## 10. Acquisition-mode design

A concept may be acquired through multiple channels:

- `experience` — encountered physically or socially;
- `conversation` — another person explains, challenges, or recommends;
- `reading` — external human-authored source;
- `artifact` — datasheet, code, log, specification, diagram, manual;
- `experiment` — deliberately produced evidence;
- `inference` — narrator connects prior knowledge;
- `teaching` — understanding deepens while explaining to another person.

Do not force every concept through every mode. Instead choose combinations that create complementary representations.

Example — `concept_stall_current`:

1. motor behaves unexpectedly under load (`experience`);
2. Mara asks Alex to predict the current (`conversation`);
3. multimeter/bench supply provides evidence (`experiment`);
4. motor datasheet gives rated stall current (`artifact/reading`);
5. Alex applies the idea to driver selection (`practice`);
6. years later, the same pattern informs power-budget reasoning (`transfer`).

## 11. Reading curriculum

The curriculum should maintain a **reading map** in parallel with the concept graph. A source can:

- introduce vocabulary;
- formalize an already-lived intuition;
- provide a competing explanation;
- deepen a concept;
- expose the narrator to a new style/register;
- create a productive unresolved question;
- support later project work;
- broaden ordinary language through literature/nontechnical reading.

A reading is not justified merely because it covers the next syllabus item. It should have a plausible Life trigger and prerequisite fit.

See `15_LIBRARY_AND_READING_EVENTS.md`.

