# Core Rules

## Development Philosophy

- Prioritize DX. Favor code that is easy to read, trace, and maintain.
- Preserve existing public behavior first. Do not arbitrarily change user experience, call contracts, or data flow.
- Prefer practical simplicity over cleverness or excessive abstraction.
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

## Naming Rules

### Basic Principles

- Use names that reveal role and intent.
- Prefer clarity over abbreviation, even when names become longer.
- Use `is`, `has`, `can`, `should`, or `needs` for booleans when appropriate.
- Use plural or clearly collective names for arrays, maps, and sets.
- Use `handle` for event handlers when the project follows that pattern.
- Preserve external field names and contracts separately from internal names when required.

### External Data

- Data that must preserve external system specifications should be managed separately from internal names.
- If the internal representation differs from the external representation, clearly define the conversion point.
- Do not arbitrarily transform external contracts in a way that creates confusion.
- Do not carelessly rename external field names just to match internal preferences.

## Variables and Constants

- Treat values as immutable unless reassignment is actually needed.
- Avoid temporary names with weak meaning.
- Group related declarations at the top of their scope when that improves scanability.
- Add a short trailing `//` comment only when name alone does not explain origin, unit, or policy.
- Promote unclear literals, thresholds, keys, and policy values into named constants when doing so improves traceability.

## Functions and Modules

- Keep one core responsibility per function or module, but avoid fragmentation that hurts readability.
- Handle exceptional cases early to reduce nesting when it improves clarity.
- Keep input, output, and side-effect boundaries visible.
- Handle nullable and optional inputs explicitly.
- Keep success/failure representation consistent within the same layer.
- Prefer official update paths over bypass-style updates.
- Abstract only after actual duplication or maintenance cost is confirmed.
- Choose the simpler method when two approaches solve the same problem equally well.
- Keep one authoritative determination point for a single classification concept.

## Comment Style

Write in Korean unless the project requires another language. Concise, consistent, focused on intent and constraints — not implementation details. Not a translation of the code.

### Basic Style

- End with noun-style expressions: `담당`, `반환`, `수행`, `정의`, `검증`.
- Avoid verbose sentences like `~을 담당하고 있습니다` or `~하는 로직입니다`.
- Focus on **Why** (business rules) and **What** (core functionality), not How.
- Do not end comments with a period.

### Comment Placement

| Position | Style | When to use |
|----------|-------|-------------|
| Exported function / class | `/** @description ...\n * @param ...\n * @returns ... */` | All public-facing functions and classes |
| Interface / type field | trailing `//` | When field purpose is not obvious from the name |
| Internal branch or block | `// WHY one-liner` | Policy rationale, non-obvious conditions |
| Variable / constant (intent unclear) | `const x = ...; // 보충 설명` | When name alone is insufficient |
| Private internal helper | `//` or omit | Only when name does not convey enough |

**JSDoc** (`/** ... */`) — exported functions and classes only. Not for file headers or internal details.
**Inline `//`** — all in-body comments: branch rationale, variable clarification, block labels.
**Do not mix styles**: `/** */` on a variable is wrong. `//` on an exported function header is wrong.

### When Comments Are Needed

- Policy-based branches or exception handling
- External system constraints or data contracts
- Reasons for performance optimization, bypass handling, or caching
- Cases where intent is difficult to understand from naming alone
- Complex state changes or side effects
- Fallback logic for legacy data formats (e.g., `// 레거시 data.url 폴백`)

### JSDoc Details

- Document parameters, return values, side effects, and exceptions when important.
- Use `@param`, `@returns`, `@throws`, `@example`, `@note`, `@description` to reduce understanding cost — not to increase tag count.
- Do not write multi-line JSDoc for simple utilities where name and type signature are self-explanatory.

### Inline Comment Details

- Short explanations for variables, state values, constants, and simple branch intent use `//`, not `/** ... */`.
- For complex branches, explain the reason and policy background, not just the condition.

### Avoid These Comments

- Comments that restate the code
- State descriptions that can easily become outdated
- Personal impressions or speculative notes
- Long procedural explanations that will drift from implementation
- Explanations unlikely to be updated when implementation changes

## Structure and Dependencies

- Change structure only when there is a clear maintenance benefit.
- Evaluate traceability and impact scope before moving code.
- Keep dependency direction consistent.
- Avoid lower-level components depending directly on higher-level policy.
- Do not break module boundaries merely for convenience.
- Avoid circular dependencies and hidden coupling.

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

## Error Handling and Data Responsibility

### User-Facing Messages

- Keep error messages centralized rather than hardcoding them inline.
- Ensure messages match the actual failure that occurred.
- Separate user-facing messages from developer-facing logs.
- Treat external input as untrusted and preserve defensive validation.

### Developer-Facing Messages

- Console/log messages should identify: module or function, technical cause, relevant context.
- Use `console.error` for service-breaking errors, `console.warn` for degraded-but-recoverable, `console.debug` for flow tracing only.

### Data Classification

- Separate validation logic by layer only when the layers truly require different criteria.
- Keep each classification concept owned by one authoritative function. Eliminate duplicates.
