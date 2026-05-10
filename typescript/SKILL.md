---
name: typescript
description: TypeScript code style and optimization guidelines. Use when writing TypeScript code (.ts, .tsx, .mts files), reviewing code quality, or implementing type-safe patterns. Triggers on TypeScript development, type safety questions, or code style discussions.
---

# TypeScript Code Style Guide

## Types and Type Safety

**Inference over explicit types**
- Let TypeScript infer types when possible; annotate only when inference fails or for clarity

**Avoid implicit `any`**
- Explicitly type when necessary instead of allowing implicit `any`

**Use accurate types**
- Prefer `Record<PropertyKey, unknown>` over `object` or `any` for flexible object types

**Interface vs Type**
- Use `interface` for object shapes (e.g., React props, data structures)
- Use `type` for unions, intersections, and mapped types

**Const assertions**
- Prefer `as const satisfies XyzInterface` over plain `as const` for type-checked constants

**Type suppression hierarchy**
- Prefer `@ts-expect-error` (fails if error is gone) over `@ts-ignore` (always suppresses) over `as any` (least safe)

**Function design**
- Avoid meaningless `null`/`undefined` parameters; design strict function contracts with required parameters or use overloads

## Async Patterns

**Modern promise syntax**
- Prefer `async`/`await` over callbacks or `.then()` chains
- Prefer async APIs over sync variants (avoid `*Sync` methods)
- Use promise-based imports: `import { readFile } from 'fs/promises'`

**Concurrent operations**
- Use `Promise.all()` for concurrent independent operations
- Use `Promise.race()` when you need the first resolved promise

## Code Structure

**Destructuring**
- Prefer object destructuring for cleaner code:
  ```typescript
  const { id, name } = user;  // ✅
  const id = user.id;         // ❌
  ```

**Naming**
- Use consistent, descriptive naming
- Avoid obscure abbreviations unless widely understood (e.g., `id`, `url`)

**Constants over magic values**
- Replace magic numbers/strings with well-named constants:
  ```typescript
  const MAX_RETRIES = 3;           // ✅
  if (attempts > 3) { ... }        // ❌
  ```

**Formatting**
- Defer formatting to tooling (Prettier, ESLint)
- Don't manually format code

## UI and Theming

**Component libraries**
- Use `@lobehub/ui` and Ant Design components instead of raw HTML tags
- Design for dark mode compatibility
- Ensure mobile responsiveness

**Styling**
- Use `antd-style` token system for colors and spacing
- Avoid hard-coded color values

## Performance

**Loop performance**
- Prefer `for...of` loops over index-based `for` loops for readability
- Use index loops only when you need the index

**Reuse existing code**
- Check `packages/utils` or installed npm packages before writing new utilities
- Don't reinvent common functionality

**Database queries**
- Query only required columns; avoid `SELECT *`
- Use projection to limit data transfer

## Time Consistency

**Single timestamp reference**
- Assign `Date.now()` to a constant once and reuse throughout the operation
- Prevents timing inconsistencies in the same logical operation

## Logging

**Never log sensitive data**
- No API keys, tokens, passwords, or PII in logs

**Proper logging practices**
- Don't use `import { log } from 'debug'` directly (logs to console)
- Use `console.error` in catch blocks instead of debug package
- Use structured logging for production systems
