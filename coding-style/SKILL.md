---
name: coding-style
description: Enforce consistent, simple, and maintainable coding practices across the project
---

# Coding Style Guidelines

## Core Principles
- Prefer simplicity over complexity
- Avoid over-engineering and premature abstractions
- Write code for humans first, machines second
- Optimize only when necessary and measurable
- Be explicit rather than implicit

## Consistency with Existing Code
- Always prioritize existing project conventions over ideal patterns
- If the codebase uses a specific naming pattern (e.g., `data`), follow it
- Do not rename variables or refactor just for style consistency
- Match the surrounding code style exactly when modifying existing files

## Structure & Organization
- Keep functions small and focused (single responsibility)
- Avoid deeply nested logic (max ~2–3 levels)
- Extract complex logic into well-named helper functions
- Group related logic together (cohesion > separation for its own sake)
- Avoid unnecessary layers (no “just in case” abstractions)

## Naming
- Use clear, descriptive, and intention-revealing names
- Avoid abbreviations unless widely known (e.g., `id`, `url`)
- Functions → verbs (`getUser`, `createOrder`)
- Variables → nouns (`user`, `orderList`)
- Booleans → prefix with `is`, `has`, `should`, `can`
- Avoid generic names like `data`, `temp`, `value`

## Functions
- One responsibility per function
- Prefer early returns over nested conditionals
- Limit number of parameters (prefer ≤ 3)
- Avoid side effects when possible
- Keep pure functions when it makes sense

## Readability
- Code should be understandable without comments
- Use comments only for **why**, not **what**
- Keep consistent formatting (follow project lint rules)
- Avoid clever or “magic” code

## Error Handling
- Fail fast and explicitly
- Do not silently ignore errors
- Use meaningful error messages
- Handle expected errors close to their source

## Types & Validation
- Prefer strict typing (when applicable)
- Validate inputs at boundaries (API, external data)
- Avoid trusting external input
- Keep schemas close to usage

## Reusability
- Reuse only when there is a clear repeated pattern
- Avoid premature generalization
- Prefer duplication over wrong abstraction

## Dependencies
- Avoid adding new dependencies unless necessary
- Prefer built-in or existing project solutions
- Keep dependency usage minimal and intentional

## Performance
- Don’t optimize prematurely
- Measure before optimizing
- Prefer readability over micro-optimizations

## Testing (if applicable)
- Test behavior, not implementation
- Keep tests simple and focused
- Cover critical paths and edge cases

## Anti-Patterns to Avoid
- God functions/classes
- Deep nesting
- Overuse of abstractions/interfaces
- Hidden side effects
- Inconsistent naming
- Large, hard-to-read files

## Output Expectations (for AI usage)
When generating code:
- Follow all rules above strictly
- Match existing project patterns
- Do not introduce new architecture without need
- Keep changes minimal and scoped
- Prefer editing existing code over rewriting everything
