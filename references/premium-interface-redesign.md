---
name: premium-interface-redesign
description: >-
  Use to audit and redesign an existing website or application interface for
  stronger visual identity, hierarchy, usability, responsiveness, accessibility,
  interaction quality, and product-specific polish. Works with the existing stack,
  preserves required product behavior, and may intentionally replace outdated
  visual or interaction patterns. Applies design judgment rather than universal
  bans on particular fonts, layouts, icon sets, or component patterns.
---

# Premium Interface Redesign

Upgrade an existing interface without turning it into a generic template.

Apply `senior-software-developer` and, for React projects, `senior-react-developer`.

This skill owns visual and interaction design. It does not replace engineering, accessibility,
performance, or product-design judgment.

## 1. Understand the Product

Before proposing visual changes:

1. Identify the product, audience, and primary tasks.
2. Inspect existing screens, routes, components, design tokens, assets, and content.
3. Determine the framework and styling system.
4. Identify what is already distinctive or effective.
5. Identify required behavior and behavior intentionally open to redesign.
6. Inspect responsive behavior.
7. Inspect loading, empty, error, permission, and destructive states.
8. Identify accessibility and performance constraints.

Do not redesign from screenshots alone when the code or interaction flow is available.

## 2. Define the Design Direction

When no clear visual direction exists, propose two or three credible directions.

Each direction should specify:

- Personality
- Typography approach
- Color behavior
- Density
- Layout character
- Surface treatment
- Motion character
- Image or illustration approach
- Suitability for the product

Recommend one direction and explain why.

Do not force alternatives when the brand system already determines the answer.

## 3. Audit Dimensions

### Visual hierarchy

Check:

- Primary action is obvious
- Page title and section hierarchy are clear
- Supporting information is visually secondary
- Dense screens distinguish navigation, controls, data, and status
- Repetition does not flatten importance
- Emphasis reflects user priorities

### Typography

Check:

- Typefaces fit the product
- Display and body roles are distinct where useful
- Sizes, weights, line heights, and spacing form a coherent scale
- Body measure supports reading
- Numeric data uses appropriate alignment or tabular figures
- Headings wrap intentionally
- Sentence case and capitalization are consistent
- Font loading cost is justified

Do not ban or require a font merely because it is common.

### Color

Check:

- Palette reflects the brand and task
- Contrast meets accessibility requirements
- Semantic colors are consistent
- Accent use is deliberate
- Grays and surfaces feel coherent
- Dark and light sections have a design reason
- Charts and status colors remain distinguishable
- Color is not the only signal

Multiple accent colors are acceptable when the system gives each one a clear role.

### Layout and rhythm

Check:

- Content width matches the task
- Alignment is intentional
- Spacing has a consistent rhythm
- Related elements stay together
- Dense interfaces use space efficiently
- Marketing interfaces have enough breathing room
- Responsive layout changes rather than merely shrinking
- Shared baselines align where alignment helps comprehension
- Asymmetry or overlap serves hierarchy rather than decoration

Do not reject sidebars, cards, centered layouts, or equal columns simply because they are common.

### Components

Check:

- Components represent real product concepts
- Cards are used only where grouping or elevation helps
- Buttons have clear hierarchy
- Forms expose labels, help, validation, and submission state
- Tables support actual data tasks
- Modals are used when interruption is justified
- Navigation communicates location
- Empty states help users proceed
- Errors explain recovery
- Skeletons or progress states match real latency

### Content

Check:

- Copy is specific and direct
- Labels use domain language
- Placeholder content is replaced with realistic draft content
- Empty and error messages explain next action
- Success messages are calm and informative
- Dates, numbers, currencies, and names are formatted consistently
- Sample data is believable without impersonating real people
- Legal or consent content appears only when actually required

### Iconography and imagery

Check:

- Icon style is consistent
- Stroke, fill, and optical size align
- Icons clarify rather than decorate
- Imagery supports the product story
- Avatars and illustrations are not needlessly repetitive
- Assets are optimized and have appropriate alternative text
- A favicon and social image exist when the product needs them

Do not reject a library solely because it is popular.

### Motion

Check:

- Motion explains state or hierarchy
- Hover and pressed states are perceptible
- Transitions are fast enough for task completion
- Layout animation avoids jank
- Reduced-motion preferences are respected
- Scroll effects do not impair control
- Animation libraries and assets have justified bundle cost

Avoid cinematic motion in task-heavy workflows unless it improves comprehension.

## 4. Interaction States

Every interactive component should define relevant states:

- Default
- Hover
- Focus
- Active or pressed
- Disabled
- Loading
- Success
- Error
- Empty
- Permission denied
- Destructive confirmation

Review keyboard and touch behavior, not only pointer hover.

Do not use `window.alert()` for normal product flows.

## 5. Responsive Design

Design intentionally for:

- Small phones
- Large phones
- Tablets
- Laptops
- Wide desktop screens

Check:

- Navigation transformation
- Table and data behavior
- Form layout
- Dialog and sheet sizing
- Touch target size
- Horizontal overflow
- Viewport units
- Sticky elements
- Safe areas
- Image cropping
- Typography scaling

Use `dvh`, `svh`, or framework guidance where mobile browser viewport behavior matters.

## 6. Accessibility

Visual polish must not reduce accessibility.

Verify:

- Semantic structure
- Logical heading order
- Visible focus
- Keyboard operation
- Sufficient contrast
- Correct labels and instructions
- Error association
- Accessible dialog and menu behavior
- Reduced motion
- Text resizing
- Screen-reader names
- Skip navigation where useful
- Meaningful alternative text

Do not use low contrast, hidden focus, or hover-only information for aesthetic reasons.

## 7. Performance

Audit design cost:

- Font files and weights
- Image formats and dimensions
- Video
- Animation libraries
- Client-side effects
- Large SVGs
- Blur and backdrop filters
- Scroll listeners
- Layout shifts
- Above-the-fold loading

Prefer the smallest asset and runtime cost that preserves the design.

Do not add texture, video, parallax, glass effects, or custom fonts without considering cost.

## 8. Redesign Strategy

Prioritize changes by value and risk.

Typical order:

1. Clarify hierarchy and information architecture
2. Establish typography and spacing system
3. Establish color and semantic tokens
4. Fix responsive structure
5. Improve core components
6. Add complete interaction states
7. Improve content
8. Add purposeful motion and surface detail
9. Optimize assets and performance
10. Remove obsolete styles and components

Do not begin with decorative effects while core hierarchy or usability is broken.

## 9. Audit Report

Before implementation, produce:

```markdown
# Interface Redesign Audit

## Product and audience

## Current strengths

## Primary problems

## Design direction

## High-priority changes

### 1. [Change]
- Evidence:
- User impact:
- Proposed treatment:
- Accessibility:
- Performance:
- Files or components:
- Risk:

## State coverage

## Responsive issues

## Content issues

## Asset and performance issues

## Elements to preserve

## Elements to remove

## Recommended implementation order
```

For substantial redesigns, obtain approval for the direction before implementation planning.

## 10. Implementation Rules

- Work with the existing stack unless migration is part of the approved redesign.
- Inspect dependency versions before importing libraries.
- Reuse good existing design primitives.
- Update design tokens before scattering one-off values.
- Preserve required product behavior.
- Intentional interaction changes may be breaking when approved.
- Delete obsolete styles, components, tokens, and assets.
- Avoid parallel old and new design systems.
- Keep changes reviewable by screen, flow, or component family.
- Verify responsive and accessibility behavior after each coherent change.

## 11. Quality Bar

A premium interface is not defined by maximal decoration.

It should feel:

- Specific to the product
- Consistent
- Readable
- Intentional
- Responsive
- Accessible
- Complete in all states
- Fast enough for its purpose
- Free of obvious template residue

Do not add noise, gradients, animation, or asymmetry merely to appear distinctive.

## 12. Self-Review

- [ ] Design direction fits the audience and product
- [ ] Existing strengths are preserved
- [ ] Hierarchy is improved before decoration
- [ ] Typography and spacing form a coherent system
- [ ] Color roles are explicit and accessible
- [ ] Loading, empty, error, and permission states are designed
- [ ] Mobile behavior is intentional
- [ ] Keyboard and screen-reader behavior remain correct
- [ ] Motion respects reduced-motion preferences
- [ ] Asset and runtime costs are justified
- [ ] Obsolete design code is removed
- [ ] One design system remains after completion
