# 17 — Research Rationale and Open Questions

> This is a working research note, not a claim that prior studies establish LIFE100's hypotheses.

## 1. Why LIFE100 is plausible enough to test

Several lines of prior work motivate pieces of the design, while leaving the central LIFE100 question unanswered.

### TinyStories — constrained distributions can make small models surprisingly capable

**Ronen Eldan and Yuanzhi Li, “TinyStories: How Small Can Language Models Be and Still Speak Coherent English?” arXiv:2305.07759 (2023).**

TinyStories showed that a deliberately restricted synthetic language distribution can support coherent multi-paragraph generation in models below 10M parameters. LIFE100 extends the general intuition — *small models may benefit from deliberately bounded data distributions* — but uses a much more technically complex, persistent, long-range corpus.

### Textbooks Are All You Need — data quality can matter disproportionately

**Suriya Gunasekar et al., “Textbooks Are All You Need,” arXiv:2306.11644 (2023).**

Phi-1 used selected “textbook quality” web data plus synthetic textbooks/exercises and achieved unusually strong code performance for its size. LIFE100 does not assume textbook-style synthetic prose is sufficient, but takes seriously the idea that data selection/construction can change capability per parameter.

### Demystifying Synthetic Data — synthetic mixture effects are conditional

**Feiyang Kang et al., “Demystifying Synthetic Data in LLM Pre-training: A Systematic Study of Scaling Laws, Benefits, and Pitfalls,” arXiv:2510.01631 / EMNLP 2025.**

The study trained over 1,000 LLM variants and found a strong result for a particular data type: roughly one-third rephrased synthetic data mixed with two-thirds natural web text could substantially accelerate convergence at larger budgets, while pure-generated textbook-style data behaved less favorably on many downstream domains. The useful synthetic fraction depended on model size, data budget, and generation method.

**LIFE100 interpretation:** this is evidence *against* choosing an arbitrary universal synthetic percentage. The reported ~30% is not a prescription for LIFE100 because LIFE100's Life-native data is structurally different from rephrased web data and its human input is intentionally selected rather than generic web text.

### Beyond Rephrasing — organization of the same content can matter

**Jiawen Tao et al., “Beyond Rephrasing: Book-Level Organization Improves Synthetic Textbook Data for Mid-Training,” arXiv:2607.28109 (2026).**

This work reports controlled comparisons in which related synthetic sections preserved as coherent books outperformed content-matched split documents and random concatenations. The study concerns large-model mid-training and book-level organization, not small-model chronological biography.

**LIFE100 interpretation:** it strengthens the reason to test whether *organization itself* can be an experimental variable. LIFE100 pushes that question further: not only “does a book help as a coherent document?” but “does knowledge embedded in a coherent developmental life help relative to the same material detached from that life?”

---

## 2. What prior work does NOT establish

No cited study establishes that:

- one persistent first-person narrator is optimal;
- chronological pretraining will outperform shuffle at ~100M parameters;
- 250M tokens is the right corpus size;
- 30%, 50%, or any other Life/human mixture is optimal;
- synthetic autobiography avoids model-collapse-like narrowing;
- reading a textbook “inside a Life” will improve transfer;
- a 100M model has enough capacity to exploit years of persistent world state;
- human-like developmental order is intrinsically useful for transformers.

Those are LIFE100 questions.

---

## 3. Principal experimental questions

### Q1 — Does Life order matter?

Same text, same token exposure, different ordering.

### Q2 — Does source contextualization matter?

Same human source segment, but either surrounded by causal Life trigger/application or detached from them.

### Q3 — What mixture works best?

Vary Life-native, human-reading, and artifact proportions.

### Q4 — Does one narrator help or narrow?

Compare stable narrator with matched multi-voice Life-native data.

### Q5 — Does recurrence help?

Compare recurring projects/machines/people with matched one-off examples.

### Q6 — Do mistakes help?

Compare lived errors/corrections with polished correct exposition.

### Q7 — What does human-written input buy us?

Measure lexical breadth, OOD comprehension, transfer, narrator stability, and source memorization as reading share increases.

### Q8 — Does coherent source structure matter at small scale?

Preserve selected chapters/books versus fragmenting their content under matched token budgets.

---

## 4. What would make LIFE100 scientifically weak

The project becomes difficult to interpret if:

- different experimental corpora contain different facts;
- different mixtures also use different source quality;
- chronological training gets more replay than shuffled training;
- source text changes between controls;
- rights limitations silently remove data from one condition;
- Life-native prose paraphrases sources so closely that “human vs synthetic” is blurred;
- tests mostly repeat training passages;
- only one random seed is used for a subtle effect;
- the corpus is scaled before small runs reveal its pathologies.

Matched controls and exact manifests are therefore core engineering requirements, not research bureaucracy.

---

## 5. Working stance

LIFE100 should be built with **strong hypotheses and weak attachment to their truth**.

The project is successful if it produces a well-controlled answer — including a null or negative answer — to whether a deliberately constructed experiential structure changes how a small language model uses limited capacity.
