---
description: Install curser modules from the central repository
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Curser Module Installation System

Install modules from the curser repository (https://github.com/4jeffclark/curser.git) to your global Cursor configuration.

## Parse Arguments

**Extract the operation and modules from `$ARGUMENTS`:**

1. **List Operation**: If arguments contain "list" → show available modules
2. **Domain Operation**: If starts with "domain:" → extract domain name, resolve to module list
3. **Update Operation**: If starts with "update" → extract module names, mark as update mode
4. **Install Operation**: Default - extract comma-separated module names

**Examples:**
- `"list"` → operation: list
- `"domain:financial"` → operation: install, modules: ["financial-commands"]
- `"update python-commands"` → operation: update, modules: ["python-commands"]
- `"financial-commands, python-rules"` → operation: install, modules: ["financial-commands", "python-rules"]

## Handle List Operation

If operation is "list":
1. Clone curser repo to temp directory: `git clone https://github.com/4jeffclark/curser.git /tmp/curser-install`
2. Read `modules.json` file
3. Parse and display available modules with descriptions
4. Clean up temp directory
5. Exit

## Resolve Domain References

If operation involves domains:
1. Read `modules.json` from curser repo
2. Look up domain in `domains` section
3. Replace domain reference with actual module list
4. Continue with module list

## Validate Modules

For each requested module:
1. Check if module exists in `modules.json`
2. If not found → error: "Module 'xyz' not found. Use `/curser.install list` to see available modules"
3. Collect valid modules for installation

## Clone Repository

**Create temp directory and clone:**
```bash
TEMP_DIR="/tmp/curser-install-$RANDOM"
git clone https://github.com/4jeffclark/curser.git "$TEMP_DIR"
cd "$TEMP_DIR"
```

**Error Handling:**
- If clone fails → "Unable to access curser repository. Check internet connection"
- If temp directory creation fails → "Unable to create temporary directory"

## Read Module Configuration

**Parse modules.json:**
```json
{
  "modules": {
    "financial-commands": {
      "commands": ["portfolio-analysis.md", "risk-assessment.md"],
      "rules": ["financial-modeling.mdc"]
    }
  }
}
```

For each requested module, collect:
- Command files: `modules/{module}/commands/*.md`
- Rule files: `modules/{module}/rules/*.mdc`

## Create Global Directories

**Ensure global directories exist:**
```bash
mkdir -p ~/.cursor/commands
mkdir -p ~/.cursor/rules
```

**Error Handling:**
- If directory creation fails → "Unable to create global cursor directories. Check permissions"

## Install Files

**For each module:**
1. **Commands:** Copy from `$TEMP_DIR/modules/{module}/commands/*.md` to `~/.cursor/commands/`
2. **Rules:** Copy from `$TEMP_DIR/modules/{module}/rules/*.mdc` to `~/.cursor/rules/`

**Update Mode Handling:**
- If operation is "update", overwrite existing files
- If operation is "install" and file exists → "Module already installed. Use 'update' to refresh"

**Error Handling:**
- File copy failures → "Failed to install module files. Check permissions"
- Partial failures → report which modules succeeded/failed

## Cleanup

**Remove temporary directory:**
```bash
rm -rf "$TEMP_DIR"
```

## Confirmation

**Report results:**
- List successfully installed modules
- Show installed commands that will appear in `/` menu
- Note: "Restart Cursor if commands don't appear immediately"

**Example Output:**
```
✅ Successfully installed: financial-commands, python-rules

📋 Installed Commands:
- portfolio-analysis (financial-commands)
- risk-assessment (financial-commands)
- pytest-setup (python-commands)

🔄 New commands will appear in Cursor's / menu after restart.
```

## Error Recovery

**Network Issues:**
- Retry clone operation up to 3 times
- Suggest checking internet connection

**Permission Issues:**
- Check if ~/.cursor directories are writable
- Suggest running with appropriate permissions

**Repository Issues:**
- Verify curser repo URL is accessible
- Check if modules.json exists and is valid JSON

## Implementation Status

**✅ Completed:**
- Argument parsing logic
- Module validation
- Repository cloning
- File installation
- Error handling framework

**🔄 In Progress:**
- Domain resolution
- Update operation logic
- Comprehensive error recovery

**📋 TODO:**
- Test with actual modules
- Add version checking
- Implement rollback on partial failures
