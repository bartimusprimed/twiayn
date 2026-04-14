# TWIAYN — This Workflow Is All You Need

An AI-augmented development pipeline with a human-in-the-loop at every decision point.

---

## What this is

A set of agent instruction files that define a consistent, opinionated development loop. Any AI coding agent working on a project that uses these instructions follows the same workflow — from blank repo to production-ready codebase.

TWIAYN covers two failure modes:

- **Building it wrong** — caught by TDD, approval gates, modular architecture, and code review.
- **Building the wrong thing** — caught by the product layer: problem framing, assumption surfacing, minimum viable scope, tradeoff naming, outcome-based "done," instrumentation, and decision logging.

The instructions enforce:
- **Problem-first thinking** — confirm the problem and success metric before any code is written.
- **Simple language** — agents communicate concisely (see [Communication Style](.github/copilot-instructions.md)).
- **Approval gates** — no code is written until the human approves a plan.
- **Modular design** — core loop first, features added incrementally.
- **Test-first development** — tests written before implementation.
- **Specialized agents** — each agent has a single responsibility and clear boundaries.

---

## The Product Layer

Before any engineering work begins, every non-trivial request passes a five-question Pre-Flight Checklist:

| Question | Why it matters |
|---|---|
| **Problem** — Whose pain are we solving? | Prevents building for the wrong user |
| **Why now** — What changed? | Prevents work that isn't timely or evidence-backed |
| **Scope** — Smallest change that tests the hypothesis | Prevents scope creep and gold-plating |
| **Success metric** — The one number we expect to move | Prevents "merged" being mistaken for "done" |
| **Reversibility** — One-way or two-way door? | Prevents costly decisions made without visibility |

### When to skip this rigor

| Change type | Apply |
|---|---|
| Typo, comment, obvious one-liner | None — just do it |
| Bug fix, small internal refactor | Problem + Scope + Success metric |
| New user-facing feature | All five checklist items |
| Architecture, public API, data model, pricing | All five + explicit one-way-door sign-off |

### The Seven Product Principles (from [product-mode](https://github.com/sohaibt/product-mode))

| # | Principle | What it prevents |
|---|---|---|
| 1 | Frame the Problem Before the Solution | Building for the wrong user |
| 2 | Make Assumptions & Unknowns Visible | Silent guessing |
| 3 | Ship the Minimum Viable Change | Scope creep, gold-plating |
| 4 | Name the Tradeoffs | Invisible costs |
| 5 | Define Done by Outcome, Not Output | "Merged" mistaken for "done" |
| 6 | Instrument Before You Ship | Shipping blind |
| 7 | Log the Decision, Flag Reversibility | Repeating mistakes, calcifying defaults |

---

## Agents

Seven specialized agents handle different aspects of the development loop. The Orchestrator routes automatically.

| Agent | Role | File |
|---|---|---|
| **Orchestrator** | Entry point. Routes workflows, enforces approval gates, coordinates handoffs. | [`.github/agents/orchestrator.md`](.github/agents/orchestrator.md) |
| **Inquiry** | Gathers project requirements through 11 structured questions (6 technical + 5 product brief). | [`.github/agents/inquiry.md`](.github/agents/inquiry.md) |
| **Architect** | Designs and maintains `ARCHITECTURE.md`. Logs decisions in `DECISIONS.md`. | [`.github/agents/architect.md`](.github/agents/architect.md) |
| **Implementor** | Writes production code. Zero scope creep. | [`.github/agents/implementor.md`](.github/agents/implementor.md) |
| **Tester** | Writes and runs all tests. Enforces TDD (red → green). | [`.github/agents/tester.md`](.github/agents/tester.md) |
| **Reviewer** | Audits codebase. Produces ranked change plans. Owns `SIMPLIFICATIONS.md`. | [`.github/agents/reviewer.md`](.github/agents/reviewer.md) |
| **Feature Planner** | Validates product brief. Decomposes features. Coordinates Implementor + Tester subagent pairs. Verifies instrumentation. | [`.github/agents/feature-planner.md`](.github/agents/feature-planner.md) |

---

## Files

```
.github/
├── copilot-instructions.md   ← Base rules applied to every agent interaction
└── agents/
    ├── orchestrator.md       ← Routes workflows, enforces gates
    ├── inquiry.md            ← Gathers 6 technical + 5 product-brief requirements
    ├── architect.md          ← Designs ARCHITECTURE.md, logs decisions in DECISIONS.md
    ├── implementor.md        ← Writes production code
    ├── tester.md             ← Writes and runs all tests (TDD)
    ├── reviewer.md           ← Audits codebase, produces change plans
    └── feature-planner.md    ← Validates product brief, decomposes features, verifies instrumentation

workflows/
├── 01-new-project.md         ← Blank repo → working core loop (Phase 0: Product Brief)
├── 02-add-feature.md         ← Core loop → new feature (Step 0: Product Brief, Step 6b: Instrumentation check)
└── 03-project-review.md      ← Cleanup / optimization pass

templates/
├── architecture.md           ← Template for ARCHITECTURE.md (includes problem statement, success metrics, assumptions)
└── decision-log.md           ← ADR-lite template for DECISIONS.md
```

---

## Usage

### Starting a new project

Point your agent at [`workflows/01-new-project.md`](workflows/01-new-project.md).

The agent will:
1. Confirm the problem statement and success metric via the **Pre-Flight Checklist** (Phase 0).
2. Ask eleven scoping questions (6 technical + 5 product brief) via the **Inquiry Agent** (Phase 1).
3. Produce an `ARCHITECTURE.md` and wait for your approval via the **Architect Agent** (Phase 2).
4. Build only the core loop once approved via the **Implementor Agent** + **Tester Agent** (Phase 3).

### Adding a feature (DEFAULT WORKFLOW ALWAYS APPLIED AFTER NEW PROJECT WORKFLOW)

Point your agent at [`workflows/02-add-feature.md`](workflows/02-add-feature.md).

The agent will:
1. Confirm the product brief (problem, why now, assumptions, success metric, reversibility) via the **Feature Planner Agent** (Step 0).
2. Split your request into individual features via the **Feature Planner Agent** (Step 1).
3. Check each against `ARCHITECTURE.md` for conflicts via the **Architect Agent** (Step 2).
4. Get your approval on the plan via the **Orchestrator Agent** (Step 3).
5. Write tests first, then implement via **Tester Agent** + **Implementor Agent** pairs (Steps 4–5).
6. Verify the success metric is measurable in the shipped change via the **Feature Planner Agent** (Step 6b).

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

