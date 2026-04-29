---
name: jbeat-common
description: Apply Jbeat common engineering conventions across all repositories. Use when an AI agent needs to preserve existing behavior, keep changes narrowly scoped, respect existing patterns, apply Jbeat naming and comment rules, review regression risk, and report executed versus unexecuted validation clearly. Applies to code review, implementation, refactoring, debugging, and planning.
when_to_use: Trigger when requests mention jbeat conventions, naming rules, comment style, regression risk, scope control, validation reporting, or preserving existing behavior.
argument-hint: "[no argument needed]"
user-invocable: true
---

# Jbeat Common

Common working conventions for all Jbeat repositories.
Use this as a shared reference layer on top of repository-specific rules.

## Core Workflow

1. Identify requested scope, preserved behavior, and the minimal safe change before acting.
2. Follow existing structure, naming, flow, and error-handling style before introducing new abstractions.
3. Do not change public behavior, call contracts, data flow, user experience, or meaningful execution order without explicit request.
4. Keep side effects visible. Avoid hidden bypasses and speculative rewrites.
5. Separate verified facts from assumptions.
6. Report results in Korean by default unless the user explicitly requests another language.

## Load References Selectively

Read only the file needed for the current task.

| File | Read when |
|------|-----------|
| [references/core-rules.md](references/core-rules.md) | Naming, comment style, function or module design, duplication policy, error handling |
| [references/quality-checklist.md](references/quality-checklist.md) | Pre-work checks, stability criteria, prohibited actions, final self-check |
| [references/reporting-format.md](references/reporting-format.md) | Final result report and validation summary |

## No Project-Specific Assumptions

Do not infer repository-specific architecture, product contracts, or framework policies from this skill alone.
Repository-local rules must come from that repository's own instruction files.
