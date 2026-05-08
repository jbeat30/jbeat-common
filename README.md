# jbeat-conventions

Shared Jbeat engineering conventions packaged as a Claude Code plugin.

Guides implementation, review, refactoring, debugging, and planning with a consistent convention set across all jbeat repositories.

## What It Covers

- Scope control and minimal safe changes
- Preserving existing behavior and contracts
- Naming and comment conventions
- Regression-risk awareness
- Honest validation and reporting

## Installation

```
plugins install jbeat-conventions@jbeat-plugins
```

## Update

```
plugins update jbeat-conventions@jbeat-plugins
```

## Commands

```
/jbeat-setup   # Initial setup — run once after installation
/jbeat-apply   # Manual mode — explicitly activate all conventions
```

## Reference Files

| File | Purpose |
|------|---------|
| `references/core-rules.md` | Change principles, function design, error handling |
| `references/naming-conventions.md` | Variable, constant, and module naming rules |
| `references/comment-conventions.md` | When and how to write comments |
| `references/language-conventions.md` | Language policy (Korean default for reports) |
| `references/quality-checklist.md` | Pre-work checks and final self-review |
| `references/reporting-format.md` | Result report and validation summary format |
