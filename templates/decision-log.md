# Decision Log: <Project Name>

> Maintained by the [Architect Agent](../.github/agents/architect.md).
> Every non-trivial architectural choice gets an entry here.
> One-way-door decisions require explicit user sign-off before the choice is enacted.

---

## How to Use

1. The Architect Agent appends an entry for every non-trivial decision.
2. Two-way-door decisions: decide fast, move on.
3. One-way-door decisions: surface to the Orchestrator → get explicit user sign-off → then proceed.
4. Each entry must include a revisit trigger so decisions don't calcify into unquestioned defaults.

**Non-trivial decisions include:** public APIs, data schemas, pricing, core UX patterns, external integrations, authentication mechanisms, deployment targets.

---

<!-- Copy the template below for each new decision. -->

## Decision: [short title]

**Date:** YYYY-MM-DD
**Context:** <!-- What problem are we solving? What constraints apply? -->
**Options considered:**
- A: <!-- description -->
- B: <!-- description -->
- C: <!-- description -->

**Choice:** <!-- Option X -->
**Reason:** <!-- Why this option over the others -->
**Reversibility:** <!-- one-way door / two-way door -->
**Revisit trigger:** <!-- The metric, date, or condition that reopens this decision -->

---
