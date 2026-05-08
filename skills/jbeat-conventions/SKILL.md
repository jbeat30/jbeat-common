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
  - Edit
  - Write
  - Bash
  - Glob
  - Grep
---

# Jbeat Conventions

Common working conventions for all jbeat repositories — backend, frontend, library, and infrastructure.
Project-specific rules are provided by each repository's local instruction documents. This skill is a shared layer on top of those.

---

## Step 0 — Verify settings.json configuration

Before loading conventions, check that `~/.claude/settings.json` has the required plugin entries.

Run:
```
echo "$HOME/.claude/settings.json"
```

Then read the file. Check for both of the following:

**A. enabledPlugins**
```json
"enabledPlugins": {
  "jbeat-conventions@jbeat-plugins": true
}
```

**B. extraKnownMarketplaces**
```json
"extraKnownMarketplaces": {
  "jbeat-plugins": {
    "source": {
      "source": "github",
      "repo": "jbeat30/jbeat-conventions"
    }
  }
}
```

If either entry is missing, add it now using Edit (file exists) or Write (file absent). Preserve all existing keys.

Report the result in Korean:
- Entry added → `⚙️ settings.json에 jbeat-conventions 항목을 추가했습니다.`
- Already present → `✅ settings.json 설정 확인 완료`

---

## Step 1 — Load and apply conventions

Read only the reference files needed for the current task.

| File | Read when |
|------|-----------|
| [references/core-rules.md](references/core-rules.md) | Development philosophy, change principles, function/module design, structure, error handling |
| [references/naming-conventions.md](references/naming-conventions.md) | Naming rules, variable and constant naming |
| [references/comment-conventions.md](references/comment-conventions.md) | Comment style, JSDoc vs inline, when to add comments |
| [references/language-conventions.md](references/language-conventions.md) | Language policy: Korean default for comments and reports |
| [references/quality-checklist.md](references/quality-checklist.md) | Pre-work checks, stability criteria, prohibited actions, final self-check |
| [references/reporting-format.md](references/reporting-format.md) | Writing the final result report and validation summary |

---

## Step 2 — Apply core workflow rules

1. **Identify scope** — Determine requested scope, behavior to preserve, and minimal safe change before acting.
2. **Respect structure** — Follow existing structure, naming, flow, and error-handling style before introducing new abstractions.
3. **Protect contracts** — Do not change public behavior, call contracts, data flow, user experience, or meaningful execution order without explicit request.
4. **Keep side effects visible** — Place side effects intentionally. Avoid hidden bypasses and speculative rewrites.
5. **Separate facts from assumptions** — Do not claim validation that was not actually executed.
6. **Report in Korean** — Write result reports in Korean by default. Use another language only when the user explicitly requests it.

---

## No Project-Specific Assumptions

Do not infer repository-specific architecture, product contracts, or framework policies from this skill alone.
Each repository provides those constraints separately through its own local instruction documents.
