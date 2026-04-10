# Workflow: Add Feature

Use this workflow when the core project loop exists and new functionality is requested.

---

## Step 1 — Feature Breakdown

**Goal:** Isolate each feature before touching any code.

Take the user's request and split it into the smallest individually deliverable units. When in doubt, split more.

**Example:**
> Request: "Add user login with Google and remember me."
> Features: (1) Google OAuth login, (2) session persistence ("remember me").

Present the feature list to the user. Confirm the split is correct before continuing.

---

## Step 2 — Architecture Check

**Goal:** Confirm each feature fits the current architecture.

Read `ARCHITECTURE.md`. For each feature:

1. Is it already listed as `[NOT IMPLEMENTED]`? → Implement that entry (do not create a duplicate).
2. Does it conflict with the architecture? → Explain the conflict and recommend a fix.
3. Can existing code be expanded to cover it? → Prefer expansion over adding new files.
4. Does adding this feature make existing code simpler? → Note the simplification.

Report findings to the user. If architectural changes are needed, propose them and wait for approval before continuing.

---

## Step 3 — Approval Gate

Present a concise plan for each feature:
- What will be added or changed.
- Any architectural changes required.
- Any existing code that will be simplified.

**Do not write any code until the user approves this plan.**

---

## Step 4 — Test First, Then Implement

**Only proceed here after explicit user approval.**

For each approved feature (in order):

### 4a. Write tests
- Write unit tests covering the expected behavior of the feature.
- Tests must fail before implementation (red).
- Commit the failing tests.

### 4b. Implement the feature
- Write the simplest code that makes the tests pass.
- Keep it modular — the feature must not tangle with unrelated code.
- Add straightforward comments where the logic is not obvious.
- Commit when all tests pass (green).

### 4c. Update `ARCHITECTURE.md`
- Change the feature status from `[NOT IMPLEMENTED]` to `[IMPLEMENTED]`.
- If it was a new feature (not previously listed), add it with `[IMPLEMENTED]`.

---

## Step 5 — Integration Tests

After all individual features are implemented and their unit tests pass:

- Write higher-level tests that validate the original user request end-to-end.
- These tests should match how a real user would interact with the feature.
- All tests (unit + integration) must pass before reporting completion.

---

## Step 6 — Report Back

Tell the user:
- Which features were added.
- Test counts and pass status.
- Any simplifications made to existing code.
- Next recommended action.
