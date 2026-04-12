# TWIAYN — This Workflow Is All You Need

An AI-augmented development pipeline with a human-in-the-loop at every decision point.

---

## What this is

A set of agent instruction files that define a consistent, opinionated development loop. Any AI coding agent working on a project that uses these instructions follows the same workflow — from blank repo to production-ready codebase.

The instructions enforce:
- **Simple language** — agents communicate concisely (see [Communication Style](.github/copilot-instructions.md)).
- **Approval gates** — no code is written until the human approves a plan.
- **Modular design** — core loop first, features added incrementally.
- **Test-first development** — tests written before implementation.

---

## Files

```
.github/
└── copilot-instructions.md   ← Base rules applied to every agent interaction

workflows/
├── 01-new-project.md         ← Blank repo → working core loop
├── 02-add-feature.md         ← Core loop → new feature (TDD)
└── 03-project-review.md      ← Cleanup / optimization pass

templates/
└── architecture.md           ← Template for ARCHITECTURE.md (filled in per project)
```

---

## Usage

### Starting a new project

Point your agent at [`workflows/01-new-project.md`](workflows/01-new-project.md).

The agent will:
1. Ask six scoping questions (platform, stack, coding practice, state, interaction, purpose).
2. Produce an `ARCHITECTURE.md` and wait for your approval.
3. Build only the core loop once approved.

### Adding a feature (DEFAULT WORKFLOW ALWAYS APPLIED AFTER NEW PROJECT WORKFLOW)

Point your agent at [`workflows/02-add-feature.md`](workflows/02-add-feature.md).

The agent will:
1. Split your request into individual features.
2. Check each against `ARCHITECTURE.md` for conflicts.
3. Get your approval on the plan.
4. Write tests first, then implement.
5. Spawn subagents when needed. (Should prompt you with the workflow before doing so, but watch your usage just incase)

### Cleaning up the codebase

Point your agent at [`workflows/03-project-review.md`](workflows/03-project-review.md).

The agent will:
1. Audit the codebase for dead code, duplication, and complexity.
2. Present a ranked change plan and wait for approval.
3. Track every change in `SIMPLIFICATIONS.md` before touching code.

---

## Communication style

Agents using these instructions apply [caveman compression](https://github.com/wilpel/caveman-compression):

- **Thinking** → maximum compression. Strip grammar, keep facts.
- **Talking to you** → direct sentences. One idea each. No preamble.

See [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for the full style guide.

