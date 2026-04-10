# Minimal Mode

Use this mode when the collector reports `doc_system_mode=minimal`, or when manual routing shows there is no split docs tree but the repository already has stable living docs.

The repository already has core living docs, but it has not yet split into a durable docs taxonomy.

## Focus

- Prefer updating the existing living docs first: `README.md`, `AGENTS.md`, `ARCHITECTURE.md`, and cross-cutting top-level docs such as `DESIGN.md`, `FRONTEND.md`, `PRODUCT_SENSE.md`, `RELIABILITY.md`, `SECURITY.md`, `PLANS.md`, or `QUALITY_SCORE.md`.
- Use `PRODUCT_SENSE.md` for problem framing, `DESIGN.md` plus `FRONTEND.md` for current design truth, and `PLANS.md`, `QUALITY_SCORE.md`, `RELIABILITY.md`, and `SECURITY.md` for validation and operational truth before inventing new pages.
- Keep `AGENTS.md` small and navigational.
- Use `ARCHITECTURE.md` or another current-state doc for durable system truth that no longer belongs in the overview.
- Strengthen the founding pack before creating the first subtree.
- Fill gaps in problem frame, system boundaries, key decisions, contract notes, and validation notes in the existing docs before you create new folders.
- Do not let that bias suppress an execution-ready planning request once the repository already has enough product and design truth to constrain implementation.

## Creation Rules

- Create the first domain-specific subtree only when it has earned a second durable page in that domain.
- Keep exploratory future work in the existing product or design docs. When execution tracking becomes first-class enough to earn `docs/exec-plans/`, put actionable work under `docs/exec-plans/active/` instead of bloating `PLANS.md`.
- First split targets: `docs/design-docs/` for design rationale, `docs/product-specs/` for user-facing behavior, `docs/references/` for schemas and contracts, `docs/generated/` for authoritative generated facts, and `docs/exec-plans/` for versioned plans. When you create `docs/exec-plans/`, scaffold `index.md`, `active/`, and `completed/`, and keep empty buckets versioned with placeholder files.
- Explicit execute-now intent plus a sufficient future-work baseline such as PRD plus spec, or equivalent scope, constraints, contracts, and acceptance notes, means the planning domain has been earned. Create the minimum `docs/exec-plans/` scaffold and land the active plan instead of returning only advice.
- If the user wants to execute but the missing inputs would make the plan fake, persist those blockers in the owning docs surfaces instead of deferring them to chat.

## Working Rule

- A minimal repo should converge by strengthening its existing docs, not by exploding into a premature taxonomy.
- A minimal repo should still materialize execution structure when the user has already crossed from refinement into implementation planning.
- A repo can be `minimal` even if `AGENTS.md` is absent, as long as other durable current-state docs already exist.
