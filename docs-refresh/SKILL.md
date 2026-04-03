---
name: docs-refresh
description: Refresh authoritative docs from current repository state.
---

# Docs Refresh

Use this to close out work by syncing durable docs with the repository's real state. It is not a general writing prompt.

Keep the workflow platform-neutral. Host-specific aliases, launcher syntax, and metadata belong in adapters.

## Principles

- The repository is the record system. Durable knowledge belongs in versioned docs near the code, not in chat.
- `AGENTS.md` is a map, not a manual. Keep it short, stable, and navigational.
- Update the smallest authoritative doc that owns the fact.
- Write for agent readability: explicit headings, scoped docs, concrete invariants, and verifiable claims.
- Prefer documenting the repository's local contract over vague references to opaque upstream behavior.
- Keep current-state docs, reference docs, plans, and history in their own lanes.

## Workflow

1. Read repository guidance first. Start with `AGENTS.md` when present, then follow only the pointers needed to find authority, ownership, freshness rules, and doc-lint requirements.
2. Run `bash scripts/collect_changed_context.sh [repo-root]` from this skill. Use it to gather git status, changed files, diff stat, high-risk areas, and coarse change classes. The script must not modify the target repository.
3. Use the current workspace state as the source of truth: staged diff, unstaged diff, untracked files, and generated artifacts when the repository treats them as authoritative outputs.
4. Inspect only the code, schema, generated artifacts, and current docs needed to confirm the real behavior change.
5. Decide whether documentation edits are needed.
6. When edits are needed, change the fewest existing authoritative docs possible.
7. Touch `AGENTS.md` only when navigation, authority, or a critical pointer is stale.
8. Update plan or debt artifacts only when the repository already uses them and the change materially affected scope, status, or unresolved drift.
9. Stop after explaining what changed or why no doc change was needed.
10. Never run `git add`, `git commit`, or automatic VCS cleanup.

## When To Edit Docs

Default to no documentation edits when the change is limited to:

- tests only
- docs only
- comments only
- formatting only
- internal refactors that do not change public behavior, architecture, state semantics, runtime operation, or external contracts
- dependency churn that does not change the repository's local abstraction, observability, or operator-facing behavior

Force a documentation review when the change touches or plausibly changes:

- API routes, request or response schema, CLI flags, run modes, scheduler behavior, or trigger flow
- core architecture, module boundaries, planner semantics, execution flow, or stability controls
- state tables, schema, persistent fields, or history semantics
- external providers, callbacks, adapters, or contracts
- addition, removal, or rename of a core module, major package, or durable documentation entry point
- a documented core belief, product rule, design principle, or operating invariant
- navigation surfaces such as `AGENTS.md`, `ARCHITECTURE.md`, or docs indexes becoming stale

If the signal is ambiguous, inspect the diff before deciding. Do not update docs just because code changed.

## Resolve Authority

When sources disagree, prefer this order:

1. Code, tests that prove behavior, schema, and authoritative generated artifacts.
2. Current-state architecture, design, product, reliability, security, and reference docs.
3. Navigation docs and indexes such as `AGENTS.md`, `ARCHITECTURE.md`, and `docs/**/index.md`.
4. Plans, decision logs, and history documents.

If the repository defines a stricter order, follow the repository rule. `AGENTS.md` never outranks code or the deeper docs it points to.

## Place Updates

- Update an existing high-authority doc before creating a new file.
- Keep entry pages as maps: short, scannable, and link-heavy.
- Put current behavior, architecture, and operator-facing semantics in current-state docs.
- Put schemas, provider contracts, and protocol details in reference docs.
- Keep plans and debt in plan artifacts, but do not hide current system truth there.
- Leave history docs as history, except for redirects or explicit staleness notes.
- Preserve the repository's existing docs taxonomy instead of inventing a parallel one.
- If the repository lacks a structured docs tree, update the nearest living overview or reference doc instead of creating a new hierarchy.

## Explain The Result

If no documentation change is needed, say so explicitly and explain why.

If documentation changed, report:

- which documents changed
- why those documents were the right convergence points
- whether `AGENTS.md` stayed unchanged on purpose, or why its navigation changed
- why you reused existing docs instead of creating new files
- what remains stale, uncovered, or needs manual follow-up

Stop after the explanation. Do not stage or commit anything.
