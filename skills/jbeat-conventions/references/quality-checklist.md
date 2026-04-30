# Quality Checklist

## Before Starting Work

- Identify the requested scope.
- Identify which existing behavior must be preserved.
- Define the minimal necessary change.
- Check for conflicts with existing code patterns and local repository rules.
- Review whether execution order, initialization order, dependency order, rendering order, or event flow must be preserved.
- Review possible type, lint, build, runtime, and side-effect impact.
- Distinguish what can be validated now from what cannot.

## During Work

- Keep changes small, traceable, and within scope.
- Preserve file structure unless there is a clear reason to change it.
- Preserve existing naming and utility usage unless directly related to the requested change.
- Do not introduce abstractions without confirmed need.
- Do not remove existing guards, validations, fallback logic, or error handling without clear justification.
- Keep side effects visible and intentional.
- Maintain type safety without hiding problems through `any`, weak assertions, or optional-chaining abuse.
- Maintain lint and build stability without weakening the original structure.
- Preserve meaningful execution order unless change is explicitly required.

## Quality and Stability Criteria

- Type errors must not be introduced.
- Lint errors must not be introduced.
- Build errors must not be introduced.
- Runtime errors must not be introduced.
- Unintended side effects must not be introduced.
- Existing public behavior must be preserved unless the request explicitly changes it.
- Existing call contracts must be preserved unless the request explicitly changes them.
- Existing data flow must be preserved unless the request explicitly changes it.
- Existing user experience must be preserved unless the request explicitly changes it.
- Normal and failure paths must not change unintentionally.

## Validation Rules

- Execute static checks, tests, builds, or runtime verification when feasible.
- Report only validations that were actually executed.
- Separate executed validations from unexecuted validations.
- Mark unvalidated items clearly and explain why they were not validated.
- Distinguish assumptions from verified facts.
- Prioritize regression-prone paths when validation range is limited.

## Prohibited Actions

- Do not perform large-scale refactoring outside the requested scope.
- Do not implement based on unverified assumptions presented as fact.
- Do not hide errors with temporary workarounds.
- Do not force personal preferences over repository rules.
- Do not change public behavior, contracts, data flow, or user experience without explicit request.
- Do not move files, reorganize modules, or replace libraries without clear justification.
- Do not disable type checks, lint rules, tests, or build checks merely to make a change look successful.
- Do not change order-sensitive code unless the reason and expected impact are clear.
- Do not add dead-code guards for scenarios confirmed impossible through data flow analysis.

## Final Self-Check

- Confirm existing intent was preserved.
- Confirm change scope stayed minimal.
- Confirm side effects were reviewed.
- Confirm type, lint, build, and runtime risks were reviewed.
- Confirm execution order, initialization order, dependency order, rendering order, and event flow were preserved unless intentionally changed.
- Confirm public behavior, call contracts, data flow, and user experience were preserved unless intentionally changed.
- Confirm executed and unexecuted validations were reported separately.
- Confirm traceability and maintainability improved or at least did not regress.
- Confirm dead code introduced or exposed by this change has been removed.
- Confirm error messages accurately reflect the actual failure scenario (user-facing vs developer-facing separated).
- Confirm classification logic is consolidated into a single authoritative function per concept.
