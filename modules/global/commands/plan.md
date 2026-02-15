---
description: Plan a feature - create technical plan document in doc/backlog (usage: FEATURE_NAME or description)
---

## User Input

```text
$ARGUMENTS
```

## Instructions

You are in **PLANNING MODE**. Your objective is to create a comprehensive technical plan document based on the feature specification.

### CRITICAL CONSTRAINTS

1. **DO NOT IMPLEMENT ANY CODE** - this is a planning-only phase
2. **CREATE ONLY ONE FILE** - the plan document in `doc/backlog/`
3. **PREFER EXISTING SPECIFICATION** - look for `{FEATURE_NAME}_SPEC.md` in `doc/backlog/`
4. **CONFIRM TECHNICAL DECISIONS** with the user before finalizing
5. **USE THE TEMPLATE** - follow `doc/backlog/FEATURE_PLAN_TEMPLATE.md` structure

---

## Planning Process

### Phase 1: Parse Arguments and Find Specification

**Argument Interpretation Priority:**

1. **Literal filename** (primary): If `$ARGUMENTS` matches or closely matches an existing `*_SPEC.md` file in `doc/backlog/`, use that specification
   - Example: `CASHFLOW_RECONCILIATION` -> look for `doc/backlog/CASHFLOW_RECONCILIATION_SPEC.md`
   - Also try with `_SPEC` suffix if user included it

2. **Narrative description** (fallback): If no matching spec file exists, treat `$ARGUMENTS` as a feature description
   - Derive a SCREAMING_SNAKE_CASE feature name from the description
   - Proceed without a spec (design phase was skipped)

**Steps:**
1. List files in `doc/backlog/` to find existing specs
2. Check if `$ARGUMENTS` matches any `*_SPEC.md` filename (case-insensitive)
3. If match found: Use that spec as the basis for planning
4. If no match: Inform user that `/design` was skipped and proceed with inline requirements gathering

### Phase 2: Research Implementation

Use these investigation techniques (read-only):

| Technique | When to Use |
|-----------|-------------|
| **Read existing code** | Find patterns to reuse, understand architecture |
| **Search codebase** | Identify integration points, dependencies |
| **Review similar features** | Learn from existing implementations |
| **Check test patterns** | Understand testing conventions |
| **Review helper scripts** | `test/helper-scripts/` for utilities |

### Phase 3: Draft Technical Plan

Create a technical plan document covering:

1. **Code Reuse Principles** - Existing code to leverage (CRITICAL)
2. **Architecture Overview** - System components and data flow
3. **Data Model** - Structures, schemas, validation rules
4. **API/Interface Design** - Function signatures, CLI commands
5. **Integration Points** - How feature connects to existing system
6. **Implementation Details** - Modules, dependencies, configuration
7. **Error Handling** - How errors are detected, reported, recovered
8. **Testing Strategy** - Unit, integration, end-to-end approach
9. **Documentation Updates** - Required updates to doc/main (DEVELOPER_GUIDE.md, END_USER_GUIDE.md)

### Phase 4: Review with User

Before creating the document:

1. **Summarize technical approach** - Confirm architecture decisions
2. **Identify reuse opportunities** - List existing code to leverage
3. **Estimate complexity** - Note any challenging areas
4. **Get approval** - Confirm user is ready to proceed

---

## Document Output

Create the technical plan document at:

```
doc/backlog/{FEATURE_NAME}_PLAN.md
```

**Naming Convention:**
- Use SCREAMING_SNAKE_CASE matching the spec
- Example: `CASHFLOW_RECONCILIATION_PLAN.md`

**Document Structure:**
Follow the template in `doc/backlog/FEATURE_PLAN_TEMPLATE.md`

---

## Response Format

Begin your response with:

```
PLANNING MODE - Creating technical plan

Feature: [brief feature summary]
Specification: doc/backlog/{FEATURE_NAME}_SPEC.md [or "None - design phase skipped"]
```

**If no spec exists (design phase skipped):**
```
No specification found for: {FEATURE_NAME}

Proceeding without formal spec (design phase skipped).

I will gather requirements inline before creating the technical plan.
Please describe:
1. What problem does this feature solve?
2. What are the key requirements?
3. Any constraints or considerations?
```

Then gather requirements and proceed through the planning phases, showing your work.

End with a summary of what was created:

```
## Planning Complete

**Technical Plan Created**: `doc/backlog/{FEATURE_NAME}_PLAN.md`

**Key Technical Decisions**:
- [Decision 1]
- [Decision 2]

**Code Reuse Summary**:
- [100% Reuse]: [Components]
- [Reuse + Enhance]: [Components]
- [New Code]: [Components]

**Estimated Complexity**: [Low/Medium/High]

Next step: Run `/implement {FEATURE_NAME}` to implement the feature.
```

---

## Document Lifecycle

1. **Design Phase** (`/design`): Creates `{NAME}_SPEC.md` in `doc/backlog/`
2. **Planning Phase** (`/plan`): Creates `{NAME}_PLAN.md` in `doc/backlog/`
3. **Implementation Phase** (`/implement`): Implements the feature
4. **Completion**: Move both documents to `doc/archive/`

---

## Reminders

- **Reuse is mandatory** - Identify existing code BEFORE proposing new code
- **Architecture matters** - Ensure feature fits existing patterns
- **Test strategy required** - Plan how to verify the implementation
- **Questions are good** - Better to clarify than assume
- **Anti-proliferation** - Only create the plan document, nothing else
