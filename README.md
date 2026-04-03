# Docs Refresh

`docs-refresh` is a portable documentation-refresh workflow packaged in a reusable prompt/skill layout. It treats the repository as the record system, starts from `AGENTS.md` as a map, inspects current workspace state, and updates only the smallest authoritative docs that need to change.

The core workflow lives in plain Markdown at `docs-refresh/SKILL.md`, so it can be adapted to any agent or prompt system that can reuse structured instructions.

## Portable Use

Use `docs-refresh/SKILL.md` as the canonical workflow instructions in your own agent stack.

If shell execution is available, also provide `docs-refresh/scripts/collect_changed_context.sh` so the workflow can gather consistent git context before deciding whether docs need to change.

Any platform-specific aliasing, registration, or metadata should be treated as an adapter layer around the core workflow, not as part of the workflow contract itself.

## Optional OpenAI/Codex Adapter

This repository also includes an optional OpenAI-compatible adapter under `docs-refresh/agents/openai.yaml`.

If you want to install it into a Codex/OpenAI-compatible skill directory, use the host platform's installer against the `docs-refresh/` path in this repository.

## Use

Invoke the workflow however your host platform exposes reusable prompts or skills. In OpenAI/Codex-compatible surfaces, the packaged aliases can be wired to names such as `$docs-refresh` or `/docs-refresh`.

The workflow will:

- read repository guidance first
- run a stable diff collector
- inspect only the code, schema, generated artifacts, and docs needed to confirm behavior
- update the fewest authoritative docs possible
- stop after explaining what changed or why no doc update was needed

It will not stage, commit, or clean up git state automatically.

## Repository Layout

- `docs-refresh/SKILL.md`: authoritative skill instructions
- `docs-refresh/scripts/collect_changed_context.sh`: diff/context collector
- `docs-refresh/agents/openai.yaml`: optional adapter metadata for OpenAI-compatible surfaces
- `AGENTS.md`: repository navigation for agents
