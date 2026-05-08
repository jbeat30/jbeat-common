# Comment Conventions

Write in Korean by default. See [language-conventions.md](language-conventions.md) for the full language policy.

Concise, consistent, focused on intent and constraints — not implementation details. Not a translation of the code.

## Basic Style

- End with noun-style expressions: `담당`, `반환`, `수행`, `정의`, `검증`.
- Avoid verbose sentences like `~을 담당하고 있습니다` or `~하는 로직입니다`.
- Focus on **Why** (business rules) and **What** (core functionality), not How.
- Do not end comments with a period.

## Comment Placement

| Position | Style | When to use |
|----------|-------|-------------|
| Exported function or class | `/** @description ...\n * @param ...\n * @returns ... */` | Public-facing functions and classes |
| Interface or type field | trailing `//` | When field purpose is not obvious from the name |
| Internal branch or block | `// WHY one-liner` | Policy rationale, non-obvious conditions |
| Variable or constant | `const x = ...; // 보충 설명` | When name alone is insufficient |
| Private internal helper | `//` or omit | Only when name does not convey enough |

**JSDoc (`/** ... */`)** is for exported functions and classes only. Not for file headers or internal details.
**Inline `//`** is for all in-body comments: branch rationale, variable clarification, block labels.
**Do not mix styles**: `/** */` on a variable is wrong. `//` on an exported function header is wrong.

## JSDoc Details

- Document parameters, return values, side effects, and exceptions when they are important.
- Use `@param`, `@returns`, `@throws`, `@example`, `@note`, `@description` to reduce understanding cost — not to increase tag count.
- Do not write multi-line JSDoc for simple utilities where name and type signature are self-explanatory.

## Inline Comment Details

- Short explanations for variables, state values, constants, and simple branch intent use `//`, not `/** ... */`.
- Add short trailing comments to important variables or constants when the name alone does not convey origin, unit, or policy (e.g., `const retryLimit = 3; // 서버 정책 기준`).
- For complex branches, explain the reason and policy background behind the branch rather than merely restating the condition.

## When Comments Are Needed

- Policy-based branches or exception handling
- External system constraints or data contracts
- Reasons for performance optimization, bypass handling, or caching
- Cases where intent is difficult to understand from naming alone
- Complex state changes or side effects
- Fallback logic for legacy data formats (e.g., `// 레거시 data.url 폴백`)

## Avoid These Comments

- Comments that restate the code
- State descriptions that can easily become outdated
- Personal impressions or speculative notes
- Long procedural explanations that will drift from implementation
- Explanations unlikely to be updated when implementation changes
