---
name: writing-implementation-plans
description: >-
  Use when a feature, refactor, migration, or bug fix is large enough to require
  a written implementation plan before coding. Produces an evidence-based,
  implementation-ready plan from the specification and repository, with exact
  ownership, task boundaries, interfaces, acceptance criteria, verification,
  risks, deletion work, and execution order. Plans describe enough detail to
  implement confidently without pre-writing the entire solution.
---

# Writing Implementation Plans

Create plans that reduce uncertainty and produce better code.

A plan is not ceremonial documentation and not a speculative rewrite of the repository. It is a
tested model of the intended change based on the specification and the actual codebase.

Apply `senior-software-developer` and any relevant framework skill while planning.

## 1. When to Plan

Write a plan when the work includes one or more of:

- Multiple coherent implementation tasks
- Cross-module or cross-service changes
- A new feature with unclear ownership
- Data or schema changes
- Security-sensitive behavior
- Significant refactoring
- Removal of an old architecture or API
- Multiple deployment or operational steps
- Work that will be delegated to another agent or engineer

Do not create a heavyweight plan for a trivial, local, obvious change.

## 2. Inputs

Use:

- The user's specification
- Approved design documents
- Repository structure
- Existing implementation
- Tests
- Schemas and contracts
- Configuration
- Package manifests and versions
- CI and build commands
- Relevant history when available

Do not invent paths, APIs, types, commands, or architectural conventions.

When a fact cannot be established, mark it as an explicit unresolved assumption or investigation
step. Do not disguise uncertainty as plan detail.

## 3. Planning Workflow

### Step 1: Restate the outcome

Define:

- What the user will be able to do
- What behavior changes
- What is intentionally removed
- Observable acceptance criteria
- Explicit non-goals

### Step 2: Map the current system

Trace the current flow:

- Entry point
- UI or caller
- Application/domain logic
- Data and external boundaries
- Existing tests
- All owned consumers of interfaces being changed
- Obsolete or competing paths

Record only facts relevant to implementation.

### Step 3: Choose the target design

State:

- The canonical path after the change
- Ownership of each responsibility
- Interfaces between tasks
- Data flow
- Error behavior
- Security and failure invariants
- What old code, API, schema, flag, or wrapper will be deleted

Do not retain backward-compatibility machinery unless the specification explicitly requires it or
the deployment environment makes a temporary migration stage necessary. Temporary migration
structures must include a deletion task.

### Step 4: Identify risk

Consider:

- Data loss
- Authorization
- Destructive behavior
- Concurrency
- Partial failure
- External dependencies
- Migration duration
- Performance
- Observability
- Recovery

The plan must be more detailed where risk is higher.

### Step 5: Decompose into tasks

A task is a coherent, independently reviewable change with:

- One primary outcome
- Clear file ownership
- Defined inputs and outputs
- Observable acceptance criteria
- A verification method
- No unresolved dependency on a later task

Tasks should be large enough to matter and small enough to review.

Do not split every edit into a separate task. Do not combine unrelated subsystems into one task.

### Step 6: Order by dependency

Prefer:

1. Characterization or baseline tests where needed
2. Foundational types, schemas, or contracts
3. Core behavior
4. Integration and UI
5. Data migration or backfill
6. Deletion of superseded paths
7. Broad verification and operational checks

Order may differ when deployment constraints require it. Explain the reason.

## 4. Plan Depth

Use the least detail that eliminates meaningful ambiguity.

### Always include

- Exact paths
- Responsibility of each file
- Interfaces or contract changes
- Acceptance criteria
- Verification commands
- Relevant failure cases
- Deletions
- Dependencies between tasks

### Include when useful

- Function signatures
- Data shapes
- Pseudocode for complex logic
- Representative test cases
- Query or migration strategy
- Rollout and recovery steps
- Accessibility behavior
- Logging or metrics

### Do not include by default

- Complete production implementation
- Large copy-paste code blocks
- Every trivial import
- Exact line numbers likely to drift
- Commit after every tiny action
- Generic advice such as "handle errors"
- Fake expected command output

A plan should guide implementation, not duplicate it.

## 5. Plan Header

Every plan begins with:

```markdown
# [Feature Name] Implementation Plan

**Goal:** [One observable outcome]

**Current problem:** [What is wrong, missing, duplicated, or obsolete]

**Target design:** [The canonical architecture after implementation]

**Deletion:** [Old paths, interfaces, flags, files, or shims to remove]

**Tech stack:** [Relevant verified technologies and versions]

**Acceptance criteria:**
- [Observable criterion]
- [Observable criterion]

**Non-goals:**
- [Explicit boundary]

**Global constraints:**
- [Security, platform, dependency, naming, or operational constraint]
```

Omit a section only when genuinely irrelevant.

## 6. Task Template

Use this structure:

```markdown
### Task N: [Outcome-oriented title]

**Purpose:** [Why this task exists]

**Depends on:** [Task numbers or "None"]

**Files:**
- Create: `exact/path`
- Modify: `exact/path`
- Delete: `exact/path`
- Test: `exact/path`

**Current evidence:**
- [Relevant fact observed in the repository]

**Design:**
- [Ownership and behavior]
- [Important control/data flow]
- [Failure behavior]
- [What not to preserve]

**Interfaces:**
- Consumes: `[exact interface, type, event, or file]`
- Produces: `[exact interface, type, event, or file]`
- Removes: `[obsolete interface or path]`

**Implementation steps:**
- [ ] [One concrete action]
- [ ] [One concrete action]
- [ ] [Delete superseded code]
- [ ] [Update all owned consumers]

**Tests and verification:**
- [ ] `[exact focused command]`
- [ ] [Specific behavior or failure case proved]
- [ ] `[broader command if justified]`

**Acceptance criteria:**
- [Observable result]

**Risks and recovery:**
- [Only when relevant]
```

Use exact signatures when downstream tasks depend on them.

## 7. Testing in Plans

Choose tests by risk.

For a bug:

- Describe the failing behavior.
- Add a regression test when practical.
- Verify the old failure no longer occurs.
- Check sibling paths that share the cause.

For new deterministic logic:

- Test-first is preferred when it clarifies the contract.

For UI:

- Define interaction, accessibility, loading, empty, error, and success behavior.
- Use component or end-to-end tests where they provide confidence.
- Do not force a meaningless unit test.

For migrations:

- Verify transformed data
- Verify restartability
- Verify failure handling
- Verify cleanup
- Define recovery when reversal is impossible

Never write "add tests" without stating what behavior must be proven.

## 8. Breaking Changes and Deletion

Plans should actively simplify.

For every replaced API, module, component, schema, or flow:

- Search all consumers
- Update owned consumers
- Delete the old implementation
- Delete compatibility wrappers
- Delete stale tests and documentation
- Remove unused dependencies and configuration
- Verify no references remain

When temporary coexistence is operationally necessary:

- Explain why
- Define the transition
- Define the removal condition
- Include the removal task in the same plan or a named immediate follow-up

No indefinite compatibility layer.

## 9. Verification Commands

Commands must come from repository evidence.

Include:

- Focused test command
- Relevant lint or static analysis
- Type checking
- Build or package verification
- Integration, migration, security, or end-to-end checks when justified

Do not promise exact output unless the output is stable and necessary. State the success condition:

```markdown
Run: `pnpm test src/orders/order-service.test.ts`
Success: command exits zero and all order cancellation cases pass.
```

## 10. Plan Quality Rules

A plan fails review when it contains:

- Invented files or interfaces
- Placeholder tasks
- Circular task dependencies
- Vague instructions
- Unowned behavior
- No acceptance criteria
- No deletion of superseded paths
- Tests unrelated to risk
- A migration with no recovery thinking
- Security-sensitive behavior with no authorization analysis
- Tasks that depend on undefined outputs
- Multiple canonical implementations after completion

Avoid:

- "Handle edge cases"
- "Add appropriate validation"
- "Refactor as needed"
- "Update relevant files"
- "Write tests"
- "Similar to the previous task"
- "Maintain compatibility" without an explicit requirement

Replace each with concrete behavior.

## 11. Self-Review

Before finalizing:

### Specification coverage

Map every requirement to at least one task.

### Architecture

Confirm the plan ends with one canonical path and clear ownership.

### Deletion

Confirm old code, compatibility shims, flags, exports, tests, and docs are removed.

### Interface consistency

Check all names, signatures, schemas, events, and task dependencies.

### Failure and security

Check authorization, invalid input, partial failure, concurrency, and destructive behavior where
relevant.

### Verification

Confirm every task has a realistic success check derived from the repository.

### Buildability

Ask: could a skilled engineer implement each task without inventing a missing contract?

Fix gaps before presenting the plan.

## 12. Independent Plan Review

For substantial plans, dispatch or perform an independent review after the complete plan is
written.

The reviewer should classify:

- **Blocker** — cannot implement safely or correctly
- **Major** — likely wrong architecture, missing requirement, or incomplete verification
- **Advisory** — useful improvement that does not block execution

Review:

- Requirement coverage
- Current-system accuracy
- Task boundaries
- Interface consistency
- Dependency order
- Deletion completeness
- Security and data risk
- Verification quality
- Buildability

Do not block on wording preferences.

## 13. Saving and Handoff

Default location:

```text
docs/plans/YYYY-MM-DD-<feature-name>.md
```

Respect repository or user conventions when different.

At handoff, report:

- Plan path
- Number of tasks
- Principal architectural decision
- Main deletion
- Highest-risk task
- Any unresolved assumption

Then offer execution through `executing-implementation-plans`.
