---
name: software-skills-suite
description: >-
  Design, plan, implement, debug, refactor, and review software using a coordinated
  engineering workflow. Includes React and Next.js guidance, architecture audits,
  interface redesign, and session handoffs. Use for repository-based software work
  or when explicitly requesting one of these workflows; choose only the guidance
  relevant to the current task.
---

# Software Skills Suite

Use the bundled guides to support the user's current software task. Select the
appropriate workflow rather than running every workflow in sequence.

## Choose the relevant guidance

For implementation, debugging, refactoring, code review, or technical design,
read [Senior Software Developer](references/senior-software-developer.md) as the
engineering foundation. Then read only the additional guides needed:

| Task | Guide | When to use |
| --- | --- | --- |
| React or Next.js work | [Senior React Developer](references/senior-react-developer.md) | Components, state, effects, data fetching, rendering, forms, or server/client boundaries. |
| Feature design | [Designing Features](references/designing-features.md) | Product behavior, scope, architecture, or acceptance criteria remain materially unclear. |
| Implementation planning | [Writing Implementation Plans](references/writing-implementation-plans.md) | A substantial change needs a written plan grounded in repository evidence. |
| Plan execution | [Executing Implementation Plans](references/executing-implementation-plans.md) | The user wants an existing approved plan implemented and verified. |
| Architecture audit | [Architecture Audit](references/architecture-audit.md) | The user wants structural improvement candidates and recommendations. |
| Interface redesign | [Premium Interface Redesign](references/premium-interface-redesign.md) | An existing website or app needs visual or interaction improvements. Add the React guide when relevant. |
| Session handoff | [Creating Session Handoffs](references/creating-session-handoffs.md) | Work must continue in another session or the user requests a continuation document. |

A standalone handoff needs only the handoff guide and the evidence needed to
describe the current state accurately. A clear local fix can proceed with the
engineering foundation and any relevant framework guidance.

## Resolve references within the suite

The eight guides retain their original names and YAML headers for provenance.
They are bundled reference documents, not separately installed skills. When a
guide says to apply, invoke, or hand off to a named guide in the table, read that
local reference and continue the corresponding workflow within this skill.
There is no dependency on another installation of those eight skills.

Treat a transition between workflows as a change in the work being performed,
not permission to create another chat, delegate work, or perform external actions.
Use another specialized skill only when it is available and needed for the task.

## Preserve the user's scope

The user's explicit instructions and existing authorization govern the task.
Do not repeat an approval request already satisfied in the conversation. Resolve
materially missing decisions before dependent work, while continuing useful
independent work where possible. An audit request authorizes recommendations;
an implementation request authorizes the requested implementation.

The guides provide templates and detailed checklists. Scale them to the actual
change, preserving the evidence, behavior, and verification that matter. Do not
require a design document, written plan, audit, or handoff for every software task.

Keep unrelated working changes intact. Ground findings in repository evidence,
verify outcomes with appropriate checks, and distinguish observed results from
expectations and work that remains unverified.
