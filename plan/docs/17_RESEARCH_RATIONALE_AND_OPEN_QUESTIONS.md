---
category: feature
---

# TL100 Research Rationale, Evidence Map, and Open Questions (Design v3)

> Status: living evidence map.
>
> Last evidence review: 2026-08-11.
>
> This document records why TL100 is worth testing, what adjacent work has and has not established, and what findings would weaken or falsify the project’s hypotheses.

## 1. Evidence standard

TL100 begins with a motivated question, not a presumed result.

Prior work can establish that:

- small models are sensitive to data design;
- curricula can alter learning dynamics;
- related documents can be useful when placed together;
- coherent document organization can matter;
- global developmental order can fail to matter;
- synthetic-data mixture effects are conditional;
- data-limited training requires careful exposure accounting.

Prior work does not establish that TL100’s full relational stream will help.

The project must distinguish:

1. findings reported by cited work;
2. TL100’s interpretation of those findings;
3. hypotheses that remain untested;
4. inferences that require new experiments.

## 2. The open intersection

The literature contains work on curriculum order, related-document packing, document coherence, synthetic data, child-directed data, and small-model training.

The specific intersection TL100 targets remains insufficiently tested:

- one persistent acquisition reference point;
- typed causal, temporal, referential, prerequisite, and epistemic relationships;
- recurring entities and delayed callbacks;
- recorded belief support, conflict, and correction;
- external sources connected to later application;
- exact same-token controls that separate local attention context from global update order;
- evaluation of transfer and epistemic state rather than world recall alone.

This is a narrower and more defensible research contribution than “train a model on a human life.”

## 3. Evidence that structured data can matter

### 3.1 TinyStories — bounded distributions can support very small models

Ronen Eldan and Yuanzhi Li, “TinyStories: How Small Can Language Models Be and Still Speak Coherent English?” arXiv:2305.07759, 2023.

Primary source: https://arxiv.org/abs/2305.07759

Reported result:

- A deliberately restricted synthetic story distribution supported fluent, coherent generation in models below 10M parameters.

TL100 relevance:

- Small models can display useful behavior when the data distribution is intentionally bounded.
- Data construction can be a primary experimental variable.

Limit:

- TinyStories does not test persistent acquisition state, global chronology, causal recurrence, or exact same-content order controls.

### 3.2 Skill-It — prerequisite relationships can improve data efficiency

Mayee F. Chen, Nicholas Roberts, Kush Bhatia, Jue Wang, Ce Zhang, Frederic Sala, and Christopher Ré, “Skill-it! A Data-Driven Skills Framework for Understanding and Training Language Models.” arXiv:2307.14430, 2023.

Primary source: https://arxiv.org/abs/2307.14430

Reported result:

- The authors formalized ordered skill relationships and reported that prerequisite-skill data could reduce the data needed for more advanced skills.
- Their sampling method improved results in synthetic, instruction, and continual-pretraining settings.

TL100 relevance:

- Prerequisite structure is a plausible mechanism.
- It also creates an essential confound: a full relational stream must be compared with a curriculum-only control.

Limit:

- Skill order is not the same as a persistent situated acquisition history.

### 3.3 In-context Pretraining — related documents inside context can help

Weijia Shi, Sewon Min, Maria Lomeli, Chunting Zhou, Margaret Li, Gergely Szilvasy, Rich James, Xi Victoria Lin, Noah A. Smith, Luke Zettlemoyer, Scott Yih, and Mike Lewis, “In-context Pretraining: Language Modeling Beyond Document Boundaries.” arXiv:2310.10638, revised 2024.

Primary source: https://arxiv.org/abs/2310.10638

Reported result:

- Related documents were ordered into shared pretraining contexts rather than randomly concatenated.
- The authors reported improvements on in-context learning, reading comprehension, faithfulness, long-context reasoning, and retrieval-augmentation evaluations.

TL100 relevance:

- Local relational availability is plausible.
- The work strongly motivates separating relationships visible to attention from chronology expressed only through optimizer updates.

Limit:

- Topical or retrieval similarity between documents is not a causal acquisition graph.

### 3.4 Corpus ordering studies — order can affect convergence

Ameeta Agrawal, Suresh Singh, Lauren Schneider, and Michael Samuels, “On the Role of Corpus Ordering in Language Modeling.” SustaiNLP 2021.

Primary source: https://aclanthology.org/2021.sustainlp-1.15/

Reported result:

- Several curriculum schedules improved transformer pretraining results relative to a vanilla condition.
- A reported one-epoch hard-to-easy condition outperformed the baseline on average GLUE score and reached comparable performance in fewer steps.

TL100 relevance:

- Update order can matter under some regimes.

Limit:

- Difficulty ordering does not isolate chronological, causal, or epistemic structure.

### 3.5 Beyond Random Sampling — larger systematic evidence for curriculum effects

Yang Zhang, Amr Mohamed, Hadi Abdine, Guokan Shang, and Michalis Vazirgiannis, “Beyond Random Sampling: Efficient Language Model Pretraining via Curriculum Learning.” EACL 2026.

Primary source: https://aclanthology.org/2026.eacl-long.271/

Reported result:

- Across more than 200 models and several training regimes, curriculum strategies accelerated early and middle convergence.
- The authors reported sustained but smaller improvements when curriculum was used as a warmup before standard random sampling.

TL100 relevance:

- Data order is a credible efficiency variable.
- Effects may be strongest in learning dynamics rather than final capabilities, so TL100 must evaluate checkpoints and sample efficiency.

Limit:

- Readability or difficulty curricula are not relational acquisition streams.

### 3.6 Influence-driven curriculum learning — useful curricula may be model-relative

Loris Schoenegger, Lukas Thoma, Terra Blevins, and Benjamin Roth, “Influence-driven Curriculum Learning for Pre-training on Limited Data.” BabyLM 2025.

Primary source: https://aclanthology.org/2025.babylm-main.26/

Reported result:

- The authors found that an influence-based, model-centric ordering could outperform random order in limited-data pretraining.

TL100 relevance:

- A human-intuitive curriculum is not automatically a model-effective curriculum.
- TL100 should measure learning dynamics rather than assume its designed order is privileged.

Limit:

- Influence ordering is selected from model behavior and does not test persistent relational structure.

### 3.7 Book-level organization — content-matched document structure can matter

Jiawen Tao, Miao Peng, Yaoming Li, Xiaokun Yuan, Mengzhou Wu, Wenhan Yu, Guoan Wang, Nuo Chen, Tong Yang, and Maxm Pan, “Beyond Rephrasing: Book-Level Organization Improves Synthetic Textbook Data for Mid-Training.” arXiv:2607.28109, 2026.

Primary source: https://arxiv.org/abs/2607.28109

Reported result:

- A content-matched condition holding generated text and tokens fixed performed better when sections remained packaged as coherent books than when treated as independent documents.
- A random-concatenation control did not recover the same result.

TL100 relevance:

- Organization can have value beyond token content and sequence length.
- Content-matched structure controls are feasible.

Limit:

- This is a recent preprint about large-model mid-training and book organization, not small-model pretraining or acquisition chronology.

## 4. Evidence that cautions against the hypothesis

### 4.1 Child-directed speech — local order mattered; global developmental order did not

Steven Y. Feng, Noah D. Goodman, and Michael C. Frank, “Is Child-Directed Speech Effective Training Data for Language Models?” EMNLP 2024.

Primary source: https://aclanthology.org/2024.emnlp-main.1231/

Reported result:

- The study compared child-directed and matched synthetic dialogue data with other corpora.
- Local discourse properties affected results.
- Global developmental ordering did not produce the expected benefit.
- Child-directed input was not uniquely valuable for the tested language models.

TL100 relevance:

- This is the most important negative adjacent result.
- Human-like developmental ordering must not be assumed useful merely because humans receive data developmentally.
- Local relational context may matter more than chronology across optimizer updates.

Design consequence:

- TL100’s first experiment separates local context from global update order.
- A null global-order result should narrow the project rather than be rationalized away.

### 4.2 Synthetic-data mixture — generated data can narrow or degrade

Feiyang Kang, Newsha Ardalani, Michael Kuchnik, Youssef Emad, Mostafa Elhoushi, Shubhabrata Sengupta, Shang-Wen Li, Ramya Raghavendra, Ruoxi Jia, and Carole-Jean Wu, “Demystifying Synthetic Data in LLM Pre-training: A Systematic Study of Scaling Laws, Benefits, and Pitfalls.” EMNLP 2025; arXiv:2510.01631.

Primary source: https://arxiv.org/abs/2510.01631

Reported result:

- Pure rephrased synthetic data did not automatically improve convergence over natural web text.
- Pure generated textbook-style data showed worse loss on several downstream domains, especially at smaller budgets.
- Useful mixture ratios depended on data type, model size, and budget.

TL100 relevance:

- A relational corpus cannot be assumed superior merely because it is curated or synthetic.
- External-language evaluation and mixture controls are mandatory.
- No universal synthetic/human ratio should be adopted.

Limit:

- TL100’s relationally constructed material differs from the synthetic types studied, so the reported mixture values are not prescriptions.

### 4.3 Compute-optimal scaling — a model-size label does not determine a data budget

Jordan Hoffmann et al., “Training Compute-Optimal Large Language Models.” arXiv:2203.15556, 2022.

Primary source: https://arxiv.org/abs/2203.15556

Reported result:

- Compute-optimal model size and training-token count scale together.
- Undertraining a comparatively large model wastes capacity under a general-language compute objective.

TL100 relevance:

- A 100M-parameter target does not justify a 250M-token target by itself.
- Corpus size, unique data, replay, exposure count, and compute must remain separate variables.

Limit:

- Compute-optimal general-language loss is not identical to TL100’s data-structure research objective.

### 4.4 Data-constrained scaling — repetition has bounded value

Niklas Muennighoff, Alexander M. Rush, Boaz Barak, Teven Le Scao, Aleksandra Piktus, Nouamane Tazi, Sampo Pyysalo, Thomas Wolf, and Colin Raffel, “Scaling Data-Constrained Language Models.” arXiv:2305.16264, revised 2025.

Primary source: https://arxiv.org/abs/2305.16264

Reported result:

- With fixed compute and constrained data, up to four repeated epochs produced little loss difference relative to equivalent unique data in the studied regimes.
- Additional repetition eventually had sharply diminishing value.

TL100 relevance:

- Controlled replay is viable but must be explicitly counted.
- Unique accepted tokens and total training exposures are not interchangeable.

Limit:

- The study concerns loss scaling across broad corpora, not relational replay or acquisition callbacks.

## 5. Additional motivating work retained from Design v2

### 5.1 Textbooks Are All You Need

Suriya Gunasekar et al., “Textbooks Are All You Need.” arXiv:2306.11644, 2023.

Primary source: https://arxiv.org/abs/2306.11644

Reported contribution:

- Carefully selected and generated textbook-like data enabled strong code performance at relatively small model scale.

TL100 relevance:

- Data quality and construction can materially affect capability per parameter.

Limit:

- Textbook quality, code specialization, and relational acquisition structure are different variables.

## 6. What no cited work establishes

No cited work establishes that:

- one persistent acquisition history is optimal;
- global chronology will outperform shuffled updates;
- a single epistemic center improves calibration or correction behavior;
- recurring identities improve general transfer rather than memorization;
- a relational stream is better than a prerequisite curriculum;
- source encounters embedded in a stream improve later source use;
- a small decoder-only transformer can exploit dependencies spanning millions of tokens;
- 100M parameters is the correct final scale;
- any fixed corpus size or material mixture is optimal;
- language-only data reproduces the efficiency of human learning;
- a model trained on acquisition records has experiences.

These remain hypotheses or are outside TL100’s claims.

## 7. Registered hypothesis language

### Primary hypothesis

For fixed text units and token exposures, preserving local relational adjacency and canonical acquisition order changes sample efficiency or relational transfer relative to controlled disruption.

### Primary null

After controlling text, exposure, context visibility, curriculum, and training schedule, the structured stream yields no repeatable improvement beyond in-stream memorization.

### Secondary hypotheses

- A stable epistemic center improves time-indexed belief and source attribution.
- Typed recurrence improves transfer across surface contexts.
- Correction arcs reduce persistence of explicitly superseded beliefs.
- Human-authored source material protects linguistic breadth at some mixtures.

### Disconfirming patterns

- gains disappear when prose quality is matched;
- curriculum-only equals the full relational condition;
- improvements occur only for recurring names and direct fact recall;
- global chronology has no effect after local context is controlled;
- external transfer degrades more than in-world metrics improve;
- results fail across seeds;
- evaluation performance tracks lexical overlap with training text.

## 8. Threat-to-validity matrix

| Threat | Why it matters | Required control |
|---|---|---|
| content mismatch | one condition may simply contain better explanations | exact-token order experiment first |
| local versus global order | shared attention context and update chronology are different mechanisms | factorial context-boundary and update-order conditions |
| prerequisite confound | curriculum may explain the full effect | curriculum-only control |
| replay imbalance | earlier items may receive more effective exposure | exact exposure manifests |
| source quality | one mixture may contain better authorities | fixed source subset in matched comparisons |
| generator signature | model learns a narrow authoring style | multiple authoring routes, style metrics, human-source controls |
| world memorization | recurring names inflate apparent capability | renamed and surface-transfer tests |
| evaluation leakage | tests paraphrase training records | graph-separated and source-held-out evaluations |
| seed variance | small effects may be accidental | multiple seeds and confidence intervals |
| capacity mismatch | a model may be unable to exploit the designed horizon | several model sizes and checkpoint curves |
| data scarcity | repeated data can overfit | unique-token and exposure accounting |
| anthropomorphic framing | metaphor is mistaken for mechanism | operational definitions and non-goals |

## 9. Ranked open questions

### Q1 — Local versus global structure

Do gains come from related items sharing an attention context, from ordered parameter updates, or from their interaction?

### Q2 — Relational construction versus curriculum

Does a persistent acquisition graph add anything beyond prerequisite ordering?

### Q3 — Transfer versus memorization

Does recurrence teach reusable structure or merely make recurring facts easier to recall?

### Q4 — Epistemic state

Can a small model learn what was known, uncertain, or believed at different stream positions?

### Q5 — Correction

Does an explicit acquisition and correction sequence reduce obsolete-belief errors, or does repeating the wrong belief strengthen it?

### Q6 — Dependency horizon

How far apart can linked items be before a model of a given size stops benefiting from the relationship?

### Q7 — Replay

Does explicit, causally motivated recurrence behave differently from arbitrary repeated exposure?

### Q8 — Mixture

How much project-authored relational material can be used before language and domain breadth deteriorate?

### Q9 — Model scale

At what model and corpus sizes do relational effects first appear, peak, or disappear?

### Q10 — Negative result interpretation

If global chronology is null, can local relational packing or graph-designed content still justify the project?

## 10. Decision rules

Evidence should increase confidence in TL100 when:

- exact-token structural conditions differ consistently across seeds;
- benefits appear on held-out transfer, not just canonical recall;
- effects survive a curriculum-only comparison;
- learning curves show interpretable changes before final convergence;
- external-language penalties are measured and acceptable;
- manifests reproduce every result.

Evidence should decrease confidence when:

- only subjective prose ratings improve;
- exact-token conditions converge to the same behavior;
- effects disappear after controlling local context;
- relational advantages are explained by extra replay;
- generated style dominates the signal;
- broad transfer collapses;
- results cannot be replicated.

## 11. Working scientific stance

TL100 proceeds with strong motivation and weak attachment to a positive result.

The project succeeds if it produces a reproducible answer to a narrow question:

> Does a controlled relational acquisition stream change small-model learning relative to matched disruption?

A clear null, a local-only effect, a curriculum-only explanation, or a measured narrowness tradeoff are all valid outcomes.
