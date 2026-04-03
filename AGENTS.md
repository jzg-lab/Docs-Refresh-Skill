# AGENTS.md

This repository publishes the `docs-refresh` documentation-refresh workflow in a reusable prompt/skill layout. Keep this file as a map, not the source of truth for behavior.

## Authority

1. `docs-refresh/SKILL.md` is the authoritative router and shared behavior contract.
2. `docs-refresh/modes/*.md` are the authoritative mode-specific workflow branches selected by the router.
3. `docs-refresh/scripts/collect_changed_context.sh` is the authoritative definition of the bundled context collector and routing oracle.
4. `docs-refresh/agents/openai.yaml` is optional adapter metadata for OpenAI-compatible surfaces and should stay aligned with the workflow name and short description.
5. `README.md` is the human-facing overview and install pointer.

## Map

- `docs-refresh/` bundles the installable skill directory.
- `docs-refresh/modes/` holds the routed workflow branches loaded after the collector decides repository mode.
- `docs-refresh/scripts/` holds helper scripts referenced by the skill.
- `docs-refresh/agents/` holds optional platform adapter metadata.

## Maintenance Rules

- Update `docs-refresh/SKILL.md` and the relevant file under `docs-refresh/modes/` together when routed behavior changes.
- Update `docs-refresh/agents/openai.yaml` whenever the skill name or short description changes.
- Keep `docs-refresh/scripts/collect_changed_context.sh` aligned with the mode names and routing rules documented in `docs-refresh/SKILL.md`.
- Keep the core workflow platform-neutral. Host-specific aliases and metadata belong in adapter files, not in the core workflow.
- Add new bundled resources under `docs-refresh/` and link them from `docs-refresh/SKILL.md` before adding more root-level docs.
- Keep root docs short; do not duplicate the full skill body here.
