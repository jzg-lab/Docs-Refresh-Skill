---
name: docs-refresh
description: Refresh authoritative docs through a routed progressive-disclosure workflow.
---

# Docs Refresh

Use this to close out work by syncing durable docs with the repository's real state. It is not a general writing prompt.

Keep the workflow platform-neutral. Host-specific aliases, launcher syntax, and metadata belong in adapters.

## Shared Rules

- The repository is the record system. Durable knowledge belongs in versioned docs near the code, not in chat.
- `AGENTS.md` is a map, not a manual. Keep it short, stable, and navigational.
- Update the smallest authoritative doc that owns the fact.
- Always run the collector before loading detailed workflow instructions.
- Never run `git add`, `git commit`, or automatic VCS cleanup.

## Route First

1. Read repository guidance first. Start with `AGENTS.md` when present, then follow only the pointers needed to find authority, ownership, freshness rules, and doc-lint requirements.
2. Run `bash scripts/collect_changed_context.sh [repo-root]`.
3. Read the collector's `[routing]` section.
4. Open only the matching mode file from `preferred_mode_doc` before acting.
5. Use the current workspace state as the source of truth: staged diff, unstaged diff, untracked files, and generated artifacts when the repository treats them as authoritative outputs.
6. Inspect only the code, schema, generated artifacts, and current docs needed to confirm the real behavior change.
7. Stop after explaining what changed or why no doc change was needed.

## Shared Decision Rules

- Usually no documentation edits for tests-only, docs-only, comments-only, formatting-only, or internal refactors that do not change public behavior, architecture, state semantics, runtime operation, or external contracts.
- Force a documentation review when the change touches APIs, schema, CLI flags, run modes, scheduler behavior, trigger flow, core architecture, state model, external contracts, durable entry points, documented core beliefs, or stale navigation.
- If the signal is ambiguous, inspect the diff before deciding. Do not update docs just because code changed.

## Shared Authority Rules

- Prefer this authority order unless the repository defines a stricter one:
  1. code, tests that prove behavior, schema, and authoritative generated artifacts
  2. current-state architecture, design, product, reliability, security, and reference docs
  3. navigation docs and indexes such as `AGENTS.md`, `ARCHITECTURE.md`, and `docs/**/index.md`
  4. plans, decision logs, and history documents
- `AGENTS.md` never outranks code or the deeper docs it points to.

## Modes

- [modes/bootstrap.md](modes/bootstrap.md): Repos with no real docs system yet. Start with phased growth from `README.md`, `AGENTS.md`, and only add deeper structure when durable domains appear.
- [modes/minimal.md](modes/minimal.md): Repos with core living docs but no split docs taxonomy. Prefer updating those docs and only create the first subtree when it has earned a second durable page.
- [modes/structured.md](modes/structured.md): Repos that already have split docs domains. Preserve the existing taxonomy and converge to the smallest authoritative page.
- [modes/repair.md](modes/repair.md): Repos whose docs system exists but navigation or authority surfaces are stale. Repair the map and indexes before expanding content.

## Explain The Result

If no documentation change is needed, say so explicitly and explain why.

If documentation changed, report:

- which documents changed
- why those documents were the right convergence points
- whether `AGENTS.md` stayed unchanged on purpose, or why its navigation changed
- why you reused existing docs instead of creating new files
- what remains stale, uncovered, or needs manual follow-up

Stop after the explanation. Do not stage or commit anything.
