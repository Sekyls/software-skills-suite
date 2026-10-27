---
name: architecture-audit
description: >-
  Use to proactively inspect an existing codebase for high-value architectural
  improvements rather than to implement a specific requested feature. Identifies
  structural friction, shallow modules, weak ownership, duplicated knowledge,
  tangled dependencies, difficult test surfaces, and deletion opportunities;
  ranks concrete candidates by impact, evidence, cost, and risk; and produces a
  decision-ready report grounded in the repository and domain language.
---

# Architecture Audit

Find architectural changes that make the codebase easier to understand, test, change, and delete.

Apply `senior-software-developer` and any relevant framework skill.

This skill diagnoses and recommends. It does not implement architecture changes until the user
selects a candidate and the work proceeds through feature design or implementation planning.

## 1. When to Use

Use when:

- The user asks how to improve the codebase architecture
- The system feels difficult to navigate or test
- Changes require touching many unrelated files
- Modules expose interfaces almost as complex as their implementations
- The same domain rule appears in several places
- Circular dependencies or unclear ownership are common
- A major refactor needs candidate discovery
- AI agents or engineers repeatedly misunderstand the same area

Do not use for:

- A clear local bug
- Routine feature work with known ownership
- Pure visual redesign
- General code review of one small diff

## 2. Architectural Vocabulary

Use precise terms naturally:

### Module

A coherent unit that owns behavior or knowledge.

### Interface

The surface consumers must understand.

### Depth

How much useful complexity a module hides behind a comparatively simple interface.

### Shallow module

A module whose interface is nearly as complex as its implementation or merely forwards work.

### Seam

A stable place where responsibilities can vary independently.

### Locality

How much relevant knowledge is available together when understanding or changing behavior.

### Leverage

How much complexity or repeated knowledge one module removes from its consumers.

### Adapter

A module that translates between genuinely different contracts or technologies.

Do not force these terms when repository or domain language communicates more clearly.

## 3. Read the Domain First

Before scanning broadly:

1. Read project documentation.
2. Read domain glossaries or context files.
3. Read relevant ADRs.
4. Inspect package and directory structure.
5. Identify major runtime boundaries.
6. Learn the repository's names for important concepts.

Use domain language in recommendations.

If documentation and code disagree, report the inconsistency.

ADRs are evidence of prior decisions, not unquestionable law. Reopen an ADR only when current
friction is concrete and significant.

## 4. Exploration Strategy

Explore organically, then validate findings with evidence.

Look for:

- Understanding one concept requires opening many tiny files
- Public interfaces mirror internal complexity
- Domain logic is scattered across controllers, components, jobs, and persistence
- Modules leak internal data structures
- Callers repeat sequencing, validation, or error handling
- Pure helpers were extracted but real complexity remains in orchestration
- Multiple services own the same rule
- One module has several unrelated reasons to change
- Tests require mocking large internal graphs
- Integration behavior is untested because no stable interface exists
- A compatibility layer preserves two canonical paths
- Cross-layer imports create cycles
- Configuration controls behavior no longer used
- Feature flags or migration paths were never removed
- Important concepts have no named owner
- Generic abstractions hide domain behavior
- Repeated branching indicates a missing domain operation
- Files change together across many commits despite living apart

Do not rely on line count alone.

## 5. Evidence Collection

For every candidate, collect:

- Relevant files and modules
- Concrete examples
- Import or call relationships
- Repeated logic or knowledge
- Tests affected
- Change history when available
- User or developer friction
- Existing ADR or documentation constraints
- What can be deleted
- What behavior must remain

Distinguish:

- **Observed** — directly supported by repository evidence
- **Inferred** — likely consequence supported by evidence
- **Speculative** — plausible but not yet demonstrated

## 6. The Deletion Test

For a suspected shallow module, ask:

> If this module were deleted and its responsibility moved to the correct owner, would the system
> become more concentrated and understandable, or would complexity merely be displaced?

A strong deletion candidate:

- Exists mainly to forward calls
- Adds naming without hiding complexity
- Forces consumers to understand internals anyway
- Duplicates an existing boundary
- Preserves an obsolete interface
- Requires synchronized changes across both old and new paths

Do not recommend deletion when the module:

- Protects a real external boundary
- Encapsulates volatile infrastructure
- Owns a stable domain operation
- Provides meaningful policy or invariants
- Supports multiple genuinely different implementations

## 7. Deepening Opportunities

A high-value deepening opportunity usually:

- Moves knowledge from many consumers into one owner
- Simplifies the public interface
- Improves locality
- Reduces required mocks
- Makes behavior testable through one stable surface
- Deletes forwarding layers or repeated orchestration
- Reduces the number of files changed for common work
- Aligns module names with domain concepts

Do not invent abstractions without demonstrated consumers.

One adapter may be provisional. Two genuinely different integrations often establish a real seam.

## 8. Candidate Scoring

Score each candidate from 1–5:

### Impact

How much developer or system friction it removes.

### Evidence

How directly the repository supports the diagnosis.

### Deletion

How much obsolete or duplicated code can be removed.

### Testability

How much the change improves meaningful test surfaces.

### Cost

Implementation effort and migration complexity.

### Risk

Likelihood of regressions, data issues, or operational disruption.

Use the scores to rank candidates, not to create false mathematical precision.

## 9. Recommendation Strength

Classify each candidate:

### Strong

- Clear repeated friction
- High evidence
- Coherent target owner
- Meaningful deletion
- Manageable risk

### Worth exploring

- Real friction
- Plausible target design
- Some uncertainty in ownership or cost

### Speculative

- Interesting pattern
- Limited evidence
- Requires focused investigation before planning

Do not present speculative ideas as established defects.

## 10. Report Format

Default to a Markdown report:

```markdown
# Architecture Audit

## Executive summary

## System map
- Major modules
- Runtime boundaries
- Important domain concepts

## Candidate 1: [Domain-oriented title]

**Strength:** Strong | Worth exploring | Speculative

**Files:**
- `path`

**Observed friction:**
- [Concrete evidence]

**Current shape:**
- [How responsibility is distributed]

**Proposed target:**
- [The deeper owner and simpler interface]

**Deletion:**
- [Files, wrappers, branches, or duplicated logic removed]

**Benefits:**
- Locality:
- Leverage:
- Testability:
- Change surface:

**Risks:**
- [Concrete risk]

**Scores:**
- Impact: X/5
- Evidence: X/5
- Deletion: X/5
- Testability: X/5
- Cost: X/5
- Risk: X/5

**Conflicts:**
- [ADR or documented decision, if any]

## Top recommendation
- [Candidate and why]

## Not recommended
- [Tempting refactors rejected due to weak evidence]
```

## 11. Optional Visual Report

Create a visual HTML report only when:

- The user requests it
- Dependency or flow diagrams materially improve understanding
- Several candidates require before/after comparison

The report must be self-contained and saved outside the repository unless requested otherwise.

Visuals may include:

- Dependency graphs
- Call flows
- Before/after module diagrams
- Change-surface maps
- Data-flow diagrams

Do not use visual polish as a substitute for architectural evidence.

## 12. Candidate Exploration

After presenting candidates, ask the user to select one.

For the selected candidate:

1. Re-inspect the relevant area deeply.
2. Define current invariants.
3. Identify the target owner.
4. Design the smallest useful interface.
5. List consumers to update.
6. Define deletion.
7. Define tests that should survive the refactor.
8. Identify ADRs or domain terms to update.
9. Hand off to `designing-features` when product or architectural decisions remain.
10. Hand off to `writing-implementation-plans` when the target design is sufficiently clear.

Do not implement directly from the audit report.

## 13. Quality Rules

Do not recommend:

- Generic "clean architecture" layering without repository evidence
- New interfaces for one hypothetical implementation
- Splitting files solely by line count
- Combining modules solely because names are similar
- Microservices as a default improvement
- Repositories, managers, handlers, or factories as pattern decoration
- A shared library that centralizes unrelated behavior
- Compatibility layers to make a refactor easier
- Rewrites without a deletion and migration story
- ADR reversal without concrete current friction

## 14. Self-Review

Before presenting:

- [ ] Domain language is accurate
- [ ] Every candidate cites concrete repository evidence
- [ ] Observed, inferred, and speculative claims are separated
- [ ] Each candidate has a coherent target owner
- [ ] Deletion is explicit
- [ ] Testability improvement is concrete
- [ ] Costs and risks are not minimized
- [ ] ADR conflicts are disclosed
- [ ] Top recommendation is justified
- [ ] Weak theoretical refactors were omitted
