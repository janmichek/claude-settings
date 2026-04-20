# Code Review Command

Perform a comprehensive, detailed code review of changes in the current branch or specified files, following OpenAssets project standards and industry best practices.

## Command Purpose
Conduct a thorough code review that catches issues before they reach production, ensures consistency with project conventions, and provides actionable feedback for improvement.

## Review Scope

By default, review all changes in the current branch compared to the dev branch (dev). Can also review:
- Specific files or directories
- Uncommitted changes (git diff)
- Recent commits
- Pull request changes

## Actions to Perform

### 1. Identify Changes to Review

- **Run git status** to see current state
- **Run git diff dev...HEAD** to see all changes in the branch
- **List all modified/added files** for systematic review
- **Identify change scope**: Is this a feature, bugfix, refactor, or cleanup?

### 2. Architecture & Design Review

**Check for:**
- [ ] Changes follow existing architectural patterns
- [ ] New features belong in appropriate domain (`assets`, `hr`, `maintenance`, etc.)
- [ ] No duplication of existing functionality
- [ ] Proper separation of concerns (components, composables, views)
- [ ] Appropriate use of shared components vs. domain-specific components
- [ ] Routing follows conventions (lazy loading, proper meta tags)
- [ ] State management uses Vue Query patterns correctly

**Questions to answer:**
- Does this change fit the overall system design?
- Are there better patterns already in the codebase?
- Is the complexity justified?
- Will this scale appropriately?

### 3. TypeScript & Type Safety Review

**Check for:**
- [ ] **No `any` types** (except justified cases with comments)
- [ ] Proper interfaces for API responses and component props
- [ ] Type-only imports where appropriate
- [ ] Correct use of generic types
- [ ] No implicit `any` from missing types
- [ ] Proper typing of composables return values
- [ ] Unused variables prefixed with `_`
- [ ] No `@ts-ignore` or `@ts-expect-error` without justification

**Run:**
```bash
npm run lint
```

### 4. Vue Component Review

**Check for:**
- [ ] Uses `<script setup lang="ts">` syntax
- [ ] Proper component naming (PascalCase)
- [ ] Views end with `View.vue`, details end with `DetailView.vue`
- [ ] Correct block order: script → template → style
- [ ] Props properly typed with `defineProps<T>()`
- [ ] Emits properly typed with `defineEmits<T>()`
- [ ] Reactive state uses `ref()` or `reactive()` appropriately
- [ ] Computed properties for derived state
- [ ] No side effects in computed properties
- [ ] Proper lifecycle hook usage
- [ ] Template uses Quasar components consistently
- [ ] No v-if with v-for on same element
- [ ] Proper key attributes in v-for loops
- [ ] Event handlers follow naming convention (@click, not v-on:click)

### 5. Composable Review

**Check for:**
- [ ] Named with `use` prefix (e.g., `useDeviceActions.ts`)
- [ ] Returns reactive refs and functions
- [ ] Uses `readonly()` for state that shouldn't be mutated externally
- [ ] Proper cleanup in `onUnmounted` if needed
- [ ] Vue Query patterns follow conventions
- [ ] Query keys use centralized `queryKeys.ts`
- [ ] Mutation callbacks handle success/error appropriately
- [ ] Query invalidation after mutations

### 6. API & Data Fetching Review

**Check for:**
- [ ] Uses `@openassets/api-client` or `api-client-v3` repositories
- [ ] No raw fetch/axios calls (use established clients)
- [ ] Proper error handling with user feedback
- [ ] Loading states handled appropriately
- [ ] Query keys centralized and consistent
- [ ] Optimistic updates where appropriate
- [ ] Proper use of `useBusinessObjects()` for CRUD
- [ ] Entity models properly defined
- [ ] API response types defined

### 7. Styling & UI Review

**Check for:**
- [ ] Uses design tokens from `design-tokens.scss`
- [ ] CSS custom properties for theming
- [ ] Scoped styles in components
- [ ] No hardcoded colors (use tokens)
- [ ] Responsive design considerations
- [ ] Proper use of Quasar spacing utilities
- [ ] Consistent with existing UI patterns
- [ ] Accessible (proper labels, ARIA attributes)
- [ ] Dark mode support (if applicable)

### 8. Internationalization Review

**Check for:**
- [ ] **No hardcoded user-facing strings**
- [ ] All text uses `t('key')` or `$t('key')`
- [ ] Translation keys added to both CS and EN files
- [ ] Keys follow domain structure (e.g., `maintenance.plan.title`)
- [ ] Proper pluralization handling if needed
- [ ] No string concatenation for translations

**Verify translation files:**
- `apps/web/src/i18n/cs/*.ts`
- `apps/web/src/i18n/en/*.ts`

### 9. Security Review

**Check for:**
- [ ] No SQL injection vulnerabilities
- [ ] No XSS vulnerabilities (proper escaping)
- [ ] No credential/token leaks in code
- [ ] Proper input validation
- [ ] No eval() or unsafe dynamic code execution
- [ ] Proper authentication checks
- [ ] Authorization enforced server-side (not just UI)
- [ ] Sensitive data not logged
- [ ] No CORS issues
- [ ] Dependencies have no known vulnerabilities

### 10. Performance Review

**Check for:**
- [ ] No unnecessary re-renders
- [ ] Proper use of computed vs. watch
- [ ] Large lists use virtual scrolling
- [ ] Images optimized and lazy-loaded
- [ ] Route-based code splitting (lazy loading)
- [ ] No memory leaks (proper cleanup)
- [ ] Efficient queries (no N+1 problems)
- [ ] Debouncing for expensive operations
- [ ] Memoization where appropriate

### 11. Error Handling Review

**Check for:**
- [ ] User-friendly error messages (via Quasar Notify)
- [ ] Errors logged appropriately
- [ ] Network errors handled
- [ ] Validation errors displayed clearly
- [ ] Try-catch blocks where needed
- [ ] Promise rejections handled
- [ ] Graceful degradation
- [ ] No silent failures

### 12. Testing Review (if tests exist)

**Check for:**
- [ ] Tests exist for new functionality
- [ ] Tests are meaningful (not just coverage)
- [ ] Edge cases covered
- [ ] Error cases tested
- [ ] Mock data is realistic
- [ ] Tests are maintainable
- [ ] No flaky tests

**Run:**
```bash
npm test
```

### 13. Code Quality & Maintainability

**Check for:**
- [ ] Clear, descriptive naming
- [ ] Functions/methods have single responsibility
- [ ] No deeply nested code (max 3-4 levels)
- [ ] No magic numbers (use named constants)
- [ ] Comments explain "why" not "what"
- [ ] No commented-out code (use git history)
- [ ] No TODO comments without issues/tickets
- [ ] No console.log left in production code
- [ ] Consistent code style with project
- [ ] Files are appropriately sized (<500 lines)

### 14. Documentation Review

**Check for:**
- [ ] Complex logic has explanatory comments
- [ ] Public APIs documented
- [ ] README updated if needed
- [ ] CLAUDE.md updated with context
- [ ] Breaking changes noted
- [ ] Migration guide if needed

### 15. Git & Version Control

**Check for:**
- [ ] Commit messages are clear and descriptive
- [ ] Logical commit breakdown
- [ ] No large binary files
- [ ] No sensitive data in commits
- [ ] Branch name follows convention
- [ ] No merge conflicts
- [ ] Clean git history

## Review Output Format

Provide structured feedback in this format:

```markdown
# Code Review Report - [Branch Name]

## Summary
Brief overview of changes and overall assessment.

**Rating**: ✅ Approved | ⚠️ Approved with Comments | ❌ Needs Changes

## Files Reviewed
- `path/to/file1.vue` - [brief description]
- `path/to/file2.ts` - [brief description]
- ...

---

## Critical Issues 🚨
Issues that MUST be fixed before merge.

### 1. [Issue Title]
**File**: `path/to/file.ts:123`
**Severity**: Critical
**Category**: Security / Performance / Bug / TypeScript

**Problem**:
[Clear description of the issue]

**Impact**:
[Why this matters]

**Solution**:
```typescript
// Suggested fix
```

---

## Major Issues ⚠️
Important issues that should be addressed.

### 1. [Issue Title]
**File**: `path/to/file.ts:45`
**Severity**: Major
**Category**: Architecture / Best Practice / Maintainability

**Problem**:
[Clear description]

**Suggestion**:
[How to improve]

---

## Minor Issues ℹ️
Nice-to-have improvements and nitpicks.

### 1. [Issue Title]
**File**: `path/to/file.ts:67`
**Severity**: Minor
**Category**: Code Style / Naming / Documentation

**Suggestion**:
[Optional improvement]

---

## Positive Highlights ✨
Things done well worth mentioning.

- Good use of [pattern/approach] in [file]
- Well-structured [component/composable] that follows conventions
- Comprehensive error handling in [file]
- Clear, maintainable code in [file]

---

## Convention Compliance

| Category | Status | Notes |
|----------|--------|-------|
| TypeScript | ✅/⚠️/❌ | [comments] |
| Vue Components | ✅/⚠️/❌ | [comments] |
| Styling | ✅/⚠️/❌ | [comments] |
| i18n | ✅/⚠️/❌ | [comments] |
| API Usage | ✅/⚠️/❌ | [comments] |
| Error Handling | ✅/⚠️/❌ | [comments] |
| Testing | ✅/⚠️/❌ | [comments] |

---

## Performance Analysis

**Potential Issues**:
- [Issue and location]

**Optimization Opportunities**:
- [Opportunity and benefit]

---

## Security Analysis

**Vulnerabilities Found**: [count]
- [Description and location]

**Recommendations**:
- [Security improvements]

---

## Architectural Notes

**Patterns Used**:
- [Pattern and where]

**Consistency**:
- [How well it matches existing code]

**Suggestions**:
- [Architectural improvements]

---

## Action Items

### Must Do (Blocking)
1. [ ] Fix [critical issue] in [file]
2. [ ] Add [missing requirement] to [file]

### Should Do (Recommended)
1. [ ] Improve [issue] in [file]
2. [ ] Refactor [pattern] in [file]

### Could Do (Optional)
1. [ ] Consider [enhancement] for [feature]
2. [ ] Document [complex logic] in [file]

---

## Review Checklist

- [ ] Architecture follows project patterns
- [ ] TypeScript types are correct and complete
- [ ] Vue components follow conventions
- [ ] No hardcoded strings (i18n used)
- [ ] Styling uses design tokens
- [ ] Security vulnerabilities checked
- [ ] Performance considered
- [ ] Error handling is appropriate
- [ ] Code is maintainable
- [ ] Tests exist and pass
- [ ] Documentation updated
- [ ] Linting passes
- [ ] Build succeeds

---

## Final Recommendation

**Decision**: ✅ Merge / ⚠️ Merge with follow-up / ❌ Request changes

**Review UI Changes manually**: Provide direct links and instructions to localhost, where to manually  check the changes 
**Open links for app occurences**: open all those provide links in Firefox Nightly like `open -a "Firefox Nightly" http://localhost:9000/link`

**Reasoning**:
[Justification for decision]

**Next Steps**:
1. [Action]
2. [Action]

**Estimated Effort**: [time to address issues]
```

## Special Review Types

### Feature Review
Focus on:
- Requirements satisfaction
- User experience
- Integration points
- Future extensibility

### Bug Fix Review
Focus on:
- Root cause addressed
- No regression introduced
- Edge cases handled
- Tests added for bug

### Refactor Review
Focus on:
- Behavior unchanged
- Complexity reduced
- Maintainability improved
- No over-engineering

### Performance Optimization Review
Focus on:
- Measurable improvement
- No premature optimization
- Trade-offs justified
- Benchmarks included

## Critical Reminders

1. **Be thorough but constructive** - Find issues but suggest solutions
2. **Prioritize issues** - Not all feedback is equally important
3. **Verify with tooling** - Run lint, tests, build
4. **Check actual files** - Don't assume, read the code
5. **Consider context** - Some rules have valid exceptions
6. **Be specific** - Include file paths and line numbers
7. **Suggest alternatives** - Don't just criticize, help improve
8. **Acknowledge good work** - Note positive aspects

## Best Practices

- Review in small batches for better focus
- Check related files for consistency
- Test changes locally if possible
- Consider backwards compatibility
- Think about edge cases
- Question unnecessary complexity
- Verify translations exist
- Check for dead code
- Look for copy-paste errors
- Consider mobile/responsive behavior

## Review Workflow

1. **Quick scan**: Get overall sense of changes
2. **Deep dive**: Review each file systematically
3. **Run tools**: Lint, test, build
4. **Cross-reference**: Check for consistency
5. **Document**: Create detailed review report
6. **Prioritize**: Categorize issues by severity
7. **Provide**: Clear, actionable feedback
