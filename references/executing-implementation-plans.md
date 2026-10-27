---
name: executing-implementation-plans
description: >-
  Use to implement an approved written plan in an existing repository. Reviews the
  plan against current repository evidence, executes tasks in dependency order,
  adapts minor stale details without ceremony, stops on material design or safety
  conflicts, verifies every completed task, deletes superseded paths, preserves
  unrelated work, and reports only evidence actually observed.
---

# Executing Implementation Plans

Execute the intended design, not the wording of a stale document.

Apply `senior-software-developer` and any relevant framework skill throughout execution.

The plan is an approved hypothesis. Repository evidence, safety, and the user's current
requirements outrank it.

## 1. Start Safely

Before editing:

1. Read the complete plan.
2. Read referenced specifications.
3. Inspect repository status.
4. Identify current branch or worktree.
5. Confirm no unrelated user changes will be overwritten.
6. Inspect the files and interfaces named by the first tasks.
7. Identify plan assumptions that have already become stale.
8. Build a task checklist preserving dependency order.

Do not begin on an unsafe shared branch when an isolated branch or worktree is available.

Never discard unrelated changes.

## 2. Validate the Plan

Check:

- Does the current repository match the plan's described architecture?
- Do named files and interfaces exist?
- Are task dependencies valid?
- Does the plan end with one canonical implementation?
- Are obsolete paths scheduled for deletion?
- Are commands available in the repository?
- Are security, data, migration, and operational risks adequately addressed?

Classify deviations.

### Minor deviation

Examples:

- File moved
- Line numbers changed
- Equivalent repository command exists
- Local naming differs
- A planned helper already exists

Action: adapt directly, preserve intent, and record the deviation.

### Material deviation

Examples:

- Planned interface is wrong
- Ownership boundary is wrong
- A dependency does not exist
- The design duplicates an existing system
- The task order cannot work
- A different architecture is required
- Scope changes substantially

Action: stop that task, revise the plan or present the issue before proceeding.

### Safety-critical deviation

Examples:

- Data-loss risk
- Authorization flaw
- Destructive migration without recovery
- Secret exposure
- Irreversible production operation
- Uncontrolled concurrency or money movement

Action: stop immediately. Do not improvise.

## 3. Task Execution Loop

For each task:

### A. Re-read the task

Confirm:

- Purpose
- Dependencies
- Files
- Interfaces
- Acceptance criteria
- Verification
- Deletion work

### B. Inspect current code

Read the exact current implementation and all relevant consumers.

Search before creating new code.

### C. Establish a baseline

For bugs or behavior changes:

- Reproduce the issue, or
- Run the focused existing test, or
- Add a characterization/regression test when useful

Record what actually happened.

### D. Implement the smallest coherent change

- Follow the target ownership
- Keep one canonical path
- Update all owned consumers
- Delete replaced code
- Remove stale aliases, exports, flags, tests, docs, dependencies, and configuration
- Avoid unrelated refactors
- Preserve security and data invariants

Do not leave a compatibility shim merely to reduce the diff.

### E. Verify narrowly

Run the task's focused checks.

Read failures and correct the hypothesis. Do not repeatedly rerun unchanged commands.

### F. Review the diff

Check:

- Acceptance criteria
- Unintended behavior
- Dead code
- Incomplete deletion
- Secrets
- Debug output
- Formatting noise
- Unrelated changes

### G. Broaden verification

Run the justified package, integration, type, lint, build, migration, security, or end-to-end
checks.

### H. Record completion

Mark the task complete only when:

- Its implementation is present
- Superseded paths are removed
- Focused verification passes
- Remaining uncertainty is explicitly recorded

## 4. Tests and Verification

Use the plan's verification as a starting point, not a substitute for judgment.

Run:

1. Focused reproduction or test
2. Tests for changed modules
3. Static analysis, type checking, lint, and formatting
4. Integration or contract tests
5. Build or package checks
6. Broader suite when risk justifies it
7. Migration, security, performance, or end-to-end checks where relevant

Never state that a test passed without observing a successful run.

If a command fails:

- Read the failure
- Determine whether it is caused by the change
- Fix the cause
- Rerun the narrowest relevant command
- Broaden only after the narrow check passes

If a command cannot run, record:

- Exact command
- Exact blocker
- What remains unverified
- Substitute evidence

### Requirements verification

Passing tests does not prove every requirement was implemented.

Before completing each task and the overall plan:

1. Re-read every acceptance criterion.
2. Map it to implementation evidence.
3. Map it to test, inspection, or runtime evidence.
4. Report any criterion not directly verified.

### Delegated work

When another agent or process performed work:

1. Inspect the actual repository diff.
2. Confirm files and interfaces exist.
3. Run relevant verification independently.
4. Compare the result against acceptance criteria.
5. Do not accept the delegate's success report as proof.

## 5. Handling Plan Errors

Do not blindly follow incorrect steps.

Correct directly when:

- The repository provides an obvious equivalent
- The adjustment does not alter architecture, scope, risk, or public behavior
- The plan's intent remains intact

Stop and revise when:

- The intended design cannot be implemented as written
- A task consumes an undefined interface
- New information changes security or data risk
- The plan would create duplicate canonical paths
- Required work lies outside approved scope
- A deletion would affect an unowned external consumer
- A planned migration is unsafe

Explain the conflict with repository evidence.

## 6. Breaking Changes

Breaking changes are allowed and often desirable.

When replacing an interface:

1. Search all repository consumers.
2. Update every owned consumer.
3. Update tests and documentation.
4. Delete the old interface.
5. Delete aliases, adapters, re-exports, fallback branches, and compatibility tests.
6. Search again to confirm no owned references remain.
7. Run broad verification appropriate to the blast radius.

Do not preserve an old path because it is convenient.

When an external consumer may exist and cannot be inspected, report that uncertainty. Do not
silently create permanent compatibility code.

## 7. Data and Migration Execution

Before executing data changes:

- Confirm the target environment
- Confirm backups or recovery strategy where required
- Confirm transaction and lock behavior
- Estimate scope
- Verify scripts are restartable when needed
- Add progress and failure visibility
- Test on representative data when possible

Never run destructive production operations implicitly.

Temporary migration paths must be deleted as soon as the transition is complete.

## 8. Security-Sensitive Execution

For authentication, authorization, secrets, uploads, payments, destructive operations, or external
input:

- Re-check trust boundaries
- Test denied and invalid cases
- Verify no fail-open behavior
- Check logs and errors for leakage
- Review race and replay behavior
- Run relevant security tooling when available

A happy-path test is insufficient.

## 9. Commits and Checkpoints

Commit by coherent review unit.

A good checkpoint:

- Implements one meaningful outcome
- Passes its relevant checks
- Does not contain unrelated cleanup
- Leaves the repository in an understandable state

Do not commit every tiny mechanical step. Do not combine unrelated tasks merely to reduce commit
count.

Before any destructive Git operation, require explicit user permission.

## 10. Completion Gate

Before declaring the plan complete:

### Requirements

- [ ] Every acceptance criterion is implemented
- [ ] Every acceptance criterion has explicit evidence
- [ ] Every task is complete or explicitly deferred by the user
- [ ] No placeholder implementation remains

### Architecture

- [ ] One canonical path remains
- [ ] Ownership matches the intended design
- [ ] No unnecessary wrapper, abstraction, or duplicate implementation remains

### Deletion

- [ ] Replaced files and APIs are deleted
- [ ] Compatibility shims are deleted
- [ ] Stale exports, tests, docs, flags, dependencies, and configuration are removed
- [ ] Repository search finds no unintended references

### Quality

- [ ] Root cause is fixed
- [ ] Security and data invariants hold
- [ ] Error and failure paths are handled
- [ ] No debug code or secrets remain
- [ ] Final diff contains no unrelated changes

### Verification

- [ ] Focused tests pass
- [ ] Relevant static checks pass
- [ ] Build or package verification passes where applicable
- [ ] Higher-risk checks pass where applicable
- [ ] Delegated work was independently inspected
- [ ] Unrun checks are clearly reported

## 11. Final Report

Report:

### Implemented

- Completed behavior
- Key architectural decision
- Main simplification or deletion

### Changed

- Important files
- Interfaces
- Data or configuration

### Removed

- Old APIs
- Compatibility layers
- Dead code
- Obsolete tests or dependencies

### Verification

For each command:

```text
command — PASS | FAIL | BLOCKED
```

Include only commands actually attempted.

### Acceptance criteria

For each criterion:

```text
criterion — VERIFIED | NOT VERIFIED | BLOCKED
evidence — [test, inspection, or runtime result]
```

### Deviations

- Minor plan adaptations
- Material changes approved during execution

### Remaining risk

- Unverified areas
- External consumers not inspectable
- Operational actions still required
- Known limits

Do not claim "production-ready," "fully secure," or "all tests pass" unless the evidence genuinely
supports the exact statement.

## 12. Stop Conditions

Stop rather than guess when:

- A safety-critical assumption is missing
- The plan conflicts materially with repository evidence
- A destructive operation could affect real data
- Required credentials or infrastructure are unavailable
- Verification repeatedly fails without a supported hypothesis
- Continuing would overwrite unrelated work
- The requested outcome has changed

A blocker is useful information. Report it precisely.
