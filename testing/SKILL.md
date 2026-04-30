---
name: testing
description: Define consistent, reliable, and maintainable testing practices across the project
---

# Testing Guidelines

## Core Principles
- Test behavior, not implementation details
- Focus on real use cases and outcomes
- Prefer simplicity and readability over completeness
- Tests should give confidence, not just coverage
- Consistency > perfection

## Scope & Strategy
- Prefer integration tests over excessive unit isolation
- Test at the boundaries (API, services, DB interactions)
- Only unit test complex or critical logic in isolation
- Avoid testing trivial code (getters, simple mappings)

## What to Test
- Main flows (happy paths)
- Important edge cases (invalid input, empty states, failures)
- Error handling and fallback behavior
- Data validation and contract boundaries
- Critical business rules

## Test Structure
- Follow AAA pattern (Arrange, Act, Assert)
- Keep each test focused on a single behavior
- Avoid large or multi-purpose tests
- Use helper functions for repetitive setup

## Naming
- Use clear, descriptive test names
- Prefer behavior-driven naming:
  - `should create user with valid data`
  - `should return 400 when input is invalid`
- Avoid vague names like `test1`, `works`, `should work`

## Readability
- Tests should be easy to understand at a glance
- Avoid complex logic inside tests
- Prefer explicit setup over “magic” abstractions
- Keep test files organized and not overly large

## Determinism
- Tests must be deterministic and repeatable
- Do not depend on execution order
- Avoid real time, randomness, or external state
- Mock only what is necessary to ensure stability

## Mocks & Dependencies
- Avoid over-mocking
- Prefer real integrations when feasible
- Mock only:
  - External services (APIs, queues, etc)
  - Unstable or slow dependencies
- Do not mock internal logic unnecessarily

## Data Handling
- Use realistic test data
- Keep data minimal but meaningful
- Avoid large fixtures unless necessary
- Reset state between tests (DB, cache, etc)

## Error Testing
- Always test failure cases where relevant
- Assert error messages/status when applicable
- Ensure invalid inputs are properly handled

## Performance
- Keep tests fast
- Avoid unnecessary heavy setup
- Prefer isolated DB/schema per test when possible

## Anti-Patterns
- Testing implementation details or private methods
- Overusing mocks for everything
- Flaky tests (timeouts, randomness, shared state)
- Large, hard-to-read test files
- Tests that depend on execution order
- Asserting too many things in a single test

## Consistency with Existing Code
- Follow the project's testing framework and patterns
- Match naming, structure, and style of existing tests
- Do not refactor unrelated tests unless explicitly asked
- Adapt to existing conventions (even if not ideal)

## When Input Is Provided (IMPORTANT)
When the user provides:
- a file
- a function
- an endpoint
- a service/module

You MUST:
- Infer what needs to be tested from that context
- Focus only on relevant behaviors
- Do not invent unnecessary scenarios
- Do not modify the original code unless explicitly asked

## Output Rules (STRICT)
- Return ONLY the test code
- No explanations, no comments outside code
- Use the project's test framework (e.g., Vitest, Jest, etc)
- Keep the output minimal and ready to paste
