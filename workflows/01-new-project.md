# Workflow: New Project

Use this workflow when starting from a blank or near-blank repository.

---

## Phase 1 — Inquiry

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
