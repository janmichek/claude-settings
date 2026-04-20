# Rules

## TypeScript

- **Strict typing**: Mandatory. Avoid `any`. Define interfaces for all API responses and component props
- **Unused variables**: Errors unless prefixed with `_` (e.g., `_unusedVar`)

## Vue Components

- Use `<script setup lang="ts">` syntax
- Component names: PascalCase (e.g., `DeviceDetailView.vue`)
- Prefer reusing components from `apps/web/src/shared/components`, secondarily use UI framework components
- Order of blocks is script -> template -> style
- Don't add comments to note different template sections

## Composables

- Named `use{Feature}.ts` (e.g., `useDeviceActions.ts`)
- Return reactive refs and functions
- Use `readonly()` for exposed state that shouldn't be mutated externally

## Routing

## API & Data Fetching

## Styling
- Implement custom styles using BEM methodology. Use component name as block name. Use lexical nesting of selectors

# AI Agent Guidelines

## Mission

- **Deliver correct, minimal, reviewable changes** that follow existing patterns, keep things simple
- **Prefer small diffs** and incremental refactors over broad rewrites
- **Keep the app working**: do not break builds, routing, auth, or runtime behavior

## Golden Rules

**DO:**
- Search for existing patterns (composables) before creating new ones
- Reuse existing utilities
- Show user-friendly errors, suggest user action
- Add explainable comment to watchers and exotic code caveats, and workarounds
- No unrelated formatting changes
- Clear naming matching domain conventions
- Appropriate error handling

**DON'T:**
- Add new libraries unless necessary and justified
- Mock around auth in production paths
- Commit credentials, tokens, or environment secrets
- Reformat unrelated code
- Leave dead code, temporary debug logs, or unused helpers
- Add comments to obvious points using similar words in variable/function name and comment
- Add comments to vue files annotating different sections
- Use `handle` prefix for vue functions. e.g. `handleSave()` → `save()`
- Use abbreviations for variable names
- No dead code or debug artifacts

## Safe Workflow

1. **Understand first**: Use repo search to find canonical patterns before inventing new ones
2. **Change second**: Touch the fewest files possible; keep changes scoped to the requested feature/bugfix
3. **Verify third**: Run eslint and tsc on affected files
