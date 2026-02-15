---
description: Design a feature - create specification document in doc/backlog (usage: describe the feature)
---

## User Input

```text
$ARGUMENTS
```

## Instructions

You are in **DESIGN MODE**. Your objective is to create a comprehensive feature specification document based on the feature description above.

### CRITICAL CONSTRAINTS

1. **DO NOT IMPLEMENT ANY CODE** - this is a design-only phase
2. **CREATE ONLY ONE FILE** - the specification document in `doc/backlog/`
3. **ASK CLARIFYING QUESTIONS** - ensure you understand requirements before documenting
4. **CONFIRM KEY DECISIONS** with the user before finalizing the spec
5. **USE THE TEMPLATE** - follow `doc/backlog/FEATURE_SPEC_TEMPLATE.md` structure

---

## Design Process

### Phase 1: Understand the Feature

1. Parse the user's feature description from `$ARGUMENTS`
2. Identify the core problem being solved
3. State your initial understanding of the feature scope
4. Ask clarifying questions about any ambiguous requirements

### Phase 2: Research Existing Code

Use these investigation techniques (read-only):

| Technique | When to Use |
|-----------|-------------|
| **Read code** | Understand existing implementations to reuse |
| **Search patterns** | Find related code, existing patterns, dependencies |
| **Review architecture** | Understand how feature fits into system |
| **Check helper scripts** | `test/helper-scripts/` may have relevant utilities |

### Phase 3: Draft Specification

Create a specification document covering:

1. **Problem Statement** - What pain points does this solve?
2. **Solution Overview** - High-level approach (not implementation)
3. **Functional Requirements** - What the system must do
4. **Non-Functional Requirements** - Performance, reuse, maintainability
5. **User Stories** - How users will interact with the feature
6. **Acceptance Criteria** - How to verify the feature works
7. **Documentation Impact** - What doc/main files need updates (DEVELOPER_GUIDE.md, END_USER_GUIDE.md)
8. **Open Questions** - Items needing further clarification

### Phase 4: Review with User

Before creating the document:

1. **Summarize key decisions** - Confirm understanding
2. **Present trade-offs** - Discuss any alternatives considered
3. **Identify risks** - Note any potential issues
4. **Get approval** - Confirm user is ready to proceed

---

## Document Output

Create the specification document at:

```
doc/backlog/{FEATURE_NAME}_SPEC.md
```

**Naming Convention:**
- Use SCREAMING_SNAKE_CASE for feature name
- Example: `CASHFLOW_RECONCILIATION_SPEC.md`

**Document Structure:**
Follow the template in `doc/backlog/FEATURE_SPEC_TEMPLATE.md`

---

## Response Format

Begin your response with:

```
DESIGN MODE - Creating feature specification

Feature: [brief feature summary]
```

Then proceed through the design phases, showing your work.

End with a summary of what was created:

```
## Design Complete

**Specification Created**: `doc/backlog/{FEATURE_NAME}_SPEC.md`

**Key Decisions**:
- [Decision 1]
- [Decision 2]

**Open Questions** (to address in planning phase):
- [Question 1]
- [Question 2]

Next step: Run `/plan {FEATURE_NAME}` to create the technical plan.
```

---

## Document Lifecycle

1. **Design Phase** (`/design`): Creates `{NAME}_SPEC.md` in `doc/backlog/`
2. **Planning Phase** (`/plan`): Creates `{NAME}_PLAN.md` in `doc/backlog/`
3. **Implementation Phase** (`/implement`): Implements the feature
4. **Completion**: Move both documents to `doc/archive/`

---

## Reminders

- **Reuse over reinvention** - Identify existing code to leverage
- **User value first** - Focus on what problem is being solved
- **Questions are good** - Better to clarify than assume
- **Keep it simple** - Start with MVP, note future enhancements
- **Anti-proliferation** - Only create the spec document, nothing else
