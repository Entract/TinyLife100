---
category: feature
---

# TL100 Glass-Box Engineering and Tokenizer Protocol

> Status: binding Design v3 engineering charter and tokenizer-family decision.
>
> Final vocabulary size and any pre-tokenization rule remain open until the documented bakeoff and human decision gate.

## 1. Why glass-box engineering is a project requirement

TL100 has two objectives:

1. investigate whether relational acquisition structure changes what a small language model learns;
2. let the project owner learn how the entire language-model system works by constructing, inspecting, and testing each conceptual layer.

The second objective changes the engineering standard. Reproducibility alone is insufficient if a critical decision is hidden behind a library default. Conversely, “from scratch” does not mean recreating operating systems, GPU kernels, automatic differentiation, or cryptographic primitives.

The rule is:

> Build and explain the concepts that determine the experiment. Borrow low-level machinery deliberately, pin it, expose its role, and test the boundary.

## 2. Definition of glass-box complete

A component is glass-box complete when the project owner can answer:

- What problem does it solve?
- What are its exact inputs and outputs?
- What mathematical or algorithmic transformation does it perform?
- Which decisions are ours and which come from a dependency?
- Which defaults could change scientific results?
- How is it represented on disk?
- How can a tiny example be calculated by hand?
- Which invariants and tests would reveal a defect?
- How does changing it affect parameter count, compute, data exposure, or evaluation?
- Which hash and version identify the exact instance used in a run?

Every major component therefore needs:

- a concise conceptual explanation;
- equations or pseudocode where useful;
- one inspectable toy example;
- an implementation contract;
- a decision record;
- deterministic tests;
- serialized artifacts that can be opened without the original process;
- a manifest link from every experiment that uses it.

## 3. Build, borrow, and verify policy

### 3.1 Build inside TL100

The project should own readable implementations of:

- canonical normalization and domain-separated hashing;
- tokenizer training, encoding, decoding, and artifact inspection;
- canonical graph, stream, and acquisition-state transitions;
- data selection, packing, boundaries, masks, and update schedules;
- the decoder-only Transformer model definition;
- parameter accounting;
- causal attention and cross-node masking logic;
- next-token loss construction;
- batching and exposure accounting;
- the training loop and learning-rate schedule;
- checkpoint metadata and evaluation orchestration;
- primary relational and epistemic evaluations.

The first implementation favors clarity over speed. An optimized replacement is allowed only after it matches the readable reference on golden and adversarial cases.

### 3.2 Borrow deliberately

The project may borrow:

- Python and its standard library;
- PyTorch tensor operations, automatic differentiation, device dispatch, and GPU kernels;
- a standards-compliant JSON Schema implementation;
- established numerical, plotting, and tabular libraries;
- file formats whose specifications and readers are stable;
- operating-system, filesystem, compression, and cryptographic primitives.

For each runtime dependency, record:

- package and version;
- license;
- why it is used;
- which scientific behaviors it can affect;
- defaults overridden by TL100;
- boundary/conformance tests;
- environment-lock identity.

### 3.3 Do not borrow invisibly

The primary experiment must not silently inherit:

- pretrained weights;
- a pretrained tokenizer vocabulary or merge table;
- an opaque chat template;
- automatic normalization or lowercasing;
- hidden data filtering;
- framework shuffling or dynamic packing;
- an undocumented optimizer or scheduler configuration;
- evaluation prompts drawn from training data;
- automatic metric aggregation whose samples cannot be inspected.

Reference implementations may be used for comparison, but their output is not accepted merely because the library is popular.

## 4. Opaque-boundary register

Maintain a machine-readable register for every borrowed boundary. Each entry records:

- boundary ID;
- component and version;
- function performed;
- inputs and outputs;
- deterministic or nondeterministic behavior;
- relevant defaults;
- known limitations;
- tests and comparison artifacts;
- decision owner and review date.

Examples include UTF-8 decoding, SHA-256, JSON canonicalization, PyTorch matrix multiplication, fused attention, random-number generation, and checkpoint serialization.

The purpose is not distrust for its own sake. It is to make the line between “we implemented this rule” and “we rely on this primitive” visible.

## 5. Discussion and decision gates

The following decisions require a written recommendation and explicit project-owner discussion before they are frozen:

1. pilot domain and acquisition graph;
2. tokenizer algorithm, vocabulary size, and special-token policy;
3. model parameter budget and architecture;
4. initialization, numerical precision, and parameter tying;
5. optimizer, learning-rate schedule, batch size, and exposure budget;
6. attention-context construction and position behavior;
7. evaluation sets, metrics, aggregation, and success thresholds;
8. any use of external source text;
9. transition from diagnostic models to larger data or a 100M-parameter model.

Implementation may build tooling before a gate, but it may not silently freeze the scientific choice.

## 6. Tokenizer decision

TL100 will not use a borrowed pretrained tokenizer for its primary from-scratch models.

It will implement a readable **byte-level byte-pair encoding (BPE)** reference tokenizer and a byte-only baseline. The final pilot tokenizer will be trained on a content-addressed TL100 tokenizer-training corpus and selected through the bakeoff in this document.

This is a deliberate middle ground:

- byte-level representation guarantees coverage and exact reversibility without an unknown token;
- BPE makes common byte sequences shorter and therefore increases effective text per context window;
- the algorithm is small enough to implement, visualize, and test completely;
- vocabulary size exposes a measurable tradeoff between sequence length and embedding parameters;
- a project-trained vocabulary does not import another model’s corpus distribution.

SentencePiece/Unigram remains a valid later comparison, not the initial implementation. Its probabilistic training and normalization pipeline add concepts worth learning after the deterministic BPE baseline is understood.

## 7. Why not simply borrow a tokenizer?

A borrowed vocabulary would save engineering time, but it imports:

- another corpus’s language, code, formatting, and frequency distribution;
- another vocabulary-size choice;
- another pre-tokenization regex;
- special-token conventions;
- possible normalization behavior;
- unexplained parameter and context costs for this unusually small model.

That would undermine the pedagogical objective and make TL100 less inspectable. It could also spend scarce embedding parameters on strings absent from the project.

Borrowed implementations such as Hugging Face Tokenizers, SentencePiece, or OpenAI’s tiktoken may be used for comparison, performance benchmarking, and independent test vectors. They do not supply the primary vocabulary.

## 8. Why not remain byte-only?

A byte-only model has an exceptionally clear 256-symbol base representation and removes learned segmentation. Research such as ByT5 demonstrates that byte-level models are viable and can avoid tokenizer preprocessing complexity.

The cost is longer sequences. Longer sequences reduce the amount of meaningful text inside a fixed attention window and increase training and inference work per character. That matters directly to TL100 because local relational availability is one of the experimental factors.

Byte-only is therefore retained as:

- the base vocabulary underneath BPE;
- a correctness baseline;
- one tokenizer bakeoff candidate;
- a possible later experimental condition.

It is not assumed to be the production choice.

## 9. Normalization boundary

Tokenization begins only after Text Normalization v1 from `07_CURATION_AND_QA.md`:

1. strict UTF-8 decoding;
2. removal and reporting of an initial UTF-8 byte-order mark;
3. Unicode NFC normalization;
4. CRLF and CR conversion to LF;
5. no other whitespace or text rewriting;
6. UTF-8 encoding without a byte-order mark.

The tokenizer itself performs no lowercasing, accent removal, whitespace cleanup, compatibility normalization, or source-specific cleaning.

The primary decoder returns bytes. A text convenience method decodes UTF-8 strictly. This distinction makes arbitrary token-sequence behavior inspectable even when a generated byte sequence is not valid UTF-8.

## 10. Initial BPE algorithm contract

### 10.1 Training units

- Each unique normalized training payload contributes once.
- Canonical rereads and compiler replay do not multiply tokenizer-training frequency.
- Payload boundaries are hard; pairs never cross them.
- Evaluation text and held-out probes are excluded.
- Metadata-only records contribute no bytes.
- Source payloads contribute only when training use is approved for the tokenizer-training purpose.
- The exact ordered payload inventory and its order-independent multiset hash are recorded.

Counting unique payloads prevents the experimental exposure schedule from changing the vocabulary.

### 10.2 Initial symbols

Token IDs `0..255` represent individual byte values exactly.

Merge tokens are assigned consecutive IDs beginning at `256`. Each merge token stores:

- left parent ID;
- right parent ID;
- resulting byte sequence;
- merge rank;
- pair count at selection;
- training configuration and corpus identities.

### 10.3 Merge iteration

For each iteration:

1. count every adjacent token pair inside each payload sequence;
2. discard pairs below the declared minimum frequency or above the maximum resulting byte length;
3. select the highest-count pair;
4. break ties lexicographically by left bytes, right bytes, left ID, then right ID;
5. assign the next token ID;
6. replace non-overlapping occurrences left-to-right in every payload;
7. record the complete decision;
8. stop at the target lexical vocabulary size or when no eligible pair remains.

Pair counting, replacement overlap, tie-breaking, and maximum-token-length behavior are test vectors, not implementation details.

### 10.4 Encoding

Encoding starts with UTF-8 bytes and applies known merges in learned rank order until no eligible pair remains. It cannot emit an unknown token.

An optimized encoder may use heaps or cached pair indexes, but it must exactly match the slow reference encoder.

### 10.5 Decoding

Decoding concatenates the byte sequence assigned to every ordinary token. For all normalized payload bytes `b`:

```text
decode_bytes(encode_bytes(b)) == b
```

Special tokens are compiler controls and are not accepted as ordinary payload content.

## 11. Pre-tokenization decision

The first reference implementation uses no word-level or regex pre-tokenizer. It prevents merges only across explicit payload boundaries and enforces a configurable maximum token byte length.

This choice is maximally visible and language-independent, but it may learn phrase fragments or boilerplate across spaces. The bakeoff must display the longest and most frequent learned tokens in escaped text and hexadecimal bytes.

A boundary-aware candidate may be added if the plain model produces pathological phrase tokens. Any pre-tokenizer must then have:

- its own algorithm and test vectors;
- explicit Unicode and byte behavior;
- no hidden library normalization;
- a separate tokenizer identity;
- comparison against the no-pretokenizer candidate.

The project will not inherit a GPT-style regex without understanding and documenting every class and boundary rule.

## 12. Special-token policy

The provisional minimal set is:

- `PAD` — fixed-shape padding, always excluded from loss;
- `BOS` — optional beginning of a compiler-defined sequence;
- `EOS` — optional end of a compiler-defined sequence;
- `NODE_BOUNDARY` — visible, condition-invariant node boundary.

Special IDs follow the lexical vocabulary. They are inserted by the compiler as typed controls, not recognized by scanning payload strings. Literal text that resembles a special-token spelling remains ordinary bytes.

No semantic source, speaker, claim, or curriculum tags enter the primary training text unless a later experiment explicitly studies them.

The final need for `BOS` and `EOS`, their loss treatment, and all numeric IDs are frozen at the tokenizer decision gate.

## 13. Vocabulary-size bakeoff

The initial candidates use these lexical vocabulary sizes, plus the four provisional special tokens:

| Lexical vocabulary | Total with four specials | Role |
|---:|---:|---|
| 256 | 260 | byte-only baseline |
| 1,024 | 1,028 | very small BPE |
| 2,048 | 2,052 | small BPE |
| 4,096 | 4,100 | medium pilot candidate |
| 8,192 | 8,196 | upper pilot comparison |

Candidates may stop below target when the minimum-frequency rule leaves no eligible pair.

No vocabulary size is the default winner.

## 14. Vocabulary parameter cost

With tied input embeddings and output projection and no output bias, vocabulary parameters are:

```text
vocabulary_parameters = total_vocabulary_size × d_model
```

With untied input/output matrices, the matrix cost is doubled. An output bias, if used, adds one parameter per vocabulary item in either case.

At `d_model = 256`:

| Total vocabulary | Tied vocabulary parameters |
|---:|---:|
| 260 | 66,560 |
| 1,028 | 263,168 |
| 2,052 | 525,312 |
| 4,100 | 1,049,600 |
| 8,196 | 2,098,176 |

For a 3M-parameter diagnostic model, a 4,100-token tied table is roughly one third of the entire budget. Vocabulary size must therefore be selected jointly with model width and the policy for counting embedding parameters.

## 15. Bakeoff measurements

For every candidate, report overall and by material class, source, domain, and text form:

- normalized bytes;
- Unicode scalar values and characters under the declared counting rule;
- total tokens;
- bytes per token;
- tokens per character;
- median and tail payload length in tokens;
- proportion of payloads exceeding intended context lengths;
- vocabulary utilization and token-frequency distribution;
- count and share of tokens below selected frequency thresholds;
- longest tokens and escaped/hex renderings;
- word, whitespace, newline, number, code, and punctuation fragmentation;
- special-token collisions;
- encode/decode throughput and peak memory;
- tied and untied parameter cost at every candidate model width;
- expected attention-cost change per normalized byte;
- behavior on held-out Unicode, code, tables, equations, and malformed-input tests.

Do not rank candidates by compression alone.

## 16. Freeze criteria

The scientific tokenizer is frozen only after:

- the pilot payload candidate set is content-addressed;
- the evaluation/probe text is excluded and hashed separately;
- every candidate passes deterministic correctness tests;
- the full vocabulary is human-inspected or programmatically grouped with manual review of every suspicious/long token;
- parameter costs are compared with candidate architectures;
- sequence lengths fit the intended context and compute envelope;
- rare or memorized phrase tokens are reviewed;
- the project owner discusses the recommendation and approves one candidate;
- the complete artifact bundle reproduces from a clean checkout and authorized inputs.

Selection uses development measurements and predeclared engineering constraints, not primary experimental test results.

Once any model training begins, changing the tokenizer creates a new experimental family. Token IDs are never silently reassigned.

## 17. Provisional versus scientific tokenizers

The pipeline needs a tokenizer before the final pilot corpus exists, creating an apparent circular dependency.

TL100 resolves this explicitly:

- **provisional tokenizer:** trained on rights-clear fixtures and draft payloads; used only to implement and test compiler/loader mechanics;
- **scientific tokenizer:** trained after the pilot payload candidate set is frozen; used for the four matched conditions and every reported model in that experimental family.

Provisional token counts are estimates. Canonical record identity does not depend on token IDs, so the scientific tokenizer can be frozen later without changing canon. Final release selection and the stated 100k–250k token range are confirmed under the scientific tokenizer before training.

## 18. Required tokenizer artifacts

One frozen tokenizer directory contains:

```text
tokenizer-config.json
training-corpus-manifest.json
normalization-policy.json
merges.jsonl
vocabulary.jsonl
special-tokens.json
test-vectors.jsonl
metrics.json
parameter-costs.json
decision.md
validation-report.json
```

Each merge row records rank, token ID, parent IDs, byte sequence in hexadecimal, count at selection, and relevant configuration. `vocabulary.jsonl` includes both a safe escaped rendering and exact bytes.

The manifest identifies every file by hash and records code, dependency, and environment versions.

## 19. Deterministic tokenizer tests

At minimum:

- all 256 base byte values round-trip through byte APIs;
- every accepted normalized payload round-trips exactly;
- empty, ASCII, multi-byte Unicode, combining-mark, emoji, code, table, newline, and long-repetition cases;
- strict handling of invalid UTF-8 at the normalization boundary;
- stable training under shuffled input-file order;
- stable tie-breaking on adversarial equal-frequency pairs;
- correct overlapping-pair replacement;
- no merge across payload or compiler boundaries;
- identical encode output before and after save/load;
- literal special-token-like strings remain ordinary bytes;
- compiler-only special insertion is typed and explicit;
- slow reference and optimized implementations agree token-for-token;
- random/property-based round-trip and serialization tests;
- vocabulary and merge graph contain no cycles or orphaned parents;
- every token’s bytes equal the concatenation of its parents.

Golden artifacts are small enough to inspect manually.

## 20. Independent verification

The readable TL100 implementation is authoritative for its own artifacts, but it receives independent pressure from:

- a second simple encoder implementation with a different internal strategy;
- optional import of the frozen vocabulary/merges into a mature BPE library where semantics align;
- comparison against byte-level educational implementations on shared toy cases;
- mutation tests that intentionally alter ranks, IDs, boundaries, and special-token handling;
- manifest reproduction in a clean environment.

Conformance means exact output agreement for the same declared algorithm. It does not mean adopting another library’s normalization, regex, or vocabulary.

## 21. Model and training glass-box follow-through

The tokenizer is only the first visible layer. Before task 19 freezes the training system, separate explanations and toy validations must cover:

- embedding lookup and tied versus untied output weights;
- positional representation;
- layer normalization;
- causal self-attention, masking, and softmax;
- multi-head reshaping;
- feed-forward blocks and activation choice;
- residual connections;
- logits and cross-entropy next-token loss;
- initialization;
- AdamW state and update equations;
- gradient accumulation, clipping, and mixed precision;
- checkpoint state;
- sampling and decoding;
- evaluation aggregation and uncertainty across seeds.

For each, TL100 should show shapes, parameter counts, a hand-sized example, implementation tests, and the exact serialized configuration.

## 22. Decision-record template

Every consequential engineering decision records:

```text
decision_id
status: proposed | discussed | accepted | superseded
question
options considered
recommendation
evidence and references
project-specific measurements
scientific variables affected
pedagogical value
risks and failure tests
owner decision
decision date
implementation tasks
artifact hashes
supersedes / superseded_by
```

Discussion summaries distinguish what was measured, inferred, preferred for learning, or accepted for scientific control.

## 23. Research and implementation references

- Sennrich, Haddow, and Birch, [Neural Machine Translation of Rare Words with Subword Units](https://aclanthology.org/P16-1162/) (ACL 2016). Foundational NLP use of BPE-style subword units.
- Kudo and Richardson, [SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing](https://aclanthology.org/D18-2012/) (EMNLP 2018). Raw-sentence subword training and an alternative Unigram/BPE implementation.
- Xue et al., [ByT5: Towards a Token-Free Future with Pre-trained Byte-to-Byte Models](https://aclanthology.org/2022.tacl-1.17/) (TACL 2022). Evidence and tradeoffs for byte-level modeling.
- Dagan, Synnaeve, and Rozière, [Getting the Most Out of Your Tokenizer for Pre-training and Domain Adaptation](https://proceedings.mlr.press/v235/dagan24a.html) (ICML 2024). Empirical evidence that vocabulary size, training data, and pre-tokenization affect efficiency and downstream results.
- Tao et al., [Scaling Laws with Vocabulary: Larger Models Deserve Larger Vocabularies](https://arxiv.org/abs/2407.13623) (NeurIPS 2024). Evidence that vocabulary size should be considered jointly with model and compute scale; its tested scales remain much larger than TL100’s smallest diagnostics.
- Vieira et al., [Language Models over Canonical Byte-Pair Encodings](https://proceedings.mlr.press/v267/vieira25b.html) (ICML 2025). Analysis of canonical versus noncanonical token sequences and probability allocation.
- Karpathy, [minbpe](https://github.com/karpathy/minbpe). A small educational byte-level BPE implementation useful as a readable comparison, not copied as TL100’s authority.
- OpenAI, [tiktoken](https://github.com/openai/tiktoken). A mature fast BPE implementation useful for understanding performance and special-token concerns.
- Hugging Face, [Tokenizers pipeline documentation](https://huggingface.co/docs/tokenizers/main/api/tokenizer) and [trainer documentation](https://huggingface.co/docs/tokenizers/main/api/trainers). Reference decomposition of normalization, pre-tokenization, model, post-processing, and training parameters.

## 24. Current decisions and open questions

### Accepted now

- Glass-box engineering is a first-class objective.
- No pretrained tokenizer vocabulary is used for the primary models.
- TL100 implements its own readable byte-level BPE and byte baseline.
- Normalization is external, explicit, and versioned.
- The tokenizer corpus is content-addressed and excludes evaluation text.
- The primary four conditions share one frozen tokenizer.
- An optimized implementation must conform to the readable reference.

### Open until measured and discussed

- final lexical vocabulary size;
- minimum merge frequency;
- maximum token byte length;
- whether a pre-tokenizer is justified;
- final special-token set and loss treatment;
- tied versus untied embeddings;
- tokenizer parameter accounting in nominal model size;
- final tokenizer-training payload set;
- whether byte-only deserves a full model comparison after the primary experiment.
