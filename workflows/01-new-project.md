# Workflow: New Project

Use this workflow when starting from a blank or near-blank repository.

### Agents Involved

| Phase | Agent | File |
|---|---|---|
| Phase 0 — Product Brief | Inquiry Agent | [`.github/agents/inquiry.md`](../.github/agents/inquiry.md) |
| Phase 1 — Inquiry | Inquiry Agent | [`.github/agents/inquiry.md`](../.github/agents/inquiry.md) |
| Phase 2 — Architecture | Architect Agent | [`.github/agents/architect.md`](../.github/agents/architect.md) |
| Phase 3 — Core Loop | Implementor Agent + Tester Agent | [`.github/agents/implementor.md`](../.github/agents/implementor.md), [`.github/agents/tester.md`](../.github/agents/tester.md) |
| All phases | Orchestrator Agent | [`.github/agents/orchestrator.md`](../.github/agents/orchestrator.md) |

---

## Phase 0 — Product Brief

> → Delegates to **[Inquiry Agent](../.github/agents/inquiry.md)**

**Goal:** Confirm the problem worth solving before any technical scoping begins.

Ask the user exactly these five questions. Get answers before moving to Phase 1.

### Required questions

1. **Problem** — Whose pain are we solving, in one sentence?
2. **Why now** — What changed? What evidence or trigger exists? What is the cost of waiting?
3. **Assumptions** — What are we taking as true that has not been validated?
4. **Success metric** — The one number we expect to move.
5. **Reversibility** — Is this a one-way door (costly to undo) or a two-way door (easily reversed)?

### Gate

Present the answers back to the user as a **Product Brief** summary. Wait for explicit confirmation that the problem statement and success metric are correct.

**Do not proceed to Phase 1 until the user confirms the Product Brief.**

---

## Phase 1 — Inquiry

> → Delegates to **[Inquiry Agent](../.github/agents/inquiry.md)**

**Goal:** Understand the project before touching any code.

Ask the user exactly these questions. Get answers before moving on.

### Required questions

1. **Purpose** — What problem does this solve? Who uses it?
2. **Platform** — Local machine, cloud hosted, embedded, or mixed?
3. **Tech stack** — Web app, native binary, interpreted scripts, or other?
4. **Coding practice** — OOP, functional, procedural, or mixed?
5. **State management** — User config, database, reactive UI, in-memory, or none?
6. **Interaction mechanism** — Web browser, CLI, native UI, game engine, API, or other?

### Inquiry rules

- Ask all six questions in one message. Do not drip them one at a time.
- If an answer is ambiguous, ask one follow-up to clarify.
- Do not suggest a stack until you have all answers.

---

## Phase 2 — Architecture Deliverable

> → Delegates to **[Architect Agent](../.github/agents/architect.md)**

**Goal:** Produce a written plan the user approves before any code is written.

### What to produce

Fill in the [architecture template](../templates/architecture.md) with:

- Project purpose (one paragraph, plain language).
- Chosen platform, stack, coding practice, state approach, interaction mechanism.
- Core loop description — the single minimal cycle that makes the project functional.
- Feature list — mark each feature as `[CORE]` or `[NOT IMPLEMENTED]`.
- Proposed file/folder scaffolding.

### Rules

- The deliverable is a Markdown document committed to the repo as `ARCHITECTURE.md`.
- Present the deliverable to the user. **Do not scaffold or write code yet.**
- Wait for explicit approval or feedback.
- Apply any requested changes. Re-present if changes are significant.
- Only proceed to Phase 3 after the user says "approved" or equivalent.

---

## Phase 3 — Core Loop Implementation

> → Delegates to **[Implementor Agent](../.github/agents/implementor.md)** (build core loop) then **[Tester Agent](../.github/agents/tester.md)** (smoke test)

**Goal:** Build only the core loop. Nothing else.

### Rules

- Implement only features marked `[CORE]` in the approved architecture.
- Structure the project modularly from day one — each concern in its own module.
- After scaffolding: run the project and confirm the core loop works end-to-end.
- If the tech stack supports a test framework, write at minimum one smoke test for the core loop.
- Commit, then ask the user to verify the running project before continuing.

### What not to do

- Do not implement `[NOT IMPLEMENTED]` features.
- Do not add "nice to haves" or future-proofing beyond what the core loop requires.
- Do not refactor or optimize at this stage.

### Handoff

Once the core loop is confirmed working, tell the user:

> "Core loop is running. Use the [Add Feature workflow](02-add-feature.md) to add anything beyond this."
