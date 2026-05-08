# Naming Conventions

## Naming Rules

### Basic Principles

- Use names that reveal role and intent.
- Prefer clarity over abbreviation, even when names become longer.
- If unit, scope, or source is important, reflect it in the name.
- Use `is`, `has`, `can`, `should`, or `needs` for booleans when appropriate.
- Use plural or clearly collective names for arrays, maps, and sets.
- Use `handle` for event handlers when the project follows that pattern.
- Use verbs that reveal role for creation (`create*`), conversion, and lookup (`get*`) functions.
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
- Avoid excessive separation if the definition becomes too far from the usage site and makes tracing difficult.
