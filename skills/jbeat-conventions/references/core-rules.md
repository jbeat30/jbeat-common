# Core Rules

## Development Philosophy

- Prioritize DX. Favor code that is easy to read, trace, and maintain.
- Preserve existing public behavior first. Do not arbitrarily change user experience, call contracts, or data flow.
- Use practical abstraction. Separate logic only when actual duplication and maintenance costs are clear.
- Prioritize traceability and intent over reducing the number of lines.
- Prefer a clear structure that fits the current context over vague future reuse.
- Prefer practical simplicity over cleverness or excessive abstraction.
- Aim for maintainable code rather than clever-looking code.
- Control regression risk before optimizing for implementation speed.
- Remove dead code only when unreachable status is confirmed through real data flow, not assumption.

## Change Principles

- Keep changes within the requested scope.
- Make the smallest traceable change that solves the task.
- Respect existing patterns, naming, flow, structure, and error-handling style first.
- Avoid structural reorganization, library replacement, or file relocation without clear justification.
- State assumptions clearly when certainty is not available.

## Judgment Principles

- Do not make arbitrary conclusions about uncertain areas.
- If a safe assumption can be made, state the assumption clearly and proceed.
- Do not present unverified information as fact.
- Do not claim that validation was performed if it was not actually executed.

## Functions and Modules

- Keep one core responsibility per function or module, but avoid fragmentation that hurts readability.
- Handle exceptional cases early to reduce nesting when it improves clarity.
- Keep input, output, and side-effect boundaries visible.
- Handle nullable and optional inputs explicitly.
- Keep success and failure representation consistent within the same layer.
- Prefer official update paths over bypass-style updates.
- Abstract only after actual duplication or maintenance cost is confirmed.
- Do not separate logic solely because it might be needed later.
- Do not separate logic if commonization makes the context harder to understand.
- Choose the simpler method when two approaches solve the same problem equally well.
- Keep one authoritative determination point for a single classification concept.

## Structure and Dependencies

- Change structure only when there is a clear maintenance benefit.
- Evaluate traceability and impact scope before moving code.
- Keep dependency direction consistent.
- Avoid lower-level components depending directly on higher-level policy.
- Do not break module boundaries merely for convenience.
- Avoid circular dependencies and hidden coupling.
- Common modules should not become places where everything is added merely for convenience.

## Duplication and Commonization

- Consider commonization when the same rule genuinely repeats.
- Do not commonize merely to reduce line count.
- Keep similar-looking logic separate when contexts or follow-up behavior differ.
- Reconsider abstraction if it increases the cost of understanding call sites.

## Stability and Quality

### Stability

- Always consider external input and possible failures.
- Do not hide errors. Make recovery strategies or failure impact visible.
- Write normal paths and failure paths separately.
- Be careful not to break existing public behavior through changes.

### Security and Sensitive Information

- Do not expose sensitive information, secrets, or credentials in code or logs.
- Do not trust external data. Consider validation or defensive logic.
- Do not easily allow risky bypass implementations, even as temporary solutions.

### Validation

- When validation is possible, perform static analysis, tests, builds, or runtime checks.
- Clearly state any parts that could not be validated.
- Do not exaggerate validation results.
- Prioritize reviewing paths with a high possibility of regression.

## Error Handling

### User-Facing Messages

- Keep error constants in a single dedicated file (e.g., `errorMessages.ts`). Do not hardcode error strings inline.
- Messages must accurately reflect the situation that actually occurred. A message about "recording failure" must not appear when the failure was a network upload error — misleading messages cause users to retry the wrong action.
- Separate error constants by their semantic meaning, not by their UI location (e.g., `VOICE_RECORDING_FAILED` vs `VOICE_SEND_FAILED`).
- User-facing messages should be clear, non-technical, and actionable: what happened and what the user can do next.
- If the rendering surface supports HTML (e.g., `innerHTML`), `<br>` line breaks are acceptable in error message constants. Document this assumption in the constant definition.

### Developer-Facing Messages

- Console and log messages should identify: the module or function where the error occurred, the technical cause, and any relevant context.
- Example pattern: `[Footer.sendVoiceRecording] S3 upload failed — ${error.message}`
- Do not expose these messages to the user UI. Keep user messages and developer diagnostics strictly separate.
- Use `console.error` for service-breaking errors, `console.warn` for degraded-but-recoverable situations, `console.debug` for flow tracing during development only.

## Data Classification and Responsibility

### Separate Validation Responsibility by Layer

- Separate validation logic by layer only when the two layers genuinely require different validation criteria.
- If both layers only need the same check (e.g., extension-based), use one shared function — do not duplicate.
- Example of genuine difference: upload layer needs MIME type + extension, rendering layer only needs extension. In that case, keep them separate.
- If both layers are satisfied by the same check, one shared function is correct — do not add complexity to the rendering layer just because the upload layer uses more.

### Single Authoritative Classification Function

- Each classification concept must have exactly one function responsible for it. If two functions answer the same question by different methods, eliminate one.
- When removing a redundant classifier, trace every call site to confirm none of them relied on the removed function's different behavior.
- Example: if `isVoiceMessage(parsedData)` is the single authority, then `isVoiceMessageFile(mimeType)` serving the same layer is redundant and must be removed.
