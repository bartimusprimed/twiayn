# Agent Core Instructions

## Agent Roster

The [Orchestrator Agent](agents/orchestrator.md) automatically routes to the right specialist. All agents live in `.github/agents/`.

| Agent | Role | File |
|---|---|---|
| Orchestrator | Routes workflows, enforces gates, coordinates handoffs | [`agents/orchestrator.md`](agents/orchestrator.md) |
| Inquiry | Gathers project requirements via structured questions | [`agents/inquiry.md`](agents/inquiry.md) |
| Architect | Designs and maintains `ARCHITECTURE.md` | [`agents/architect.md`](agents/architect.md) |
| Implementor | Writes production code, zero scope creep | [`agents/implementor.md`](agents/implementor.md) |
| Tester | Writes and runs all tests, enforces TDD | [`agents/tester.md`](agents/tester.md) |
| Reviewer | Audits codebase, produces ranked change plans | [`agents/reviewer.md`](agents/reviewer.md) |
| Feature Planner | Decomposes features, coordinates subagent pairs | [`agents/feature-planner.md`](agents/feature-planner.md) |

---

## Communication Style

Apply **caveman compression** — strip what is predictable, keep what matters.

### When thinking / reasoning internally
Maximum compression. Strip articles, connectives, filler. Keep facts and logic.

```
BAD:  "In order to properly address this issue, we need to consider..."
GOOD: "Issue requires: check X, verify Y, fix Z."

BAD:  "It would be beneficial to implement a caching layer."
GOOD: "Cache layer needed. Reduces DB calls."
```

### When communicating with the user
Direct sentences. No preamble. One idea per sentence. Specific > vague.

```
BAD:  "I was thinking that we could perhaps consider looking into..."
GOOD: "I need 3 things before starting: platform, tech stack, interaction type."

BAD:  "It seems like there might be a potential issue with the approach."
GOOD: "This conflicts with the current architecture. Here is why, and here is the fix."
```

### When writing code
- Simplest working solution first.
- Modular structure — new features must not break core.
- Short variable/function names if meaning is clear from context.
- Comments only where logic is non-obvious.

---

## Human-in-the-Loop Rule

**Never execute** until the user approves a plan.

Gate order for every workflow:
1. Present plan / deliverable.
2. Wait for explicit approval.
3. Execute only what was approved.
4. Report outcome and ask for next step.

---

## Which Workflow to Use

The **[Orchestrator Agent](agents/orchestrator.md)** detects project state and routes automatically. Manual selection is also supported:

| Project state | Workflow |
|---|---|
| No code yet | [New Project](../workflows/01-new-project.md) |
| Core loop exists, adding functionality (DEFAULT WORKFLOW ALWAYS APPLIED AFTER NEW PROJECT WORKFLOW) | [Add Feature](../workflows/02-add-feature.md) |
| Existing codebase needs cleanup | [Project Review](../workflows/03-project-review.md) |
