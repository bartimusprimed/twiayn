# Workflow: Add Feature

Use this workflow when the core project loop exists and new functionality is requested.
This is the default workflow after project creation is complete.

### Agents Involved

| Step | Agent | File |
|---|---|---|
| Step 0 — Product Brief | Feature Planner Agent | [`.github/agents/feature-planner.md`](../.github/agents/feature-planner.md) |
| Step 1 — Feature Breakdown | Feature Planner Agent | [`.github/agents/feature-planner.md`](../.github/agents/feature-planner.md) |
| Step 2 — Architecture Check | Architect Agent | [`.github/agents/architect.md`](../.github/agents/architect.md) |
| Step 3 — Approval Gate | Orchestrator Agent | [`.github/agents/orchestrator.md`](../.github/agents/orchestrator.md) |
| Step 4a — Write Tests | Tester Agent | [`.github/agents/tester.md`](../.github/agents/tester.md) |
| Step 4b — Implement Feature | Implementor Agent | [`.github/agents/implementor.md`](../.github/agents/implementor.md) |
| Step 4c — Update Architecture | Architect Agent | [`.github/agents/architect.md`](../.github/agents/architect.md) |
| Step 5 — Integration Tests | Tester Agent | [`.github/agents/tester.md`](../.github/agents/tester.md) |
| Step 6 — Report Back | Orchestrator Agent | [`.github/agents/orchestrator.md`](../.github/agents/orchestrator.md) |
| Step 6b — Verify Instrumentation | Feature Planner Agent | [`.github/agents/feature-planner.md`](../.github/agents/feature-planner.md) |
| Subagent Coordination | Feature Planner Agent | [`.github/agents/feature-planner.md`](../.github/agents/feature-planner.md) |

---

## Step 0 — Product Brief

> → Delegates to **[Feature Planner Agent](../.github/agents/feature-planner.md)**

**Goal:** Confirm the problem is worth solving before any feature work begins.

For the incoming request, confirm or collect answers to:

1. **Problem** — Whose pain are we solving, in one sentence?
2. **Why now** — What changed? What evidence or trigger exists?
3. **Assumptions** — What are we taking as true that has not been validated? (2–3 per feature)
4. **Success metric** — The one number we expect to move.
5. **Reversibility** — One-way or two-way door?

If a Product Brief was already provided in the Inquiry Summary, use it — do not re-ask answered questions.

### Gate

Present a **Product Brief** summary to the user. Wait for explicit confirmation — or an explicit "skip with justification" — before proceeding to Step 1.

Acceptable skip justification: typo fix, obvious bug, comment-only change. For anything else, the Product Brief is required.

---

## Step 1 — Feature Breakdown

> → Delegates to **[Feature Planner Agent](../.github/agents/feature-planner.md)**

**Goal:** Isolate each feature before touching any code.

Take the user's request and split it into the smallest individually deliverable units. When in doubt, split more.

**Example:**
> Request: "Add user login with Google and remember me."
> Features: (1) Google OAuth login, (2) session persistence ("remember me").

Present the feature list to the user. Confirm the split is correct before continuing.

---

## Step 2 — Architecture Check

> → Delegates to **[Architect Agent](../.github/agents/architect.md)**

**Goal:** Confirm each feature fits the current architecture.

Read `ARCHITECTURE.md`. For each feature:

1. Is it already listed as `[NOT IMPLEMENTED]`? → Implement that entry (do not create a duplicate).
2. Does it conflict with the architecture? → Explain the conflict and recommend a fix.
3. Can existing code be expanded to cover it? → Prefer expansion over adding new files.
4. Does adding this feature make existing code simpler? → Note the simplification.

Report findings to the user. If architectural changes are needed, propose them and wait for approval before continuing.

---

## Step 3 — Approval Gate

> → Managed by **[Orchestrator Agent](../.github/agents/orchestrator.md)**

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

> → Delegates to **[Tester Agent](../.github/agents/tester.md)**

- Write unit tests covering the expected behavior of the feature.
- Tests must fail before implementation (red).
- Commit the failing tests.

### 4b. Implement the feature

> → Delegates to **[Implementor Agent](../.github/agents/implementor.md)**

- Write the simplest code that makes the tests pass.
- Keep it modular — the feature must not tangle with unrelated code.
- Add straightforward comments where the logic is not obvious.
- Commit when all tests pass (green).

### 4c. Update `ARCHITECTURE.md`

> → Delegates to **[Architect Agent](../.github/agents/architect.md)**

- Change the feature status from `[NOT IMPLEMENTED]` to `[IMPLEMENTED]`.
- If it was a new feature (not previously listed), add it with `[IMPLEMENTED]`.

---

## Step 5 — Integration Tests

> → Delegates to **[Tester Agent](../.github/agents/tester.md)**

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

---

## Step 6b — Verify Instrumentation

> → Delegates to **[Feature Planner Agent](../.github/agents/feature-planner.md)**

After reporting completion, verify that the success metric defined in Step 0 is measurable in the shipped change.

Check:
- [ ] Is the north-star metric observable in production (logs, analytics, counters)?
- [ ] Was instrumentation shipped in the same change as the feature?
- [ ] Is there a defined baseline and time horizon for checking the metric?

If any item is unmet, flag it as a gap in the report. Do not block the merge — but the gap must be named and tracked.

```markdown
## Instrumentation Check

| Metric | Observable? | Shipped with feature? | Baseline defined? | Gap |
|---|---|---|---|---|
| <metric> | Yes / No | Yes / No | Yes / No | <description or "none"> |
```


## Subagent Coordination (Multi-Phase Features)

> → Coordinated by **[Feature Planner Agent](../.github/agents/feature-planner.md)** using **[Implementor](../.github/agents/implementor.md) + [Tester](../.github/agents/tester.md)** pairs

When implementing large features with multiple interconnected sub-components:

1. **Phase Planning** — Break the feature into phase-ordered units; identify blocking dependencies
2. **Critical Path** — Identify phases that block others; run these sequentially
3. **Parallel Work** — Run independent phases in parallel to maximize velocity
4. **Subagent Model** — Each subagent owns one complete feature phase:
   - Writes tests first (red state)
   - Implements the feature (green state)
   - Updates ARCHITECTURE.md with `[IMPLEMENTED]` status
   - Reports back with test results and any code simplifications discovered
5. **Integration Tests** — After all phases complete, write end-to-end tests that validate the full feature request
6. **Final Report** — Summarize which phases completed, test counts/pass status, and any architectural simplifications

**Example workflow for "Target detail window system":**
- Phase A (blocking): Expand Target model with properties → Test target property schema
- Phase B (blocking on A): Module filtering logic → Test filter rules per target
- Phase C (blocking on A): Detail window component → Test window rendering
- Phase D (blocking on C): Terminal emulator → Test emulator lifecycle
- Phase E (parallel after B): MITRE filtering UI → Test filter interaction
- Phase F (parallel): Theme refresh → Test color contrast
- **All phases complete** → Write integration test for full "click target → see detail window → run module" flow
- **Report**: 6 features implemented, 28 tests pass, no simplifications, ready for merge