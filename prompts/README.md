# Prompt contracts — Design v2

Prompt text should be version-controlled and hashed.

Recommended files to implement next:

- `curriculum_scheduler.md`
- `encounter_planner.md`
- `source_selector.md`
- `episode_planner.md`
- `writer.md`
- `technical_critic.md`
- `continuity_critic.md`
- `epistemic_critic.md`
- `voice_critic.md`
- `source_integrity_critic.md`
- `curriculum_critic.md`
- `diversity_critic.md`
- `life_critic.md`
- `targeted_reviser.md`

Each prompt should define:

- role;
- allowed inputs;
- output schema;
- forbidden behavior;
- failure reporting;
- version.

## Source-specific rules

`source_selector` must never infer rights/training eligibility. It may recommend candidates, but canonical inclusion requires registry fields and deterministic policy checks.

`writer` writes only Life-native narrator prose. It must not reproduce external source text unless the episode plan explicitly permits a small natural quotation and project policy allows it.

`source_integrity_critic` checks source identity, segment mapping, copying/leakage, and whether surrounding Life prose accurately represents the encountered material.

`voice_critic` scores Alex's narrator-authored prose, not the style of an external reading.

Do not rely on one enormous prompt containing the whole project specification.
