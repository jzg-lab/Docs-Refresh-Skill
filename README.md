# Docs Refresh

`docs-refresh` is a portable documentation-refresh workflow packaged in a reusable prompt/skill layout. It treats the repository as the record system, starts from `AGENTS.md` as a map, inspects current workspace state, and uses progressive disclosure to load only the workflow branch that matches the repository's current docs maturity.

The core workflow lives in plain Markdown at `docs-refresh/SKILL.md`, so it can be adapted to any agent or prompt system that can reuse structured instructions.

## Portable Use

Use `docs-refresh/SKILL.md` as the canonical workflow instructions in your own agent stack.

If shell execution is available, also provide `docs-refresh/scripts/collect_changed_context.sh` so the workflow can gather consistent git context before deciding whether docs need to change.

The workflow is routed. The top-level skill stays short, runs the collector first, reads `doc_system_mode`, and then follows the matching mode file under `docs-refresh/modes/`.

Any platform-specific aliasing, registration, or metadata should be treated as an adapter layer around the core workflow, not as part of the workflow contract itself.

## Optional OpenAI/Codex Adapter

This repository also includes an optional OpenAI-compatible adapter under `docs-refresh/agents/openai.yaml`.

If you want to install it into a Codex/OpenAI-compatible skill directory, use the host platform's installer against the `docs-refresh/` path in this repository.

## Use

Invoke the workflow however your host platform exposes reusable prompts or skills. In OpenAI/Codex-compatible surfaces, the packaged aliases can be wired to names such as `$docs-refresh` or `/docs-refresh`.

The workflow will:

- read repository guidance first
- run a stable diff collector
- read the collector's routing mode before loading detailed instructions
- inspect only the code, schema, generated artifacts, and docs needed to confirm behavior
- update the fewest authoritative docs possible
- stop after explaining what changed or why no doc update was needed

It will not stage, commit, or clean up git state automatically.

## Modes

- `bootstrap`: new or under-documented repos that need a minimal map and living overview before any deeper taxonomy exists
- `minimal`: repos with core docs such as `AGENTS.md`, `ARCHITECTURE.md`, or cross-cutting top-level docs, but no split docs tree yet
- `structured`: repos that already have split doc domains and should preserve that taxonomy
- `repair`: repos whose docs system exists but whose navigation or authority surfaces are stale enough to fix first

New repositories should grow in phases. `docs-refresh` should not generate a full docs tree on first contact unless the repository has already earned those durable domains.

## Eventual Shape

This is an illustrative final-state example, not a required bootstrap scaffold:

```text
AGENTS.md
ARCHITECTURE.md
docs/
├── design-docs/
│   ├── index.md
│   ├── core-beliefs.md
│   └── ...
├── exec-plans/
│   ├── active/
│   ├── completed/
│   └── tech-debt-tracker.md
├── generated/
│   └── db-schema.md
├── product-specs/
│   ├── index.md
│   ├── new-user-onboarding.md
│   └── ...
├── references/
│   ├── design-system-reference-llms.txt
│   ├── nixpacks-llms.txt
│   ├── uv-llms.txt
│   └── ...
├── DESIGN.md
├── FRONTEND.md
├── PLANS.md
├── PRODUCT_SENSE.md
├── QUALITY_SCORE.md
├── RELIABILITY.md
└── SECURITY.md
```

## Repository Layout

- `docs-refresh/SKILL.md`: authoritative skill instructions
- `docs-refresh/modes/`: routed workflow branches selected by the collector
- `docs-refresh/scripts/collect_changed_context.sh`: diff/context collector
- `docs-refresh/scripts/test_collect_changed_context_routing.sh`: shell smoke test for collector routing
- `docs-refresh/agents/openai.yaml`: optional adapter metadata for OpenAI-compatible surfaces
- `AGENTS.md`: repository navigation for agents
