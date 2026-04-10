---
name: docs-refresh
description: Refresh authoritative docs through a routed progressive-disclosure workflow.
---

# Docs Refresh

Use this to keep durable docs authoritative for both current truth and explicit planned work. Sync implemented behavior from the repository's real state, and land execution-ready future work in durable plan artifacts. It is not a general writing prompt and should not confuse a folder tree with real project understanding.

Keep the workflow platform-neutral. Host-specific aliases, launcher syntax, and metadata belong in adapters.

## Shared Rules

- Classify the user request before mode routing: current-state refresh, future-spec refinement, or actionable execution planning.
- Treat explicit intent to "start implementation", "do the next step", "land the file structure", "split phases", or equivalent execute-now language as actionable execution planning, not as a request for more chat-only refinement.
- The repository is the record system. Durable knowledge belongs in versioned docs near the code, not in chat.
- `AGENTS.md` is a map, not a manual. Keep it short, stable, and navigational.
- Update the smallest authoritative doc that owns the fact.
- Treat PRD, SRS, architecture notes, decision logs, contract references, and validation notes as responsibilities, not mandatory filenames.
- If the repository already has sanctioned docs domains such as `docs/design-docs/`, `docs/product-specs/`, `docs/references/`, `docs/generated/`, `docs/exec-plans/`, `DESIGN.md`, `FRONTEND.md`, `PLANS.md`, `PRODUCT_SENSE.md`, `QUALITY_SCORE.md`, `RELIABILITY.md`, or `SECURITY.md`, use them before inventing new folders.
- In mixed or custom docs systems, map each split domain to a role such as current-state, reference, planning, validation, decision, history, or archive before you normalize anything. Healthy custom domains can stay in place until drift, duplicate authority, or execution planning makes standardization necessary.
- When normalizing ad hoc custom docs folders into the sanctioned taxonomy, preserve the previous source material under `old_docs/` unless the repository already defines a stricter archive location.
- Prefer the bundled collector before manual routing, but do not block on it if it cannot be run from the skill directory.
- Never run `git add`, `git commit`, or automatic VCS cleanup.

## Route First

1. Read repository guidance first. Start with `AGENTS.md` when present, then follow only the pointers needed to find authority, ownership, freshness rules, and doc-lint requirements.
2. Resolve the directory containing this `SKILL.md`, then classify the request before mode routing: current-state refresh, future-spec refinement, or actionable execution planning.
3. If you can run bundled files from the skill directory, run the collector from that skill directory against `[repo-root]`. Do not assume the target repo has its own `scripts/collect_changed_context.sh`.
4. If the collector succeeds, read `[repo_layout]`, `[planning]`, `[routing]`, and `[knowledge]`. Treat `repo_taxonomy_mode`, `taxonomy_health`, `role_map`, `normalization_candidates`, `migration_candidates`, `plan_readiness`, `stale_plan_placement`, and `active_plan_target` as the routing contract. Open only the file named by `preferred_mode_doc`. Load [references/foundation-checklist.md](references/foundation-checklist.md) when `knowledge_phase` is not `operations` or `foundation_gaps` is non-empty.
5. If the collector is unavailable, cannot be resolved from the skill directory, or shell execution is unavailable, manually collect `git status --short`, changed files, diff stat, the docs layout, obvious custom split domains under `docs/`, and the core foundation surfaces.
6. Use the manual routing fallback below to choose exactly one mode file, then infer the foundation phase with the checklist reference.
7. Use the current workspace state as the source of truth for implemented behavior, but use explicit user intent plus repository constraints for future-work plan artifacts.
8. Inspect only the code, schema, generated artifacts, and current docs needed to confirm the real behavior change or the real planning constraint.
9. Stop after explaining what changed or why no doc change was needed.

## Manual Routing Fallback

Use this only when the bundled collector cannot be run from the skill directory or its routing output is unavailable.

- `bootstrap`: no split docs tree exists, and the repository does not yet have a stable docs system beyond `README.md` or a few incidental docs. `README.md` only is still `bootstrap`.
- `minimal`: no split docs tree exists, but the repository already has one or more stable living docs such as `AGENTS.md`, `ARCHITECTURE.md`, or durable top-level current-state docs. A repo can be `minimal` even if `AGENTS.md` is absent.
- `structured`: split docs domains already exist, either in the standard taxonomy or as healthy custom domains under `docs/` whose role map is still usable.
- `repair`: a real docs system exists, but its map or authority is broken enough that content edits would deepen drift.
- Missing `AGENTS.md` alone does not mean `repair`.
- Sparse docs alone do not mean `repair`.
- When in doubt between `minimal` and `repair`, choose `minimal` unless the repository already has a real docs system whose map is broken.

## Foundation Axis

After you choose a mode, use the collector's `knowledge_phase` when available. If you are in fallback mode, infer the phase manually.

- `framing`: the repository still needs a durable problem frame, success criteria, or map before deeper doc taxonomy is useful.
- `design`: the overview exists, but system boundaries, invariants, or important decisions are still implicit.
- `contracts`: the repository's APIs, schemas, generated interfaces, or external contracts are evolving faster than its reference docs.
- `operations`: the core frame and design exist; remaining gaps are validation, rollout notes, reliability, security, quality scorecards, or stale navigation.
- Before creating new folders, close the highest-risk gap among problem frame, system boundaries, decision log, contract docs, and validation plan.
- Use [references/foundation-checklist.md](references/foundation-checklist.md) to pressure-test those gaps and decide whether the answer belongs in an existing doc, a new section, or a newly earned subtree.

## Shared Decision Rules

- Usually no documentation edits for tests-only, docs-only, comments-only, formatting-only, or internal refactors that do not change public behavior, architecture, state semantics, runtime operation, or external contracts.
- Force a documentation review when the change touches APIs, schema, CLI flags, run modes, scheduler behavior, trigger flow, core architecture, state model, external contracts, durable entry points, documented core beliefs, or stale navigation.
- If the signal is ambiguous, inspect the diff before deciding. Do not update docs just because code changed.
- Use current-state docs for what is true today, plan artifacts for explicit committed future work, and product or design docs for future behavior that is still being shaped.
- When the user explicitly wants the next step executed and the repository already has enough future-work truth to constrain implementation, do not stop at prose. Land the execution structure in the repository in the same pass: scaffold or reuse the planning surface, create the active plan, and encode file structure, phase breakdown, acceptance points, and blockers there.
- Planning split: Do not confuse plan scaffolding with validation truth. Create or update `docs/exec-plans/active/` only for execution-ready work; otherwise tighten `PRODUCT_SENSE.md`, `DESIGN.md`, `FRONTEND.md`, `docs/product-specs/`, or `docs/design-docs/`.
- In `bootstrap` and `minimal` repos, explicit execution intent plus an adequate problem frame and implementation-defining inputs such as PRD plus spec, or equivalent scope, constraints, contracts, and acceptance notes, is enough to earn the first planning subtree.
- If execution intent is explicit but key decisions are still missing, create or update the owning future-work docs with durable blockers in the repository, such as `docs/design-docs/`, `docs/product-specs/`, `OPEN_QUESTIONS.md`, or `ASSUMPTIONS.md`, instead of replying with chat-only uncertainty.
- If the collector reports `repo_taxonomy_mode=custom` or `repo_taxonomy_mode=mixed`, reuse healthy custom domains when their `role_map` is clear. Normalize only the smallest conflicting surfaces identified by `normalization_candidates` or `migration_candidates`.
- Plan lifecycle: In structured repos with a standard `docs/exec-plans/` tree, audit `stale_plan_placement` even when git is clean. Move done-marked plans from the root or `active/` into `completed/` in the same pass, including shared baseline or prerequisite plans once they are accepted. Update indexes, umbrella docs, and cross-links so path semantics and content semantics stay aligned. Treat `completed in content, still in active/` as a lifecycle inconsistency to fix immediately.
- Treat `old_docs/` as a legacy archive, not as a convergence point for new truth.
- In `bootstrap` and `minimal` repos, strengthen the founding pack before expanding taxonomy. A new docs subtree is the last move, not the first.
- Exception: when the user is clearly asking to execute next and the key planning inputs already exist, the planning subtree is no longer premature. Create the minimum `docs/exec-plans/` scaffold needed and place the active plan in the same pass.
- When a repository has earned `docs/exec-plans/` as a durable plan domain, keep that subtree navigable. The default scaffold is `docs/exec-plans/index.md`, `docs/exec-plans/active/`, and `docs/exec-plans/completed/`.
- When the default `docs/exec-plans/` scaffold is missing and you can run bundled files from the skill directory, use [scripts/scaffold_exec_plans.sh](scripts/scaffold_exec_plans.sh) against `[repo-root]`. It creates the scaffold without overwriting existing plan docs and keeps empty lifecycle buckets versioned with placeholder files.
- If explicit planning intent targets `docs/exec-plans/` and the collector reports `plan_readiness=needs-scaffold` or `plan_readiness=needs-standardization`, create the minimum standard scaffold needed and land the active plan in the same pass. When you migrate a custom planning surface, preserve the prior material under `old_docs/`.

## Shared Authority Rules

- For future-work planning, explicit user intent plus the repository's current documented constraints can justify durable plan updates even when no code diff exists. The authority order below is for current-state truth.
- Prefer this authority order unless the repository defines a stricter one:
  1. code, tests that prove behavior, schema, and authoritative generated artifacts
  2. current-state architecture, design, product, reliability, security, and reference docs
  3. navigation docs and indexes such as `AGENTS.md`, `ARCHITECTURE.md`, and `docs/**/index.md`
  4. plans, decision logs, and history documents
- `AGENTS.md` never outranks code or the deeper docs it points to.

## Modes

- [modes/bootstrap.md](modes/bootstrap.md): no real docs system yet; grow a founding pack before adding taxonomy.
- [modes/minimal.md](modes/minimal.md): core living docs exist, but no split docs tree yet; strengthen those docs first.
- [modes/structured.md](modes/structured.md): split docs domains already exist; preserve the taxonomy and converge to the owning page.
- [modes/repair.md](modes/repair.md): the docs system exists but the map is stale; repair navigation and authority before expanding content.
- Each mode file supports both collector-selected routing and the manual fallback rules above.

## Explain The Result

If no documentation change is needed, say so explicitly and explain why.

If documentation changed, report:

- which documents changed
- why those documents were the right convergence points
- whether the change stayed in current-state docs, future-spec docs, or an active execution plan
- any role-map, normalization, or migration decision used for custom docs domains
- whether `AGENTS.md` stayed unchanged on purpose, or why its navigation changed
- why you reused existing docs instead of creating new files
- whether any legacy custom docs were preserved under `old_docs/`
- what remains stale, uncovered, or needs manual follow-up

Stop after the explanation. Do not stage or commit anything.
