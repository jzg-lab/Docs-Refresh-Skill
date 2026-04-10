# Execution Plan Contract

Use this when the request has been classified as actionable execution planning.

The goal is to prevent descriptive plan prose from masquerading as an execution-ready active plan.

## Core Rule

- An active execution plan must be taskified and phase-structured. Section headings alone are not enough.
- Use a plan index plus one markdown file per execution phase under the active plan directory.
- `Step 1`, `Phase 1`, or narrative breakdowns can organize work, but they do not satisfy the contract unless each execution phase has its own markdown file and contains concrete checklist tasks.
- Do not treat scaffold readiness as execution readiness. A repository may be ready for `docs/exec-plans/active/` while a specific draft plan is still too vague to execute.
- If material ambiguity would change scope, routing, dependencies, sequencing, or acceptance, ask the user concise clarifying questions before you taskify the plan.
- If those blockers remain unresolved, mark the work as not execution-ready and persist the blockers in the owning docs instead of inventing fake tasks.

## Minimum Plan Shape

- One index file should define the goal, scope, phase ordering, global constraints, and links to the phase files.
- Each execution phase should live in its own markdown file.
- The index should summarize sequencing and status; the phase files should carry the actionable details.

## Minimum Task Shape

Each phase file should contain checklist-grade tasks that can be advanced, blocked, or accepted independently.

Each task must include:

- `Preconditions`: what must already be true before the task starts
- `Files to change`: the expected files, folders, or docs surfaces that will be edited
- `Expected output`: the artifact or state change the task should produce
- `Done when`: observable acceptance criteria for task completion
- `Blockers`: open dependencies, decisions, or risks that can stop progress
- `Dependencies or parallelism`: what must happen first and what can run in parallel

## Rejection Rule

The plan is not execution-ready if any of these are true:

- it keeps all execution detail in one monolithic markdown document instead of phase files
- it only contains explanatory prose or chapter headings
- it cannot identify the concrete unit of work to complete next
- it cannot say what files or surfaces are expected to change
- it lacks done-when criteria for task completion
- it hides material blockers instead of naming them
- it leaves sequencing or parallelism implicit when that affects execution

## Existing Fuzzy Plans

- If a repository already has a vague execution plan in a single document, do not keep extending that document once the user asks to execute.
- If current docs and explicit user intent give you reliable phase boundaries, split that plan into an index plus phase files under the active plan directory.
- If phase boundaries, dependencies, or acceptance remain materially unclear, ask before you split. Do not invent phase files from guesswork.

## Practical Test

Ask:

- Can someone execute the next unchecked task without inventing missing scope?
- Can they tell when that task is done without another planning pass?
- Can they tell what blocks the task and what can proceed in parallel?

If the answer is no, the plan still belongs in refinement, not active execution.
