# Bootstrap Mode

Use this mode when the collector reports `doc_system_mode=bootstrap`, or when manual routing shows there is no split docs tree and no stable docs system beyond `README.md` or a few incidental docs.

The repository does not have a real docs system yet. Grow one in phases instead of generating a full scaffold on first contact.

## Focus

- Create or update `README.md` as the living overview when the repository has no better current-state document yet.
- Create `AGENTS.md` as the map when the repository needs a stable navigation entry point for future agents.
- Capture the initial founding pack before you grow taxonomy: problem frame, system boundaries, key decisions, and validation notes.
- Create `ARCHITECTURE.md` only when the codebase already has multiple durable domains, subsystems, or cross-cutting operational behavior that no longer fits cleanly inside `README.md`.

## Placement Rules

- Prefer the smallest durable foundation over a full docs tree.
- Treat the OpenAI-like docs layout as the eventual target shape, not day-one output.
- Keep `AGENTS.md` short and navigational even during bootstrap.
- Do not create `docs/` subtrees just because the repository is new.
- Do not let this caution override explicit execution intent once the repository already has enough future-work truth to support a real plan.

## Growth Triggers

- Create `docs/design-docs/` when stable design principles or architecture rationale need more than one durable page.
- Create `docs/product-specs/` when user-facing flows or product constraints have split beyond overview docs.
- Create `docs/references/` when schemas, provider contracts, protocol details, or LLM-oriented references need their own reference pages.
- Create `docs/generated/` only when generated facts are treated as authoritative repository outputs.
- Create `docs/exec-plans/` when plans, progress logs, or debt tracking are versioned as first-class artifacts. When you do, scaffold `docs/exec-plans/index.md`, `docs/exec-plans/active/`, and `docs/exec-plans/completed/` so execution work has a stable entry point and lifecycle buckets, and keep empty buckets versioned with placeholder files until real plan docs exist.

## Working Rule

- Treat PRD, SRS, architecture notes, and decision records as responsibilities, not mandatory file names.
- Keep the smallest durable set of docs that answers what the repo solves, owns, excludes, decided, and how it will be validated.
- If decision or validation notes still fit inside `README.md` or `ARCHITECTURE.md`, keep them there until they earn a second durable page.
- Bootstrap should leave the repository with a founding pack, not an empty cathedral of placeholder directories.
- If the user is explicitly asking to execute next and the foundational inputs already constrain implementation, scaffold the minimum `docs/exec-plans/` structure and land the active plan in the same pass instead of stopping at product or design prose.
- That active plan must be phase-structured and taskified. Keep one markdown file per execution phase once work is ready to run.
- If routing intent or execution-critical details are materially unclear, ask the user concise clarifying questions before you generate the active plan.
- If execution is requested but blocked by unresolved choices, create durable blockers in the repository, such as `docs/product-specs/`, `docs/design-docs/`, `OPEN_QUESTIONS.md`, or `ASSUMPTIONS.md`, rather than leaving the ambiguity only in chat.
- Missing `AGENTS.md` is normal here. It is not, by itself, a repair signal.
