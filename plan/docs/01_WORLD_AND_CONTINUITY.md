# 01 — World and Continuity Specification

## 1. Purpose

The LIFE100 world must be coherent enough that recurring experience has meaning.

The world bible is not merely lore. It is an **input constraint on generation** and a machine-readable consistency system.

The world should be rich enough to support years of learning but small enough that a 100M-parameter model can repeatedly encounter the same structures.

---

## 2. Design principle: bounded richness

Do not create a globe-sized fictional universe.

Prefer a compact recurring geography such as:
- one home and neighborhood;
- one workshop/makerspace;
- one technical school/lab;
- a small number of local businesses and workplaces;
- several recurring outdoor/test locations;
- a few later travel locations introduced when curriculum requires them.

Likewise, prefer a stable cast of perhaps 15–40 meaningfully recurring people over hundreds of disposable names.

Objects and machines should recur. A multimeter first used for a battery can later diagnose a motor driver. A bench supply can appear across years. A badly aligned cart can become a remembered analogy for losses.

---

## 3. Canonical entity classes

Every persistent entity belongs to a ledger.

### People
Fields should include:
- canonical ID;
- name;
- first encounter;
- age band if relevant;
- relationship to narrator;
- stable traits;
- expertise;
- speech tendencies;
- shared history;
- known information;
- conflicts/tensions;
- current status;
- forbidden contradictions.

### Places
- canonical ID;
- name;
- geography;
- physical layout;
- recurring sensory details;
- contained machines/objects;
- associated people;
- changes over time.

### Machines and important objects
- canonical ID;
- name;
- type;
- acquisition/build date;
- specifications known to narrator;
- maintenance/failure history;
- modifications;
- current state;
- conceptual roles.

### Projects
- canonical ID;
- objective;
- start/end;
- participants;
- constraints;
- prerequisites;
- milestones;
- failures;
- decisions;
- result;
- lessons;
- later callbacks.

### Concepts
- canonical ID;
- definition in curriculum;
- prerequisite concepts;
- first exposure;
- first competent use;
- misconceptions;
- later transfer events;
- mastery estimate.

### Mistakes
Mistakes are first-class entities when educationally important:
- what narrator believed/did;
- why it was plausible;
- consequence;
- discovery mechanism;
- correction;
- recurrence risk;
- later memory callbacks.

### Preferences
Stable preferences may concern:
- explanation style;
- tools;
- design principles;
- working habits;
- aesthetic choices;
- risk tolerance;
- conversational behavior.

Preferences should emerge from experience rather than appear as arbitrary profile facts.

### Unresolved questions
An unresolved question can span many episodes:
- question;
- origin;
- partial hypotheses;
- evidence gathered;
- status;
- resolution episode or intentionally unresolved state.

### Discoveries
- observation;
- context;
- prior belief;
- new understanding;
- significance;
- linked concepts/projects.

### Vocabulary
Track important words and phrases:
- first encounter;
- inferred meaning;
- explicit definition;
- later natural usage;
- technical register.

### Memories
A memory record links earlier episodes to later callbacks. It does not imply perfect verbatim recall. It establishes what earlier events can plausibly be referenced.

### Sources / library items
External knowledge sources are first-class persistent entities:
- source ID;
- title/creator;
- source type;
- provenance;
- rights/licensing status;
- first encounter;
- segments encountered;
- reread/reference history;
- concepts connected;
- narrator attitude/interest where relevant;
- unresolved questions created by the source;
- later applications and callbacks.

The source's objective contents and the narrator's current understanding of it are separate state.

### Reading events
A reading event records a specific encounter with a source:
- trigger/reason;
- source/segments;
- knowledge state before;
- comprehension state after;
- notes/questions/misconceptions;
- project or curiosity context;
- later callback targets.

Reading events are chronological state changes even when the source text itself is stored separately.

---

## 4. Narrator knowledge state

At each point in the canonical stream, there is a difference between:
- **world truth**;
- **what the narrator has directly observed**;
- **what the narrator has been told**;
- **what the narrator has read/encountered in recorded sources**;
- **what the narrator currently infers or believes**;
- **what the narrator incorrectly believes**;
- **what remains uncertain**.

The system should be able to answer not only *what Alex knows*, but **how Alex could know it**.

This distinction is critical.

Example:

World truth:
`R3 failed because the motor's stall current exceeded the driver rating.`

Narrator state at Episode 420:
`I suspect a software timing issue.`

The prose in Episode 420 must preserve the wrong hypothesis. Later evidence can resolve it.

---

## 5. Time

Every canonical episode receives:
- ordinal position;
- world date or relative date;
- life era;
- project phase;
- narrator knowledge snapshot/version.

Chronology should be precise enough for continuity but not so bureaucratic that prose becomes diary metadata.

The prose itself need not begin with a date unless natural.

---

## 6. Geography

Physical recurrence is valuable.

A workshop layout should remain stable enough that references such as "the scope on the second bench" have persistent meaning until the workshop explicitly changes.

World geometry may eventually be represented in structured form:
- rooms;
- adjacency;
- storage locations;
- machine locations;
- ordinary routes.

This can support consistency checks and embodied/spatial episodes later.

---

## 7. Continuity events

All meaningful state changes should be explicit records:
- person introduced;
- person leaves;
- machine acquired;
- machine modified;
- project begins;
- project ends;
- place renovated;
- source discovered/recommended/acquired;
- reading begins or resumes;
- source segment encountered;
- source is abandoned or reread;
- concept mastered;
- misconception corrected;
- preference changes;
- question resolved.

Episode generation consumes the state *before* an episode and emits proposed state mutations *after* it.

Those mutations are reviewed before becoming canonical.

---

## 8. World creation process

The world should be designed in layers:

### Stage A — constraints
Decide:
- technological era;
- broad cultural setting;
- narrator starting point;
- available institutions;
- realism level;
- language conventions.

### Stage B — anchor locations
Design 5–10 recurring places in detail.

### Stage C — anchor cast
Design 10–20 high-recurrence people plus a controlled secondary cast.

### Stage D — anchor machines
Design 20–50 machines/objects that can recur across curriculum arcs.

### Stage E — project backbone
Design the first 20–40 project arcs.

### Stage F — unresolved threads
Seed questions, tensions, ambitions, and problems that can resolve later.

Only after these are reviewed should bulk episode generation begin.

---

## 9. Recommended world tone

The world should feel ordinary enough that technical competence grows naturally.

Avoid:
- constant dramatic emergencies;
- every conversation becoming a lesson;
- implausibly convenient experts;
- magical availability of equipment;
- perfect project outcomes;
- characters who exist only to ask exposition questions.

Prefer:
- practical constraints;
- modest budgets;
- missing parts;
- misunderstandings;
- waiting for measurements;
- incremental repairs;
- boredom and routine in small doses;
- social relationships not reducible to technical teaching;
- technical learning embedded in real objectives.

The result should read as a life that happens to be unusually information-dense, not as a textbook wearing a diary costume.
