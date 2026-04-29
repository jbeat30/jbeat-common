# Reporting Format

Use Korean by default unless the user explicitly requests another language.

## Final Report Order

1. Summary
2. Key changes
3. Quality and stability check
4. Validation results
5. Remaining risks or items that need confirmation

## Quality and Stability Check Items

- Type error possibility
- Lint error possibility
- Build error possibility
- Runtime error possibility
- Possibility of unintended side effects
- Whether execution order changed
- Whether initialization order changed
- Whether dependency order changed
- Whether rendering order changed
- Whether event flow changed
- Whether existing public behavior was preserved
- Whether existing call contracts were preserved
- Whether existing data flow was preserved
- Whether existing user experience was preserved
- Whether normal paths and failure paths were preserved

## Validation Reporting Rules

- Separate validations that were executed from validations that were not executed.
- Do not claim that type checking, linting, testing, building, or runtime verification was performed unless it actually was.
- If validation was not possible, state the reason explicitly.
- Distinguish facts from assumptions.
- Do not exaggerate validation results.
- State remaining risks clearly without minimizing them.

## Reporting Style

- Prioritize actual changes and impact scope over theory.
- Explain by file, module, or feature unit when that improves traceability.
- Keep the report concise but explicit about what is verified and what is not.
