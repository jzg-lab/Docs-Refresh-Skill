---
name: docs-refresh
description: Sync repository documentation by treating the repository as the record system, using AGENTS.md as a map, reading the current workspace git diff, and updating the smallest authoritative docs needed to keep agent-readable project knowledge fresh.
---

# Docs Refresh

Treat this as a task-closing documentation synchronizer for agent-readable repositories, not a general writing tool.

The core workflow should remain platform-neutral. Aliases, launcher syntax, and host-specific metadata are optional adapters around these instructions, not part of the workflow contract.

## Core Stance

- The repository is the record system. Durable project knowledge belongs in versioned docs near the code, not in ad hoc chat context.
- Give the agent a map, not a manual. `AGENTS.md` should stay short, stable, and navigational.
- Optimize for progressive disclosure. Start from small entry points and follow links to the right depth instead of loading giant instruction blobs.
- Optimize for agent readability. Prefer stable structure, explicit headings, scoped documents, concrete invariants, and verifiable claims.
- Treat plans as first-class artifacts. Execution plans, decision logs, and debt trackers matter, but they do not replace current-state docs.
- If a constraint matters for future reasoning and is only present in task context, promote it into the right repository doc instead of assuming future agents will inherit the chat.
- Prefer inspectable local abstractions over hand-wavy references to opaque upstream behavior. If the repository has reimplemented or wrapped a dependency for clarity, document the local contract.
- Write docs so lint, CI, and doc-gardening automation can verify freshness, cross-links, ownership, and structure.

## Workflow

1. Read repository guidance before touching docs.
   - Read `AGENTS.md` when present, but treat it as a table of contents unless the repository explicitly says otherwise.
   - Read `ARCHITECTURE.md`, relevant index pages, and only the current docs needed to locate the right authority.
   - Respect any documented authority order, ownership model, freshness checks, and doc-lint rules.
2. Run `scripts/collect_changed_context.sh` from this skill against the current repository root.
3. Read only the code, schema, generated artifacts, and current docs needed to confirm the real behavior change.
4. Decide whether documentation updates are actually needed.
5. When updates are needed, edit the fewest existing authoritative documents possible.
6. Touch `AGENTS.md` only when repository navigation changed or an important pointer is missing or stale.
7. If the work changed plan status, decision logs, or tracked debt, update the existing plan or debt artifact in addition to current-state docs, not instead of them.
8. Update an existing index, quality tracker, or freshness scorecard only when the repository already uses one and your change materially affects it.
9. Stop after edits and explain the result.
10. Never run `git add`, `git commit`, or automatic VCS cleanup.

Use the current workspace state as the source of truth:

- Read unstaged diff.
- Read staged diff.
- Include untracked files.
- Include generated artifacts when the repository treats them as authoritative outputs.
- Do not limit analysis to the most recent commit.

## Decide Whether To Edit Docs

Default to no documentation edits when the change is limited to:

- Tests only.
- Documentation only.
- Comments only.
- Formatting only.
- Internal refactors that do not change public behavior, architecture, state semantics, runtime operation, or external contracts.
- Private dependency churn that does not change the repository's local abstraction, observability, or operator-facing behavior.

Force a documentation review when the change touches or plausibly changes:

- API routes, request or response schema, CLI flags, run modes, scheduler behavior, or trigger flow.
- Core architecture, module boundaries, planner semantics, execution flow, or stability controls.
- State tables, schema, persistent fields, history semantics, or high-frequency field meaning.
- External providers, callbacks, adapters, contracts, or integration-specific constraints.
- Addition, removal, or rename of a core module, major package, or durable documentation entry point.
- A documented core belief, product rule, design principle, or operating invariant.
- The repository's navigation surfaces such as `AGENTS.md`, `ARCHITECTURE.md`, or docs indexes becoming stale because files moved or ownership changed.

When the file-level signal is ambiguous, inspect the diff before deciding. Do not update docs just because code changed.

## Keep `AGENTS.md` Small

- Do not turn `AGENTS.md` into an encyclopedia.
- Prefer roughly 100 lines of navigation, constraints, and pointers over dense prose.
- Store durable detail in structured docs, then link to it from `AGENTS.md`.
- If `AGENTS.md` contains detailed operational truth that belongs elsewhere, move that content into the right doc and leave a pointer behind.
- Only add new `AGENTS.md` content when it improves navigation or clarifies authority.

## Apply Occam's Razor

Prefer convergence over expansion.

- Update an existing high-authority document before creating a new file.
- Keep entry pages as maps; do not turn them into sprawling body documents.
- Merge overlapping explanations into one durable page when they describe the same problem domain.
- Create a new document only when the topic is clearly independent, stable, and worth indexing.
- Keep design, current facts, reference material, plans, generated artifacts, and history separate, but with the fewest layers possible.
- Do not move current facts into history documents.
- Do not use plan documents or history documents as the primary place to describe current system behavior.

## Optimize For Agent Readability

- Prefer explicit headings, durable nouns, and repository-local terminology over implied context and chat-only jargon.
- State current behavior and invariants before deep rationale.
- Keep cross-links tight: maps should point to leaf docs, and leaf docs should link back to their index when that pattern already exists.
- Preserve or improve validation markers, freshness notes, ownership metadata, and status fields when the repository already uses them.
- Prefer boring, composable descriptions of local abstractions over summaries that defer understanding to opaque third-party behavior.
- When you find stale docs you cannot fully repair, leave an explicit follow-up in the repository's existing debt or plan tracker instead of letting drift stay implicit.

## Resolve Authority

When sources disagree, prefer this order:

1. Code, tests that prove behavior, schema, and generated artifacts the repository treats as authoritative.
2. Current-state architecture, design, product, reliability, security, and reference docs.
3. Navigation docs and indexes such as `AGENTS.md`, `ARCHITECTURE.md`, and `docs/**/index.md`.
4. Active plans, completed plans, decision logs, and history documents.

If the repository defines a stricter order in `AGENTS.md`, `ARCHITECTURE.md`, or a core guide, follow the repository rule.

`AGENTS.md` never outranks code or the deeper docs it points to.

## Adapt To Repository Layout

If the repository contains a structured docs tree, adapt to it instead of inventing a parallel system. Common targets include:

- `docs/core/` when the repository keeps current-state behavior and architecture in one consolidated docs area.
- `docs/design-docs/` for stable design beliefs, architecture rationale, core principles, and validated design records.
- `docs/product-specs/` for product behavior, flows, constraints, and user-facing semantics.
- `docs/references/` for schemas, provider contracts, protocol details, library notes, and LLM-oriented reference material.
- `docs/generated/` for generated facts such as schema dumps; regenerate or align them only when the repository expects them to stay in sync.
- `docs/exec-plans/active/`, `docs/exec-plans/completed/`, and `docs/exec-plans/tech-debt-tracker.md` for execution plans, progress, decisions, and debt.
- `docs/history/` for historical context, migrations, prior decisions, and explicit staleness notices only.
- Top-level guides such as `DESIGN.md`, `FRONTEND.md`, `PLANS.md`, `PRODUCT_SENSE.md`, `QUALITY_SCORE.md`, `RELIABILITY.md`, and `SECURITY.md` for cross-cutting maps, scorecards, and standards.

Apply these placement rules:

- Put current behavior, architecture, and operator-facing semantics in the repository's current-state docs.
- Put external contracts, schemas, provider details, and protocol facts in reference docs.
- Keep indexes and top-level maps short, scannable, and link-heavy.
- Keep active debt tracking and forward-looking plans in plan docs.
- Leave history docs as historical context only, except for redirects or explicit staleness notes.
- Keep `ARCHITECTURE.md` aligned with the current system shape, but do not duplicate lower-level reference detail there.

If the repository does not have that split structure, update the nearest living overview and reference documents instead of creating a new documentation tree.

## Treat Plans As First-Class Artifacts

- Small changes may only need current-state docs.
- Complex work should keep its execution plan, progress notes, and decision log in version control when the repository already follows that pattern.
- Update plan status when implementation materially changed scope, completed milestones, introduced debt, or reversed a prior assumption.
- Do not bury current system behavior only inside a plan. If something is now true of the system, update the current-state doc as well.

## Use The Diff Collector

Run:

```bash
bash scripts/collect_changed_context.sh [repo-root]
```

Use the script output to collect:

- `git status --short`
- Unstaged and staged changed files
- Untracked files
- Diff stat
- High-risk implementation areas
- Compact change classes such as `only-tests`, `only-docs`, `api`, `runtime`, `state-model`, `external-contracts`

Treat the script as a stable context collector only. The script must not modify the target repository.

## Explain The Result

If no documentation change is needed, say so explicitly and explain why.

If documentation changed, report:

- Which documents changed.
- Why those documents were the right convergence points in the repository's record system.
- Whether `AGENTS.md` stayed unchanged on purpose, or why its navigation needed adjustment.
- Why new files were not created, if that was a plausible alternative.
- What changed in the docs.
- What is still not covered, still stale, or still needs manual follow-up.

Stop after the explanation. Do not stage or commit anything.
