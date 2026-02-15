---
description: Re-read project documentation to re-establish context (usage: docs, patterns, code, helpers, all)
---

## User Input

```text
$ARGUMENTS
```

## Instructions

Parse the user input to determine which context category to refresh. Match fuzzy/partial input to these categories:

| User Input (fuzzy match) | Category |
|--------------------------|----------|
| `help`, `?`, `usage` | **HELP** - Show usage instructions |
| `docs`, `doc`, `documentation`, `guides` | **DOCS** - Product documentation only |
| `patterns`, `work`, `workflow`, `rules`, `principles`, `constitution` | **PATTERNS** - Work patterns and principles only |
| `code`, `style`, `coding`, `conventions` | **CODE** - Coding conventions and architecture patterns |
| `helpers`, `helper`, `scripts`, `debug`, `troubleshoot` | **HELPERS** - Helper scripts library for debugging |
| `all`, `everything`, `full`, empty/blank | **ALL** - Complete context refresh |

If input is ambiguous or unrecognized, default to **ALL**.

---

## HELP Category

Display this usage guide and do NOT read any files:

```
/refreshcontext - Re-establish project context

Usage:
  /refreshcontext [category]

Categories:
  help, ?      Show this help message
  docs         Read product documentation (Developer Guide, End User Guide)
  patterns     Read work patterns (Constitution, principles)
  code         Read coding conventions (Python style, architecture, testing)
  helpers      Read helper scripts library (debugging and validation utilities)
  all          Read everything (default if no argument provided)

Examples:
  /refreshcontext docs       - Just the documentation
  /refreshcontext work       - Just the work patterns and principles
  /refreshcontext patterns   - Same as above
  /refreshcontext code       - Coding conventions and architecture
  /refreshcontext helpers    - Helper scripts for debugging
  /refreshcontext all        - Full context refresh
  /refreshcontext            - Same as 'all'
```

After displaying help, stop. Do not read any files.

---

## DOCS Category

Read these files for product documentation context:

1. **Developer Guide**: `doc/main/DEVELOPER_GUIDE.md`
2. **End User Guide**: `doc/main/END_USER_GUIDE.md`

After reading, summarize:
- Key product capabilities
- How developers interact with the codebase
- How end users interact with the product

---

## PATTERNS Category

Read this file for work patterns and principles:

1. **Constitution**: `.specify/memory/constitution.md` - Authoritative source for all project principles

After reading, confirm understanding of these NON-NEGOTIABLE principles:

1. **Ledger as Ground Truth** - NEVER calculate financial state from memory; ALWAYS query the ledger
2. **Anti-Proliferation** - Do NOT create documentation, scripts, or artifacts unless explicitly requested
3. **Deterministic Account Identification** - Use exact matching, not fuzzy string matching
4. **Accurate Transaction Visibility** - Never artificially modify or hide ledger values
5. **Separation of Concerns** - Audit system uses file-only access, never runtime objects
6. **Start with Working Code** - Always begin with existing patterns, never reinvent

---

## CODE Category

Read these files for coding conventions and architecture patterns:

1. **Python Style**: `.cursor/rules/python-style.mdc` - Naming, imports, type hints, error handling
2. **Architecture Patterns**: `.cursor/rules/architecture-patterns.mdc` - Service patterns, code reuse, logging
3. **Testing Patterns**: `.cursor/rules/testing-patterns.mdc` - Test structure, coverage, fixtures
4. **File Organization**: `.cursor/rules/file-organization.mdc` - Directory structure, naming conventions

After reading, summarize key conventions for:
- Code style and organization
- Service architecture patterns
- Testing requirements

---

## HELPERS Category

List the contents of `test/helper-scripts/` to understand available debugging and validation utilities.

**Purpose**: The helper-scripts library contains reusable debugging and validation scripts that have been tested and proven useful. This library should grow organically over time.

**CRITICAL Guidelines**:

1. **Always Check First**: Before creating ANY new debugging or validation script, check `test/helper-scripts/` for existing scripts that can be used or adapted
2. **Reuse and Adapt**: Prefer modifying or extending existing helper scripts over creating new ones
3. **Contribute Back**: If you create a useful debugging script elsewhere (e.g., in a devworkspace), move it to `test/helper-scripts/` so it becomes part of the shared library
4. **Naming Convention**: Use descriptive prefixes: `check_*`, `validate_*`, `analyze_*`, `compare_*`, `inspect_*`, `verify_*`, `walk_*`, `calc_*`

After listing, categorize the scripts by purpose:
- **check_*** - Quick validation checks
- **validate_*** - Comprehensive validation
- **analyze_*** - Deep analysis and diagnostics
- **compare_*** - Comparison utilities
- **inspect_*** - Data inspection
- **verify_*** - Verification utilities
- **walk_*** - Data traversal utilities
- **calc_*** - Calculation utilities

---

## ALL Category

Read everything from DOCS, PATTERNS, CODE, and HELPERS categories above.

Provide a comprehensive summary covering:
1. Product documentation highlights
2. Critical principles and constraints
3. Coding conventions and architecture patterns
4. Available helper scripts for debugging (with category counts)

---

## Response Format

Begin your response with:

```
Context Refresh: [CATEGORY]
```

Then provide a **concise bullet list of topic headings only** showing what you learned. Keep each item to a short phrase. Do not elaborate or explain — just confirm what was consumed.

### Example Output (DOCS)

```
Context Refresh: DOCS (last updated: 2025-01-27)

Learned:
- Developer Guide: project setup, CLI commands, testing procedures
- End User Guide: product overview, input requirements, output formats
```

### Example Output (PATTERNS)

```
Context Refresh: PATTERNS

Learned:
- Ledger-as-Ground-Truth principles
- Anti-Proliferation rules
- Deterministic Account Identification
- Accurate Transaction Visibility
- Separation of Concerns (Reporting/Auditing)
- Code Reuse and Consolidation patterns
```

### Example Output (CODE)

```
Context Refresh: CODE

Learned:
- Python Style: naming, imports, type hints, error handling
- Architecture: service patterns, code reuse, logging levels
- Testing: structure, coverage, fixtures, devworkspace
- File Organization: directory structure, naming conventions
```

### Example Output (HELPERS)

```
Context Refresh: HELPERS

Learned:
- Helper Scripts Library: 72 scripts available
  - check_* (28): validation checks
  - validate_* (10): comprehensive validation
  - analyze_* (9): deep analysis
  - compare_* (3): comparison utilities
  - verify_* (4): verification
  - Other: inspect, walk, calc utilities
- REMEMBER: Always check here before creating new debug scripts
- CONTRIBUTE: Move useful scripts here from other locations
```

### Example Output (ALL)

```
Context Refresh: ALL (docs last updated: 2025-01-27)

Learned:
- Developer Guide: [top topics]
- End User Guide: [top topics]
- Constitution: [key principles]
- Code Conventions: [key patterns]
- Helper Scripts: [count] scripts in [categories]
```

Keep the output brief — this is confirmation feedback, not a detailed summary.
