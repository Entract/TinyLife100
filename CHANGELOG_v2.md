# LIFE100 Design v2 — Change Summary

## Core conceptual change

Design v1 treated LIFE100 primarily as one synthetic first-person corpus with external sources used backstage for factual grounding.

Design v2 defines the Life as the **organizing structure of the entire dataset**.

External human-authored books, textbooks, manuals, papers, literature, code, documentation, and artifacts can now become explicit experiences at designed moments in the chronology while retaining their native authorship/voice.

## Added

- `docs/15_LIBRARY_AND_READING_EVENTS.md`
- `docs/16_CORPUS_MIXTURE_AND_COMPILATION.md`
- `schemas/source.schema.json`
- `schemas/reading_event.schema.json`
- `schemas/stream_item.schema.json`
- reading/source/stream examples
- material-class and mixture configuration
- rights/provenance hard-gate design
- contextualized vs decontextualized experiment
- Life/source mixture sweep
- source holdout and reading-transfer evaluations
- first-100-episode interleaved reading plan

## Changed

- Project hypothesis now distinguishes **one narrator** from **one point of reception**.
- Canonical chronology is now a stream of typed items rather than episodes only.
- Narrator knowledge tracks acquisition provenance: observed/told/read/measured/inferred.
- Voice contract applies to Life-native narrator prose, not external readings.
- 250M-token target is a compiled-corpus target rather than a synthetic-prose target.
- No fixed natural/synthetic ratio is assumed.
- Source inclusion requires explicit provenance and rights/training-use status.
