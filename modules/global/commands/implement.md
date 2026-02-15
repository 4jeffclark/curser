---
description: Implement a feature - execute technical plan and archive documents (usage: FEATURE_NAME or description)
---

## User Input

```text
$ARGUMENTS
```

## Instructions

You are in **IMPLEMENTATION MODE**. Your objective is to implement the feature according to the technical plan, then archive the design documents.

### CRITICAL CONSTRAINTS

1. **REQUIRE PLAN AT MINIMUM** - plan must exist in `doc/backlog/` (spec is optional)
2. **FOLLOW THE PLAN** - implement according to the technical plan
3. **REUSE EXISTING CODE** - leverage identified code, DO NOT reinvent
4. **TEST AS YOU GO** - verify each component works before moving on
5. **ARCHIVE ON COMPLETION** - move documents to `doc/archive/` when done

---

## Implementation Process

### Phase 1: Parse Arguments and Find Documents

**Argument Interpretation Priority:**

1. **Literal filename** (primary): If `$ARGUMENTS` matches or closely matches an existing `*_PLAN.md` file in `doc/backlog/`, use that plan
   - Example: `CASHFLOW_RECONCILIATION` -> look for `doc/backlog/CASHFLOW_RECONCILIATION_PLAN.md`
   - Also try with `_PLAN` suffix if user included it

2. **Narrative description** (fallback): If no matching plan file exists, treat `$ARGUMENTS` as a feature description
   - Derive a SCREAMING_SNAKE_CASE feature name from the description
   - Inform user that `/plan` must be run first (cannot implement without a plan)

**Steps:**
1. List files in `doc/backlog/` to find existing plans and specs
2. Check if `$ARGUMENTS` matches any `*_PLAN.md` filename (case-insensitive)
3. If plan found: Also check for matching `*_SPEC.md` (optional)
4. If no plan found: Inform user to run `/plan` first - implementation requires a plan
5. Review plan (and spec if exists) to understand full scope

### Phase 2: Create Implementation Checklist

Based on the technical plan, create a todo list with:

1. **Setup tasks** - Any configuration or scaffolding needed
2. **Core implementation** - Main feature components
3. **Integration tasks** - Connecting to existing system
4. **Testing tasks** - Unit tests, integration tests
5. **Documentation tasks** - Code comments, inline docs
6. **doc/main updates** - Update DEVELOPER_GUIDE.md and/or END_USER_GUIDE.md as needed

### Phase 3: Execute Implementation

For each checklist item:

1. **Review plan section** - Understand what needs to be done
2. **Check for reuse** - Use existing code per plan
3. **Implement** - Write minimal code to accomplish the task
4. **Verify** - Test that the component works
5. **Check lints** - Fix any linter errors introduced

### Phase 4: Validate and Complete

1. **Run full test suite** - Ensure no regressions
2. **Verify acceptance criteria** - Check against spec
3. **Update doc/main** - Update DEVELOPER_GUIDE.md and/or END_USER_GUIDE.md with feature documentation
4. **Create implementation summary** - Document what was done
5. **Archive documents** - Move spec and plan to `doc/archive/`

---

## Document Archival

On successful completion, move documents:

```
doc/backlog/{FEATURE_NAME}_PLAN.md -> doc/archive/{FEATURE_NAME}_PLAN.md
doc/backlog/{FEATURE_NAME}_SPEC.md -> doc/archive/{FEATURE_NAME}_SPEC.md  (if exists)
```

Create a brief implementation summary in the archive:

```
doc/archive/{FEATURE_NAME}_IMPLEMENTATION.md
```

This summary should include:
- What was implemented
- Any deviations from the plan
- Files created or modified
- Documentation updated (doc/main files)
- How to use the feature
- Note if design phase was skipped (no spec)

---

## Response Format

Begin your response with:

```
IMPLEMENTATION MODE - Executing technical plan

Feature: [brief feature summary]
Specification: doc/backlog/{FEATURE_NAME}_SPEC.md [or "None - design phase skipped"]
Technical Plan: doc/backlog/{FEATURE_NAME}_PLAN.md
```

Then create a todo list and proceed through implementation.

End with a completion summary:

```
## Implementation Complete

**Feature**: {FEATURE_NAME}

**Files Created**:
- [file1.py]
- [file2.py]

**Files Modified**:
- [existing_file.py]: [what was changed]

**Documentation Updated**:
- doc/main/DEVELOPER_GUIDE.md: [section updated]
- doc/main/END_USER_GUIDE.md: [section updated] (if applicable)

**Tests Added**:
- [test_file.py]

**Documents Archived**:
- doc/archive/{FEATURE_NAME}_PLAN.md
- doc/archive/{FEATURE_NAME}_SPEC.md (if existed)
- doc/archive/{FEATURE_NAME}_IMPLEMENTATION.md

**Verification**:
- [ ] All acceptance criteria met
- [ ] All tests passing
- [ ] No linter errors
- [ ] Code follows existing patterns
- [ ] doc/main documentation updated

The feature is ready for use. [Brief usage instructions]
```

---

## Document Lifecycle

1. **Design Phase** (`/design`): Creates `{NAME}_SPEC.md` in `doc/backlog/`
2. **Planning Phase** (`/plan`): Creates `{NAME}_PLAN.md` in `doc/backlog/`
3. **Implementation Phase** (`/implement`): Implements the feature
4. **Completion**: Move all documents to `doc/archive/`

---

## Error Handling

**If plan is missing (BLOCKING - cannot proceed):**
```
Cannot proceed - technical plan not found.

Expected: doc/backlog/{FEATURE_NAME}_PLAN.md

Please run `/plan {FEATURE_NAME}` first to create the technical plan.
(You can skip `/design` if needed - `/plan` will gather requirements inline.)
```

**If spec is missing but plan exists (OK - proceed):**
```
Note: No specification found (design phase was skipped).
Proceeding with implementation based on technical plan only.

Plan: doc/backlog/{FEATURE_NAME}_PLAN.md
```

**If implementation fails:**
- Document the failure point
- Suggest how to resolve
- DO NOT archive incomplete work

---

## Reminders

- **Follow the plan** - Deviations should be documented and justified
- **Reuse is mandatory** - Use existing code as identified in plan
- **Test thoroughly** - Don't skip verification steps
- **Update doc/main** - DEVELOPER_GUIDE.md and/or END_USER_GUIDE.md must be updated for user-facing features
- **Archive properly** - Documents should be moved, not copied
- **Anti-proliferation** - Only create necessary files
