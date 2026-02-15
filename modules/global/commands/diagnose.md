---
description: Diagnose a code issue without making changes - find root cause first (usage: describe the issue)
---

## User Input

```text
$ARGUMENTS
```

## Instructions

You are in **DIAGNOSTIC MODE**. Your objective is to investigate the issue described above and arrive at a **root cause** before any code changes are made.

### CRITICAL CONSTRAINTS

1. **DO NOT MODIFY ANY CODE** until the user explicitly grants permission
2. **DO NOT CREATE ANY FILES** (no scripts, no documentation, no artifacts)
3. **FOCUS ON UNDERSTANDING** - read code, trace logic, verify assumptions
4. **ASK CLARIFYING QUESTIONS** if needed to narrow down the issue
5. **CONFIRM KEY ASSUMPTIONS** with the user before concluding

---

## Diagnostic Process

### Phase 1: Understand the Issue

1. Parse the user's issue description from `$ARGUMENTS`
2. Identify the affected area of code (files, functions, data flow)
3. State your initial hypothesis about what might be wrong

### Phase 2: Investigate

Use these investigation techniques (read-only):

| Technique | When to Use |
|-----------|-------------|
| **Read code** | Understand the implementation logic |
| **Search patterns** | Find related code, usages, dependencies |
| **Check test outputs** | Review actual vs expected results |
| **Trace data flow** | Follow data through the system |
| **Review ledger entries** | For financial calculation issues |
| **Check helper scripts** | `test/helper-scripts/` may have relevant diagnostics |

### Phase 3: Verify Assumptions

Before concluding, explicitly verify key assumptions:

1. **Code assumptions** - Is the code doing what you think it does?
2. **Data assumptions** - Is the data in the expected format/state?
3. **User assumptions** - Confirm understanding of expected behavior with user
4. **Integration assumptions** - Are components interacting correctly?

### Phase 4: Present Findings

Provide a structured summary:

```
## Diagnostic Summary

**Issue**: [One-line description of the problem]

**Root Cause**: [What is actually causing the issue]

**Evidence**:
- [Key finding 1]
- [Key finding 2]
- [Key finding 3]

**Assumptions Verified**:
- [Assumption 1]: [Confirmed/Refuted]
- [Assumption 2]: [Confirmed/Refuted]

**Proposed Fix**: [High-level description of the fix - DO NOT IMPLEMENT]

**Questions for User** (if any):
- [Question 1]
- [Question 2]
```

---

## Response Format

Begin your response with:

```
DIAGNOSTIC MODE - No code changes will be made without permission

Investigating: [brief issue summary]
```

Then proceed through the diagnostic phases, showing your work.

End with the Diagnostic Summary and explicitly ask:

```
Ready to proceed with the fix? Please confirm before I make any code changes.
```

---

## Example Interaction

**User**: /diagnose The audit is showing 53% tax rate which seems too high

**Agent Response**:
```
DIAGNOSTIC MODE - No code changes will be made without permission

Investigating: Audit showing unexpectedly high 53% tax rate

## Phase 1: Understanding

The tax burden fidelity check is reporting a 53% effective tax rate, which exceeds
the expected 5-40% bounds. This suggests either:
- A calculation error in the check itself
- An issue with the underlying tax modeling
- A mismatch in what "income" means for this calculation

## Phase 2: Investigation

[Agent reads relevant code, checks data, traces logic...]

## Phase 3: Verify Assumptions

Let me confirm:
- The check uses REVENUE debits as income: $5M
- Total tax from LIABILITY credits: $2.67M
- 2.67M / 5M = 53.4%

But wait - are retirement account withdrawals being counted as taxable income?
[Agent investigates further...]

## Diagnostic Summary

**Issue**: Tax burden fidelity check showing 53% effective rate

**Root Cause**: The check only counts REVENUE account debits as income ($5M),
but taxes are also applied to retirement account withdrawals ($20.5M) which
are ASSET credits. The income denominator is too small.

**Evidence**:
- REVENUE debits: $5,006,734
- ASSET credits (withdrawals): $20,508,373
- Total tax: $2,672,661
- Rate using REVENUE only: 53.4%
- Rate using REVENUE + withdrawals: 10.5%

**Assumptions Verified**:
- Tax is calculated on withdrawals: Confirmed
- REVENUE accounts capture all income: Refuted - misses withdrawals

**Proposed Fix**: Update the check to include ASSET credits (withdrawals)
in the income denominator alongside REVENUE debits.

Ready to proceed with the fix? Please confirm before I make any code changes.
```

---

## Reminders

- **Patience over speed** - Take time to understand before proposing fixes
- **Evidence over guessing** - Base conclusions on what you observe in code/data
- **Collaboration over dictation** - Work with the user to confirm understanding
- **Prevention over reaction** - Look for related issues that might have the same root cause
