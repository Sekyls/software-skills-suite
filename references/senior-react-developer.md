---
name: senior-react-developer
description: >-
  Use for React and Next.js implementation, refactoring, debugging, and review.
  Adds React-specific architecture, rendering, state, effects, hooks, server/client
  boundaries, data fetching, forms, accessibility, and performance guidance on top
  of the senior-software-developer skill. Do not use this skill as a substitute for
  general engineering, security, database, Git, testing, or operational judgment.
---

# Senior React Developer

Apply `senior-software-developer` first. This skill contains only React-specific guidance.

Build React code whose data flow is obvious, rendering is predictable, state is minimal, effects
are rare, accessibility is native, and abstractions correspond to real UI concepts.

## 1. Read the React Architecture

Before editing:

- Identify the framework and router: Next.js App Router, Pages Router, Vite, Remix, or other.
- Determine React and framework versions from manifests.
- Inspect neighboring components, hooks, route files, providers, and tests.
- Determine the existing data-fetching model.
- Determine the design-system and form libraries already in use.
- Identify server and client boundaries.
- Trace the user interaction from route to rendered component to mutation and refresh.
- Search for an existing component, hook, schema, service, query key, or pattern before creating one.

Do not impose a folder layout from another repository.

## 2. Component Responsibilities

A component should primarily:

- Render UI
- Compose components
- Handle direct user interaction
- Read state through the project's established boundary
- Express loading, empty, error, and success states
- Preserve semantic structure and accessibility

Move non-visual domain behavior out of JSX-heavy components.

A component may contain small local helpers, constants, and prop types when they are truly local.
Extract them only when reuse, complexity, or repository convention justifies it.

Avoid:

- Components that perform unrelated orchestration
- Components that mix remote data access, complex transformation, and presentation
- Wrapper components that only spread props
- Generic renderers created for one screen
- Boolean-prop explosions
- Giant components with several independent regions and dialogs
- Fragmentation into tiny files that obscure one interaction

Prefer composition over configuration-driven component frameworks.

## 3. Server and Client Boundaries

In frameworks with server components:

- Default to server rendering when the component does not need browser-only behavior.
- Add `"use client"` only at the narrowest interactive boundary.
- Do not mark an entire route client-side because one child uses state.
- Keep secrets, privileged data access, and server-only dependencies outside client bundles.
- Pass serializable values across server/client boundaries.
- Avoid duplicating the same fetch on server and client without a deliberate reason.
- Use server actions, route handlers, or client mutations according to the project's established model.
- Revalidate or update caches intentionally after writes.

Review bundle impact when moving code into a client component.

## 4. State Ownership

Use the least powerful state mechanism that fits.

### Derived values

Compute during render. Do not store values that can be derived from props or existing state.

```tsx
const fullName = `${firstName} ${lastName}`;
```

Do not synchronize derived state with an effect.

### Local UI state

Use `useState` for state owned by one interaction:

- Open or closed
- Selected tab
- Draft input
- Temporary disclosure
- Local optimistic state

### Reducers

Use `useReducer` when transitions are related, state has multiple fields, or invalid transitions
must be prevented.

### URL state

Use the URL for shareable or navigable state:

- Search
- Filters
- Sorting
- Pagination
- Selected entity
- Active view when deep-linking matters

### Remote state

Use the project's data-fetching library or framework mechanism. Do not copy remote data into local
state merely to mirror it.

### Context

Use context for stable cross-tree concerns such as theme, session, localization, or a focused
compound component. Do not use one global context as an application database.

Split contexts when frequently changing values cause unrelated rerenders.

## 5. Effects

Effects synchronize React with an external system.

Valid examples:

- Browser APIs
- Subscriptions
- Timers
- Imperative third-party widgets
- Non-React event sources

Effects are usually wrong for:

- Deriving state
- Responding to a button click
- Transforming fetched data
- Resetting state that can be reset by key or event
- Chaining application logic that belongs in one handler
- Mirroring props into state

Every effect must be reviewed for:

- Correct dependencies
- Cleanup
- Race conditions
- Stale closures
- Duplicate work in development Strict Mode
- Cancellation of obsolete async work
- Whether the effect can be removed

Do not suppress dependency lint rules without a specific, documented reason.

## 6. Hooks

A custom hook should represent reusable stateful behavior or a coherent feature concern.

Good hooks:

- Have one clear responsibility
- Expose a narrow API
- Hide state-machine or data-fetching mechanics
- Return grouped, named concepts
- Preserve stable semantics
- Are testable through behavior

Avoid:

- Hooks that return a flat bag of many unrelated values
- Hooks that merely rename one library hook
- Hooks created only to move lines out of a component
- Generic hooks whose type parameters hide the domain
- Hooks that render JSX
- Hooks that depend on conditional call order

Name hooks for behavior: `useUserSearch`, `useCheckout`, `useInvoiceFilters`.

Query keys should be stable, hierarchical, and based on all inputs that affect the result.

## 7. Data Fetching and Mutations

Follow the repository's chosen model. In client-query architectures:

- Reads use query primitives.
- Writes use mutation primitives.
- Query functions remain free of rendering concerns.
- All query inputs appear in the query key.
- Cancellation signals are forwarded when supported.
- Errors remain distinguishable from empty results.
- Cache invalidation is precise.
- Optimistic updates include rollback and reconciliation.
- Pagination preserves previous data only when that is the intended experience.
- Dependent queries use explicit enablement rather than effect chains.

Do not add a hook or service layer merely because a diagram says one must exist. Add boundaries
that improve ownership, reuse, testing, or substitution.

Components may call framework-approved server actions, loaders, or generated clients directly when
that is the repository's chosen architecture. Consistency and clarity matter more than ritual
layering.

## 8. Rendering and Control Flow

Render all meaningful states deliberately:

- Initial loading
- Background refresh
- Empty
- Error
- Partial data
- Success
- Mutation pending
- Mutation failure
- Permission denied

Do not convert an error into an empty array unless the product explicitly defines those states as
equivalent.

Prefer early returns or extracted meaningful sections over deeply nested ternaries.

Use stable keys representing item identity. Never use an array index when items can be inserted,
removed, reordered, or filtered.

Keep render functions pure. Do not mutate props, global data, caches, or collections during render.

## 9. Forms

Choose the smallest form approach that fits the repository and complexity.

### Simple forms

For a few independent fields:

- Semantic `<form>`
- Visible labels
- Controlled or uncontrolled native inputs
- Native validation where sufficient
- Explicit submission state
- Clear field and form errors

### Complex or form-heavy applications

Use the established form and schema stack. A typical choice is:

- Schema validation
- Typed form values
- React Hook Form
- Resolver integration
- Accessible field components
- Controlled adapters for custom selectors

Rules:

- Keep one source of truth for validation.
- Do not duplicate schema validation in submit handlers.
- Map form shape to API shape at an explicit boundary.
- Associate every error with its field.
- Use `aria-invalid` and `aria-describedby`.
- Focus the first invalid field after failed submission when practical.
- Preserve submitted values after server rejection.
- Disable or guard duplicate submission.
- Distinguish pending from success.
- Reset intentionally when a create/edit dialog changes entity.

Do not centralize a schema, type, or default object solely because it exists. Colocate local form
definitions when the project allows it and extraction adds no value.

## 10. Semantic HTML and Accessibility

Use native HTML before ARIA.

- One logical `<main>` per page layout.
- Headings follow a meaningful hierarchy.
- Actions use `<button>`.
- Navigation uses links.
- Data tables use table semantics.
- Form fields have labels.
- Lists use list elements.
- Dialogs use accessible primitives.
- Icon-only controls have accessible names.
- Images have correct alternative text.
- Loading and async status are announced where needed.
- Errors are not communicated by color alone.
- Focus is visible.
- Keyboard interaction matches the visual interaction.
- Motion respects reduced-motion preferences.

Do not add ARIA that conflicts with native semantics.

For custom composite widgets, follow the relevant WAI-ARIA interaction pattern completely rather
than adding isolated roles.

## 11. Dialogs, Menus, and Overlays

Prefer established accessible primitives.

Verify:

- Focus moves into the overlay
- Focus is trapped when appropriate
- Escape closes when appropriate
- Focus returns to the trigger
- The title and description are announced
- Background content is not interactable
- Nested overlays do not break focus order
- Destructive actions require deliberate confirmation
- Pending actions cannot be accidentally repeated

Do not build a modal from a positioned `<div>` unless implementing the full interaction model is
the actual task.

## 12. Lists, Tables, and Large Collections

For lists and tables:

- Keep identity stable.
- Separate filtering, sorting, pagination, and rendering concerns.
- Keep filter and pagination state in the URL when shareability matters.
- Use semantic tables for tabular relationships.
- Provide captions or accessible names.
- Mark sortable state with `aria-sort`.
- Make row actions keyboard accessible.
- Avoid making an entire row clickable when it contains other controls.
- Virtualize only when measurement shows a need.
- Preserve scroll and selection intentionally across refreshes.

Do not create a universal table abstraction before multiple real screens establish a stable
pattern.

## 13. Performance

Start with correctness and measurement.

Review:

- Unnecessary client boundaries
- Expensive work repeated during render
- Broad context rerenders
- Unstable object and callback props passed to memoized children
- Duplicate queries
- Waterfalls
- Oversized client bundles
- Large unvirtualized collections
- Images and fonts
- Hydration mismatches
- Layout shifts

Use `useMemo`, `useCallback`, and `memo` only when:

- A measured or strongly evidenced problem exists
- Referential stability is required by an API
- The computation is meaningfully expensive
- The memoization boundary is understandable

Do not memoize everything. Memoization adds dependencies, memory, and debugging cost.

Prefer framework-level data loading, code splitting, and server rendering before manual
micro-optimization.

## 14. Error Boundaries and Recovery

Use error boundaries for rendering failures at useful recovery boundaries.

- Provide a user action: retry, navigate, reload, or report.
- Log enough context to diagnose the failure.
- Do not expose sensitive internals.
- Keep expected validation and business errors out of error boundaries.
- Use route-level boundaries when the framework supports them.
- Ensure loading and error boundaries do not cause layout chaos.

## 15. React Review Checklist

### Architecture

- [ ] Server and client boundaries are intentional
- [ ] Components have coherent visual responsibility
- [ ] State lives at the lowest correct owner
- [ ] Remote state is not unnecessarily mirrored locally
- [ ] Hooks have narrow behavior-focused APIs
- [ ] No abstraction exists only to satisfy a pattern

### Effects

- [ ] Every effect synchronizes with an external system
- [ ] Dependencies and cleanup are correct
- [ ] Async work cannot overwrite newer state
- [ ] No derived-state or event-handling effect remains

### Rendering

- [ ] Loading, empty, error, and success are distinct
- [ ] Keys are stable
- [ ] Render is pure
- [ ] Control flow is readable
- [ ] Errors are not silently treated as empty data

### Forms

- [ ] Labels and errors are associated correctly
- [ ] Validation has one source of truth
- [ ] Duplicate submission is prevented
- [ ] Server rejection preserves useful input
- [ ] Custom controls integrate accessibly

### Accessibility

- [ ] Native semantic elements are used
- [ ] Keyboard operation works
- [ ] Focus is visible and restored
- [ ] Async status is perceivable
- [ ] Dialogs and menus follow complete interaction patterns

### Performance

- [ ] No unnecessary client boundary
- [ ] No broad context rerender problem
- [ ] No duplicate fetch or waterfall introduced
- [ ] Memoization is justified
- [ ] Bundle and collection size are considered where relevant

## 16. Review Feedback

Classify React-specific findings using the parent skill's severity levels.

A finding must describe:

- The exact component, hook, or route
- The user-visible or maintenance failure
- Why React behaves that way
- The smallest clear correction

Do not block on preferred folder names, arbitrary line counts, or personal component style.

## 17. Relationship to the General Skill

Do not duplicate general rules here.

The parent `senior-software-developer` skill governs:

- Root-cause debugging
- General design and abstraction
- Security and privacy
- Data and persistence
- APIs and distributed systems
- General testing strategy
- Verification before completion
- Observability
- Git and destructive operations
- Completion reporting

This skill governs only React-specific implementation and review.
