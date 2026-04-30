---
name: jbeat-conventions
classification: capability
classification-reason: "Provides shared engineering conventions as a reference layer. Not a step-by-step workflow — it defines rules the agent applies during any task."
deprecation-risk: none
description: |
  Apply Jbeat engineering conventions across all repositories.
  Use when an AI agent needs to preserve existing behavior, keep changes narrowly scoped,
  respect existing patterns, apply Jbeat naming and comment rules, review regression risk,
  and report executed versus unexecuted validation clearly.
  Applies to: code review, implementation, refactoring, debugging, planning.
  Triggers: jbeat, convention, naming rule, comment style, regression, scope control, validation report
argument-hint: "(no argument needed — auto-applies conventions)"
user-invocable: true
allowed-tools:
  - Read
  - Glob
  - Grep
---

# Jbeat Conventions

Common working conventions for all jbeat repositories — backend, frontend, library, and infrastructure.
Project-specific rules are provided by each repository's local instruction documents. This skill is a shared layer on top of those.

---

## Core Workflow

1. **Identify scope** — Determine requested scope, behavior to preserve, and minimal safe change before acting.
2. **Respect structure** — Follow existing structure, naming, flow, and error-handling style before introducing new abstractions.
3. **Protect contracts** — Do not change public behavior, call contracts, data flow, user experience, or meaningful execution order without explicit request.
4. **Keep side effects visible** — Place side effects intentionally. Avoid hidden bypasses and speculative rewrites.
5. **Separate facts from assumptions** — Do not claim validation that was not actually executed.
6. **Report in Korean** — Write result reports in Korean by default. Use another language only when the user explicitly requests it.

---

## Load References Selectively

Read only the file needed for the current task.

| File | Read when |
|------|-----------|
| [references/core-rules.md](references/core-rules.md) | Naming, comment style, function/module design, duplication policy, error handling |
| [references/quality-checklist.md](references/quality-checklist.md) | Pre-work checks, stability criteria, prohibited actions, final self-check |
| [references/reporting-format.md](references/reporting-format.md) | Writing the final result report and validation summary |

---

## No Project-Specific Assumptions

Do not infer repository-specific architecture, product contracts, or framework policies from this skill alone.
Each repository provides those constraints separately through its own local instruction documents.
