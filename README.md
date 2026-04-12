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
- **Specialized agents** — each agent has a single responsibility and clear boundaries.

---

## Agents

Seven specialized agents handle different aspects of the development loop. The Orchestrator routes automatically.

| Agent | Role | File |
|---|---|---|
| **Orchestrator** | Entry point. Routes workflows, enforces approval gates, coordinates handoffs. | [`.github/agents/orchestrator.md`](.github/agents/orchestrator.md) |
| **Inquiry** | Gathers project requirements through 6 structured questions. | [`.github/agents/inquiry.md`](.github/agents/inquiry.md) |
| **Architect** | Designs, creates, and maintains `ARCHITECTURE.md`. | [`.github/agents/architect.md`](.github/agents/architect.md) |
| **Implementor** | Writes production code. Zero scope creep. | [`.github/agents/implementor.md`](.github/agents/implementor.md) |
| **Tester** | Writes and runs all tests. Enforces TDD (red → green). | [`.github/agents/tester.md`](.github/agents/tester.md) |
| **Reviewer** | Audits codebase. Produces ranked change plans. Owns `SIMPLIFICATIONS.md`. | [`.github/agents/reviewer.md`](.github/agents/reviewer.md) |
| **Feature Planner** | Decomposes feature requests. Coordinates Implementor + Tester subagent pairs. | [`.github/agents/feature-planner.md`](.github/agents/feature-planner.md) |

---

## Files

```
.github/
├── copilot-instructions.md   ← Base rules applied to every agent interaction
└── agents/
    ├── orchestrator.md       ← Routes workflows, enforces gates
    ├── inquiry.md            ← Gathers project requirements
    ├── architect.md          ← Designs and maintains ARCHITECTURE.md
    ├── implementor.md        ← Writes production code
    ├── tester.md             ← Writes and runs all tests (TDD)
    ├── reviewer.md           ← Audits codebase, produces change plans
    └── feature-planner.md    ← Decomposes features, coordinates subagents

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
1. Ask six scoping questions (platform, stack, coding practice, state, interaction, purpose) via the **Inquiry Agent**.
2. Produce an `ARCHITECTURE.md` and wait for your approval via the **Architect Agent**.
3. Build only the core loop once approved via the **Implementor Agent** + **Tester Agent**.

### Adding a feature (DEFAULT WORKFLOW ALWAYS APPLIED AFTER NEW PROJECT WORKFLOW)

Point your agent at [`workflows/02-add-feature.md`](workflows/02-add-feature.md).

The agent will:
1. Split your request into individual features via the **Feature Planner Agent**.
2. Check each against `ARCHITECTURE.md` for conflicts via the **Architect Agent**.
3. Get your approval on the plan via the **Orchestrator Agent**.
4. Write tests first, then implement via **Tester Agent** + **Implementor Agent** pairs.
5. Coordinate subagents for multi-phase features via the **Feature Planner Agent**.

### Cleaning up the codebase

Point your agent at [`workflows/03-project-review.md`](workflows/03-project-review.md).

The agent will:
1. Audit the codebase for dead code, duplication, and complexity via the **Reviewer Agent**.
2. Present a ranked change plan and wait for approval.
3. Track every change in `SIMPLIFICATIONS.md` before touching code.
4. Apply changes via the **Implementor Agent**, reverting on test failures.

---

## Communication style

Agents using these instructions apply [caveman compression](https://github.com/wilpel/caveman-compression):

- **Thinking** → maximum compression. Strip grammar, keep facts.
- **Talking to you** → direct sentences. One idea each. No preamble.

See [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for the full style guide.

