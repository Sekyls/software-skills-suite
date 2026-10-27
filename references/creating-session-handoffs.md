---
name: creating-session-handoffs
description: >-
  Use when work must continue in another session, agent, or environment. Produces
  a compact, evidence-based handoff document that preserves objectives, decisions,
  repository state, completed work, verification, unresolved risks, and the next
  recommended action without duplicating specifications, plans, ADRs, commits, or
  diffs that can be referenced directly.
---

# Creating Session Handoffs

Give the next engineer or agent enough context to continue accurately without rereading the entire
conversation.

A handoff is a navigation and state document, not a replacement for specifications, plans, ADRs,
issues, commits, or code.

## 1. When to Use

Use when:

- The conversation or task will continue in another session
- A different agent will take over
- Work is paused at a meaningful boundary
- The context window is becoming difficult to manage
- A blocker requires another environment or person
- The user requests a handoff, recap, or continuation document

Do not create a handoff for completed one-shot work with no continuation need.

## 2. Source of Truth

Inspect available evidence:

- Current conversation
- Specifications
- Implementation plans
- ADRs
- Issues
- Repository status
- Branch or worktree
- Diffs
- Commits
- Test output
- Generated artifacts
- Blocker details

Reference existing artifacts rather than duplicating them.

Distinguish:

- Confirmed fact
- Decision
- Assumption
- Recommendation
- Unverified claim
- Blocker

## 3. Privacy and Security

Before writing:

- Remove API keys
- Remove passwords
- Remove tokens
- Remove private keys
- Remove unnecessary personal information
- Avoid copying sensitive payloads
- Avoid embedding secrets from logs
- Replace sensitive values with descriptive placeholders

Do not redact information required to continue when it can be safely described at a higher level.

## 4. Required Content

### Objective

What the project or current task is trying to achieve.

### Current state

Where work currently stands.

### Completed work

Only completed and evidenced outcomes.

### Decisions

Important decisions and rationale.

### Artifacts

Paths or links to specifications, plans, ADRs, reports, and generated files.

### Repository state

When available:

- Repository
- Branch
- Worktree
- Clean or dirty state
- Important uncommitted files
- Relevant commits
- Stashes or temporary work

### Verification

Commands actually run and observed results.

### Failed approaches

Experiments or hypotheses that were disproven and should not be repeated.

### Unresolved issues

Open questions, blockers, risks, and unverified areas.

### Next action

The smallest correct next step.

### Suggested skills

Which skills the next agent should use and in what order.

## 5. Handoff Format

Use:

```markdown
# Session Handoff: [Topic]

**Prepared for:** [Next session purpose, when known]

**Status:** In progress | Blocked | Ready for planning | Ready for execution | Ready for review

## Objective

## Current state

## Completed work
- [Evidence-based outcome]

## Decisions
- **Decision:** [What]
  - **Reason:** [Why]
  - **Implication:** [What the next agent must preserve]

## Artifacts
- `[path]` — [purpose]

## Repository state
- Repository:
- Branch/worktree:
- Working tree:
- Relevant commits:
- Important uncommitted changes:

## Verification
- `[command]` — PASS | FAIL | BLOCKED
  - Evidence: [concise result]

## Acceptance criteria status
- [Criterion] — VERIFIED | NOT VERIFIED | BLOCKED

## Failed approaches
- [Approach]
  - Evidence:
  - Do not repeat unless:

## Unresolved issues
- [Issue]
  - Why it matters:
  - Evidence available:
  - Decision needed:

## Risks and warnings

## Next recommended action
1. [Concrete next step]

## Suggested skills
1. `skill-name` — [why]
```

Omit unavailable repository fields rather than inventing values.

## 6. Avoid Duplication

Do not reproduce:

- Full specifications
- Full plans
- Full diffs
- Entire ADRs
- Long logs
- Complete test output
- Large code blocks

Reference them by path, commit, issue, or URL and summarize only the information needed to navigate.

## 7. Evidence Rules

Do not write:

- "All tests pass" without fresh observed evidence
- "The bug is fixed" when only code was changed
- "Ready to deploy" without deployment evidence
- "No risks remain"
- "The agent completed everything" without independent inspection

Use:

- **Passed**
- **Reviewed**
- **Expected**
- **Not verified**
- **Blocked**

## 8. Tailoring

When the user states what the next session will do, emphasize relevant context.

Examples:

### Next session will implement

Emphasize:

- Approved design
- Plan path
- Task order
- Interfaces
- Repository state
- Verification baseline

### Next session will debug

Emphasize:

- Reproduction
- Logs
- Boundary evidence
- Hypotheses tested
- Failed fixes
- Current strongest hypothesis

### Next session will review

Emphasize:

- Diff
- Acceptance criteria
- Risk areas
- Tests run
- Unverified claims
- Architectural decisions

### Next session will redesign

Emphasize:

- Design direction
- Screens
- Assets
- States
- Responsive behavior
- Accessibility constraints

## 9. Saving

Default to the operating system's temporary directory so the repository remains unchanged.

Use a clear name:

```text
handoff-YYYY-MM-DD-<topic>.md
```

Save inside the repository only when the user requests persistent project documentation.

## 10. Self-Review

Before delivering:

- [ ] Objective is clear
- [ ] Current state is accurate
- [ ] Completed work is evidence-based
- [ ] Decisions include rationale
- [ ] Existing artifacts are referenced rather than duplicated
- [ ] Repository state is not invented
- [ ] Verification lists only commands actually run
- [ ] Failed approaches are captured
- [ ] Unresolved issues are actionable
- [ ] Next action is concrete
- [ ] Sensitive information is removed
- [ ] Suggested skills match the next task
