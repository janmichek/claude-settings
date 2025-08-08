# Development Rules & Best Practices

## Core Development Principles

- Write clean, readable, and maintainable code over comprehensive documentation
- Avoid Hasty Abstractions (AHA Principle): Prefer duplication over wrong abstraction
- make sure the code is written according to official Vue.js Style Guide
- Prioritize security and performance in all implementations
- Include comprehensive error handling
- Create reusable, isolated UI components

## Code Quality & Standards
- Use descriptive variable and function names
- Keep functions small and focused (single responsibility principle)
- Avoid deep nesting, keep things flat and explainable (maximum 3-4 levels)
- Use consistent formatting and indentation
- Remove dead code and unused imports
- Add comments for complex business logic only
- Apply consistent naming conventions (prefer BEM for CSS classnames)
- Add inline comments for complex algorithms only

### Examples: Good vs Bad Naming

```javascript
// ❌ Bad: Single word, unclear purpose
ComingSoon.vue

// ✔️ Good: Domain + Element Type
LoginLayout.vue
ChatForm.vue
DialogueActionMenu.vue
BotCard.vue
TrainingButton.vue
```

### Naming Recommendations

Avoid generic terms, use specific descriptors:

```javascript
// ❌ Bad: Generic names
❌ data → ✔️ details
❌ info → ✔️ description
❌ text → ✔️ specific context (title, description, label)
❌ value → ✔️ formattedValue
❌ item → ✔️ specific descriptor (user, product, option etc.)
❌ type → ✔️ variant, specificType
❌ onSubmit() -> ✔️ submit()


// ✔️ Good: Specific, semantic names
userDetails
productDescription
buttonVariant
selectedUser
formattedPrice
headingTitle
```

### Component Length Guidelines

- Keep Vue components under 150 lines
- Break large components into smaller, focused ones

## Error Handling

- Always handle errors gracefully
- Use try-catch blocks appropriately
- Provide meaningful error messages
- Log errors with sufficient context
- Fail fast when appropriate

## Performance & Optimization

- Apply appropriate font loading strategies
- Optimize images and assets for web delivery

## HTML & Semantic Structure

- Write valid, semantic HTML5
- Use structured data markup when appropriate (Schema.org)
- Validate markup using W3C standards
- Ensure proper document structure and headings hierarchy
- keep HTML flat and prepared for BEM naming

## CSS & Styling

- Use CSS modules or styled-components for scoping
- Follow BEM naming convention for CSS classes
- Write maintainable postcSS that passes Stylelint rules
- Use CSS variables
- Ensure sufficient color contrast for accessibility

### Examples: CSS Naming Best Practices

```css
/* ❌ Bad: Generic selector */
video {
  width: 100%
}

/* ✔️ Good: BEM-style naming */
.preview-file__video {
  width: 100%
}

/* ❌ Bad: Color-based naming */
.element--yellow {
  color: yellow;
}

/* ✔️ Good: Semantic state naming */
.element--warning {
  color: yellow;
}

/* ❌ Bad: Dependent selectors */
.button .icon {
  color: red;
}

/* ✔️ Good: BEM structure */
.button__icon {
  color: red;
}
```

### CSS Property Order

Prioritize properties in this order:

```css
.component {
  /* 1. Positioning properties */
  display: flex;
  position: relative;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  
  /* 2. Dimensional properties */
  width: 100%;
  height: auto;
  min-height: 200px;
  
  /* 3. Typography */
  font-family: 'Inter', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 1.5;
  
  /* 4. Spacing */
  margin: 0;
  padding: 16px;
  
  /* 5. Visual properties */
  background-color: white;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}
```

### Real-world CSS Example

```css
.loading {
    /* 1. Positioning properties */
    display: flex;
    flex-direction: column;
    align-items: center;

    /* 2. Dimensional properties */
    height: 240px;
    border-radius: 100%;

    /* 3. Typography */
    font-size: 14px;
    line-height: 19px;

    /* 4. Spacing */
    margin-top: var(--space-4);

    /* 5. Visual properties */
    background: var(--gray-300);
    animation: scale 4.5s ease-in-out infinite;
}
```

### CSS Sizing Convention

Use consistent sizing scale:

```css
/* Spacing scale */
.spacing-xs { padding: 4px; }
.spacing-sm { padding: 8px; }
.spacing-md { padding: 16px; }
.spacing-lg { padding: 24px; }
.spacing-xl { padding: 32px; }

/* Font sizes */
.text-xs { font-size: 12px; }
.text-sm { font-size: 14px; }
.text-md { font-size: 16px; }
.text-lg { font-size: 18px; }
.text-xl { font-size: 20px; }
```

### CSS Best Practices

- Every styled element needs a class name (avoid tag selectors)
- Use full names, no abbreviations
- Flat naming structure (avoid deep nesting)
- Always use semantic class names
- Avoid dependent selectors
- simple CSS, no utility classes
- minimalist class naming, by its parent

```css
/* ✔️ Good: taken from html li */
.user-menu__list {
  width: 100%
}

/* ✔️ Good: taken from parent component */
.user-menu__user-link {
  width: 100%
}

/* ✔️ Secondary: taken from feature, when already taken from html*/
.user-menu__avatar {
  width: 100%
}

``` 

## JavaScript & TypeScript Programming

- Prefer const/let over var
- Use async/await over Promises.then()
- Implement proper null/undefined checks
- Use optional chaining (?.) and nullish coalescing (??)
- Use full names, no abbreviations
- Document code with JSDoc

### Function vs Const Declaration Convention
- Use `function` declarations for actions/behaviors (verbs): handle*, submit*, update*, format*, navigate*
- Use `const` for computed values, reactive data, and configuration objects
- Benefits: Better semantic clarity, improved debugging, proper hoisting

## Vue.js Specific Guidelines
- Use `<script setup>` with Composition API for new components
- Keep components focused and single-purpose
- Use PascalCase for component names, kebab-case for events
- Prefer local state over global state when possible
- Use descriptive composable names (useOrder, useFilters)
- Implement proper cleanup in onUnmounted hooks

### Examples: Template Logic Extraction

```vue
<!-- ❌ Bad: Complex logic in template -->
<template>
  <button v-if="!isLoading || userCount > 1 && isTraining"/>
</template>

<!-- ✔️ Good: Logic moved to computed property -->
<template>
  <button v-if="isButtonHidden"/>
</template>

<script setup>
const isButtonHidden = computed(() => {
  return isLoading.value || 
         userCount.value > 1 && 
         isTraining.value
})
</script>
```

### BEM HTML Structure

```html
<!-- ✔️ Good: BEM naming in Vue templates -->
<ul :class="user__list">
    <li :class="user__item">
        <a class="user__link"/>
    </li>
</ul>

<!-- Button sizing with modifiers -->
<button class="button button--xl"/>
```

### Vue.js Event Naming

Write events in past tense:

```vue
<!-- ❌ Bad: Present tense -->
<UserForm @save="handleSave" @delete="handleDelete" />

<!-- ✔️ Good: Past tense -->
<UserForm @saved="handleSaved" @deleted="handleDeleted" />

<!-- Example: Button events -->
<button @send-button-pressed="uploadImage()"/>
```

### Component Design Principles

```vue
<!-- ❌ Bad: Internal spacing -->
<template>
  <div class="card">
    <div class="card__content">
      <h2 class="card__title">Title</h2>
      <p class="card__description">Description</p>
    </div>
  </div>
</template>

<style>
.card {
  margin: 16px; /* ❌ Don't add external spacing */
}
.card__content {
  padding: 24px; /* ✔️ Internal spacing is fine */
}
</style>

<!-- ✔️ Good: No internal whitespacing, parent manages spacing -->
<template>
  <div class="card">
    <div class="card__content">
      <h2 class="card__title">Title</h2>
      <p class="card__description">Description</p>
    </div>
  </div>
</template>

<style>
.card__content {
  padding: 24px;
}
</style>
```

## Accessibility & Inclusion

- Provide alternative text for images
- Maintain proper color contrast ratios

## Framework & Library Guidance

- Prefer vanilla solutions when frameworks add unnecessary complexity
- Evaluate bundle size impact of each dependency
- Keep dependencies updated and secure
- Remove unused dependencies regularly
- Start with the simplest solution first: Add complexity only when necessary
- Question utility libraries: Prefer native implementations when they're straightforward

## Testing & Quality Assurance

- Write unit tests for JavaScript functionality and core business logic
- Include Cypress tests for critical user paths and API endpoints
- Test error scenarios and edge cases
- Maintain high test coverage (aim for 80%+)
- Mock external dependencies properly
- place all mocks in a dedicated `__mocks__`
- Use static code analysis tools (SonarQube recommended)

## Security Best Practices

- Validate and sanitize all user inputs
- Use parameterized queries to prevent injection attacks
- Implement proper authentication and authorization
- Store sensitive data securely (environment variables)
- Use HTTPS for all communications
- Implement rate limiting for APIs
- Keep dependencies updated and audit for vulnerabilities
- Never commit secrets or API keys
- Implement proper CORS policies

## API Design & Integration

- Follow RESTful conventions
- Use appropriate HTTP status codes
- Implement proper request/response validation
- Include API versioning strategy
- Provide comprehensive and very decorated error responses
- Use consistent response formats
- Follow React Query/SWR patterns for data fetching
- Optimize API calls and avoid N+1 problems

## Environment & Configuration

- Use environment variables for configuration
- Never commit secrets or API keys to version control
- Use configuration files for different environments

## Git and Version Control

- Write clear, descriptive commit messages
- Create feature branches for new development
- Review code before merging (all code should be reviewed)
- Use semantic versioning for releases
- Keep commits atomic and focused
- Store all code in version control systems
- Document architectural decisions and trade-offs

## Documentation Requirements

- Include README with setup instructions
- Document API endpoints with examples and live preview link
- Add inline comments for complex algorithms only
- Maintain changelog for releases
- Regularly maintain readme.md
- Document environment variables and configuration

## CRUD UI Action Naming

Use clear, action-oriented naming for CRUD operations:

```javascript
// ❌ Bad: Ambiguous naming
"New Entity" → "Create Entity" -> "/create"
"Edit Entity" → "Save Entity" -> "/edit"
"Delete Entity" → "Delete Entity Forever" -> "/delete"

// ✔️ Good: Clear action naming
"Create User"
"Save Changes"
"Delete User Forever"
"Update Profile"
"Add Product"
```

## Architecture Guidelines

### ITCSS Structure
- Follow Inverted Triangle CSS architecture
- Organize styles from generic to specific
- Use BEM methodology consistently
- Implement with PostCSS

### Component Isolation
- Components should be completely isolated
- No external margins or positioning
- Parent components manage spacing and layout
- Use CSS custom properties for theming

### Flat Naming Structure
- Avoid deep CSS nesting
- keep js, css, and html flat rather than deeply nested
- Keep selectors flat and semantic
- Use BEM for clear component structure
