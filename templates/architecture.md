# Architecture: <Project Name>

> This document is the single source of truth for project architecture.
> Update it whenever features are added, changed, or removed.
> All agents must read this before writing any code.

---

## Purpose

<!-- One paragraph. Plain language. What does this project do and who uses it. -->

---

## Problem Statement

<!-- One sentence: whose pain are we solving, and what changes for them when this project succeeds.
     Example: "Freelance developers waste hours manually tracking client invoices; this project automates that." -->

---

## Success Metrics

| Metric | Value |
|---|---|
| North-star metric | <!-- The one number we expect to move --> |
| Baseline | <!-- Current value (from data, not vibes) --> |
| Expected direction & size | <!-- e.g. +5% conversion, –20% latency --> |
| Time horizon | <!-- When we check: 7 days? 30? --> |
| Guardrail metrics | <!-- What must NOT get worse --> |

---

## Assumptions

| Assumption | Status | Owner |
|---|---|---|
| <!-- State the assumption --> | `validated` / `assumed` / `unknown` | |

---

## Configuration

| Dimension | Decision | Notes |
|---|---|---|
| Platform | <!-- local / cloud / embedded --> | |
| Tech stack | <!-- web / native binary / scripts / other --> | |
| Coding practice | <!-- OOP / functional / procedural / mixed --> | |
| State management | <!-- config file / database / reactive UI / in-memory / none --> | |
| Interaction mechanism | <!-- web / CLI / native UI / game engine / API --> | |

---

## Core Loop

<!-- Describe the single minimal cycle that makes the project functional.
     Example: "User runs CLI command → app reads config → app calls API → result printed to stdout." -->

---

## Features

| Feature | Status | Module / File | Notes |
|---|---|---|---|
| <!-- Core feature --> | `[CORE]` | | |
| <!-- Planned feature --> | `[NOT IMPLEMENTED]` | | |
| <!-- Completed feature --> | `[IMPLEMENTED]` | | |

---

## File Structure

```
project-root/
├── <!-- list files and folders with one-line descriptions -->
```

---

## Dependencies

| Name | Version | Purpose |
|---|---|---|
| | | |

---

## Change Log

| Date | Change | Author |
|---|---|---|
| | Initial architecture created | |

---

## Decision Log

Non-trivial architectural decisions are tracked in [`DECISIONS.md`](../DECISIONS.md) using the [decision log template](decision-log.md). See that file for the full record of one-way-door and significant two-way-door decisions.
