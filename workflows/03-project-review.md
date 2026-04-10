# Workflow: Project Review / Cleanup

Use this workflow when the codebase needs optimization or simplification — not new features.

---

## Step 1 — Audit

Read the entire codebase. Look for:

- **Dead code** — functions, variables, imports never used.
- **Duplication** — logic repeated in more than one place.
- **Overcomplexity** — a simpler structure would do the same job.
- **Naming** — unclear names that require a comment to understand.
- **Test gaps** — code paths with no test coverage.
- **Dependency bloat** — libraries that could be replaced with a few lines of code.

Do not change anything yet.

---

## Step 2 — Present the Plan

Write a change plan and show it to the user before touching any code.

For each proposed change include:
- **What** — the file and the specific thing being changed.
- **Why** — concrete benefit (fewer lines, removed duplication, faster, clearer).
- **Risk** — low / medium / high and a one-line reason.

Group changes by risk level. Present high-risk changes separately and wait for individual approval on those.

**Do not proceed until the user approves the plan.**

---

## Step 3 — Track Changes

Create `SIMPLIFICATIONS.md` in the repo root (or append to it if it already exists).

For each change you are about to make, add an entry:

```markdown
## YYYY-MM-DD — <short title>

**File:** `path/to/file.ext`
**Change:** What was changed and why.
**Revert:** What to restore if a regression is found.
```

Commit `SIMPLIFICATIONS.md` before making any code changes.

---

## Step 4 — Apply Changes

Apply one logical group at a time. After each group:

1. Run the full test suite.
2. If tests fail, revert the group and document the failure in `SIMPLIFICATIONS.md`.
3. If tests pass, commit with a message that matches the entry in `SIMPLIFICATIONS.md`.

---

## Step 5 — Report Back

Tell the user:
- What was changed.
- Before/after metrics where measurable (line count, test count, etc.).
- Anything that was skipped and why.
- Link to `SIMPLIFICATIONS.md` for the full record.
