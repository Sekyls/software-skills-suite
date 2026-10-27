---
name: designing-features
description: >-
  Use before planning or implementing a feature when product intent, behavior,
  user experience, scope, architecture, or success criteria are materially
  ambiguous. Turns an idea into an approved, implementation-ready design through
  focused investigation, concrete questions, alternative approaches, explicit
  decisions, and a written specification. Skip this skill for clear, local bug
  fixes or fully specified changes.
---

# Designing Features

Turn uncertain intent into a clear product and technical design.

This skill operates before `writing-implementation-plans`. It resolves what should be built and
why. The planning skill resolves how the approved design will be implemented.

Apply `senior-software-developer` and any relevant domain skill while designing.

## 1. When to Use

Use this skill when:

- The user describes an idea rather than defined behavior
- Important acceptance criteria are missing
- Multiple valid product or architectural approaches exist
- Several subsystems may be involved
- User experience or workflow requires decisions
- The request contains conflicting goals
- A redesign changes user behavior, not merely styling
- The user asks for a specification, architecture, or product design

Skip it when:

- The request is a clear, local bug fix
- Acceptance criteria are explicit
- The change is isolated and obvious
- A complete approved specification already exists
- The user explicitly requests direct implementation and no material ambiguity remains

Do not impose a design ceremony on trivial work.

## 2. Establish Context

Before asking detailed questions:

1. Inspect relevant repository files, documentation, interfaces, tests, and recent decisions.
2. Identify the current user flow and system behavior.
3. Determine whether the request is one coherent feature or several independent systems.
4. Identify constraints already established by the repository or specification.
5. Separate confirmed facts from assumptions.

Do not ask the user for information that the repository can answer.

## 3. Scope Check

If the request combines independent systems, decompose it before designing details.

Examples:

- Authentication
- Billing
- Messaging
- File storage
- Analytics
- Administration

A coherent feature should have one primary outcome and a testable boundary.

For a large request:

1. Name the independent subprojects.
2. Explain dependencies.
3. Recommend an implementation order.
4. Design the first subproject fully.
5. Leave later subprojects explicitly out of scope.

## 4. Clarification Strategy

Ask only questions that materially change the design.

Prioritize:

- Who uses the feature?
- What problem are they solving?
- What must happen?
- What must never happen?
- What data enters and leaves?
- What permissions apply?
- What constitutes success?
- What constraints are fixed?
- What behavior may be deleted or replaced?
- What failure experience is acceptable?

Ask one focused question at a time when interaction is useful. Prefer concrete options when the
decision space is known.

Do not ask abstract questions such as "What tone do you want?" when the real issue is a specific
interaction, audience, or outcome.

Do not continue questioning after the design is sufficiently constrained.

## 5. Explore Alternatives

For material decisions, present two or three credible approaches.

For each approach, explain:

- Core idea
- User experience
- Technical shape
- Advantages
- Costs
- Failure modes
- What it simplifies or deletes
- Why it fits or conflicts with the repository

Lead with the recommended approach.

Do not manufacture alternatives when one option is clearly correct.

## 6. Design Principles

A strong design:

- Has one primary user outcome
- Has explicit acceptance criteria
- Defines one canonical path
- Assigns clear ownership
- Uses repository evidence
- Removes unnecessary features and compatibility paths
- Defines failure behavior
- Protects security and data invariants
- Is small enough to implement and verify
- Avoids speculative extensibility

Prefer deep, cohesive modules over many shallow forwarding layers.

Do not preserve obsolete behavior without an explicit requirement.

## 7. Design Content

Cover only the sections relevant to the feature.

### Problem

- Current pain
- Affected users
- Why the existing behavior is insufficient

### Goals

- Observable outcomes
- Business or user value
- Quality expectations

### Non-goals

- Explicit exclusions
- Deferred capabilities
- Adjacent systems not being redesigned

### User experience

- Entry point
- Main flow
- Alternate paths
- Empty, loading, error, and permission states
- Recovery from failure
- Destructive confirmations
- Accessibility expectations

### Domain model

- Important concepts
- Ownership
- Invariants
- Relationships
- Terms that require precise definitions

### Architecture

- Canonical data and control flow
- Module responsibilities
- External integrations
- State ownership
- Server/client or service boundaries
- What is removed

### Data

- Inputs
- Outputs
- Persistence
- Validation
- Retention
- Migration or cleanup

### Security and privacy

- Authentication
- Authorization
- Sensitive data
- Abuse cases
- Audit or trace requirements

### Failure behavior

- Invalid input
- Partial failure
- Retry
- Timeout
- Duplicate actions
- Concurrency
- User-visible recovery

### Testing

- Critical behavior
- Contract boundaries
- Important failure cases
- End-to-end journey
- Performance or migration evidence if relevant

### Operations

- Logging
- Metrics
- Rollout
- Recovery
- Removal of temporary transition structures

## 8. Design Interrogation

Before approval, challenge the design.

Ask internally:

- What assumption is carrying the most risk?
- What would make this feature fail for users?
- Which responsibility has no clear owner?
- Where could two canonical paths emerge?
- What part is speculative?
- What can be removed?
- What happens when the external dependency is unavailable?
- What happens when the same action is submitted twice?
- What happens when permissions change during the flow?
- Could the feature be half the size?

When a user rejects an option for a durable architectural reason, suggest recording that decision
in an ADR if future engineers would otherwise repeat the debate.

Do not create an ADR for temporary scheduling or preference decisions.

## 9. Specification Format

Save the approved design using:

```markdown
# [Feature Name] Design

## Status
Draft | Approved

## Problem

## Users and use cases

## Goals

## Non-goals

## Acceptance criteria
- [Observable behavior]

## Current system
- [Relevant repository facts]

## Options considered

### Option A
### Option B

## Decision
- [Selected approach and reason]

## User experience

## Domain model

## Architecture and data flow

## Interfaces and contracts

## Data and migration

## Security and privacy

## Failure and recovery behavior

## Accessibility

## Testing strategy

## Operations and observability

## Deletion and cleanup

## Open decisions
- [Only unresolved decisions that genuinely block planning]
```

Omit irrelevant sections rather than filling them with generic text.

Default path:

```text
docs/specs/YYYY-MM-DD-<feature-name>.md
```

Respect user or repository conventions when different.

Do not commit the specification automatically. Commit only when requested or when the active
workflow explicitly requires it.

## 10. Approval Gate

For substantial or ambiguous designs, obtain user approval before planning.

Approval can be concise:

- Approve
- Approve with listed changes
- Reject and revise

For small designs, a short design summary and one approval gate are sufficient. Do not require
approval after every paragraph.

## 11. Self-Review

Before handoff:

### Completeness

- [ ] Problem and users are clear
- [ ] Acceptance criteria are observable
- [ ] Non-goals prevent scope expansion
- [ ] One canonical design is selected
- [ ] Important alternatives were considered

### Architecture

- [ ] Responsibilities have owners
- [ ] Interfaces are understandable
- [ ] Data flow is explicit
- [ ] Obsolete paths are identified for deletion
- [ ] No permanent compatibility layer was introduced without requirement

### Risk

- [ ] Security and authorization are addressed
- [ ] Failure and recovery are defined
- [ ] Data and migration risks are addressed
- [ ] Concurrency and duplicate actions are considered where relevant

### Buildability

- [ ] A planning agent can derive tasks without inventing missing behavior
- [ ] Open questions are genuinely blocking
- [ ] Repository facts and assumptions are distinguishable

## 12. Handoff

After approval:

1. Save the specification.
2. Report the path.
3. Summarize the selected design.
4. Name the principal deletion or simplification.
5. Identify the highest-risk area.
6. Invoke or recommend `writing-implementation-plans`.

Do not begin implementation from this skill.
