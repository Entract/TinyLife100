# TinyLife100 data directories (Design v2 legacy layout)

> This directory layout predates Design v3 and remains provisional until the canonical graph and compiler specifications are migrated.

- `drafts/` — generated/edited Life material not yet canon
- `canon/` — immutable accepted records and ledgers
- `exports/` — reproducible training views derived from canon
- `evals/` — held-out evaluation material and manifests
- `sources/` — source registry, approved source material where storage policy permits, and source segment metadata
- `readings/` — reading-event planning/records if kept outside `canon/` during drafting
- `artifacts/` — code/log/spec/document artifacts used as Life experiences

## Source-content rule

A source being referenced in `sources/` does **not** mean its full text should be committed to Git.

Possible source storage modes include:

- `repo_fulltext`
- `local_fulltext`
- `metadata_only`
- `grounding_excerpt_only`
- `blocked`

Full text that is not approved for public redistribution should remain outside the public repository. Canonical records can reference immutable IDs/hashes and local/object-store locations.

Do not infer redistribution or training permission from public web availability.

## Large files

Do not commit large generated binary/tokenized shards directly to Git without an explicit storage strategy (Git LFS, object storage, release artifacts, etc.).

Canonical metadata, manifests, schemas, small rights-clear examples, and hashes should remain version-controlled.
