# Curser System - Development Handover

## Project Objective

Create a modular, agentic system for managing Cursor AI commands and rules across multiple projects without conflicts. The system should allow developers to install custom command modules on-demand from a central repository, making them available globally without interfering with project-specific Cursor configurations.

## Problem Statement

The user has a mixture of custom commands (like `myspeckit.*`) and shared commands (like `speckit.*`) in their project `.cursor/` folder. They want to:

1. Keep shared/speckit commands version-controlled in projects
2. Manage personal/custom commands centrally across workstations
3. Install command modules on-demand without manual file management
4. Avoid conflicts between personal and team configurations

## Solution Architecture

### Core Components

1. **Bootstrap Command**: `curser.install.md` - Manual installation entry point (copy to project `.cursor/commands/`)
2. **Module Registry**: `modules.json` - Defines available modules and their contents
3. **Modular Repository**: `modules/` directory with categorized command/rule packages
4. **Global Installation**: Commands install to `~/.cursor/commands/` and `~/.cursor/rules/`

### User Journey

1. **Bootstrap**: User copies `curser.install.md` from this repo to project `.cursor/commands/`
2. **Installation**: User runs `/curser.install financial-commands` in Cursor
3. **Automatic Process**: Command clones repo, validates modules, copies files globally
4. **Availability**: New commands appear in Cursor's `/` menu across all projects

## Implementation Status

### Completed

1. **Command Structure**: `curser.install.md` with argument parsing, list/domain/update/install logic
2. **Repository Structure**: Modular organization with `modules.json` registry
3. **Sample Content**: Financial commands module (portfolio-analysis.md, financial-modeling.mdc)
4. **Error Handling Framework**: Error cases and recovery guidance in command
5. **Documentation**: README.md and HANDOVER.md

### Partially Implemented

1. **Domain Resolution**: Logic in command; needs testing with domain mappings
2. **Update Operations**: Framework in command; overwrite behavior needs validation
3. **File Installation**: Described in command; agent performs clone/copy; cross-platform testing needed

### Remaining Work

#### High Priority
1. Cross-platform testing (Windows, macOS, Linux)
2. Retry logic for network failures
3. Version checking for module updates
4. Rollback on partial installation failures

#### Medium Priority
1. Private repository authentication if needed
2. File conflict handling during install/update
3. Module dependencies
4. Caching of repo clone to speed installs

#### Low Priority
1. Cursor extension for browsing modules
2. Usage analytics
3. Automated tests for installed commands

## Technical Details

### Command Arguments
- `list` - Show available modules
- `domain:name` - Install all modules for a domain
- `module1, module2` - Install specific modules
- `update module` - Update existing module

### File Structure
```
curser/
├── modules.json
├── curser.install.md
├── README.md
├── HANDOVER.md
└── modules/
    └── financial-commands/
        ├── commands/     # .md files
        └── rules/        # .mdc files
```

### Dependencies
- Git (for cloning)
- Cursor agent (runs the command and performs clone/copy)

## Next Steps for Development

1. **Immediate**: Test install flow with `/curser.install list` and `/curser.install financial-commands`
2. **Short-term**: Implement high-priority items (retries, version check, rollback)
3. **Medium-term**: Caching, dependencies, conflict handling
4. **Long-term**: Extension, analytics

## Handover Notes

### Current State
Bootstrap command and repo structure are in place. Installation is performed by the Cursor agent following the command instructions; no standalone script. Needs real-world and cross-platform testing.

### Key Files
- `curser.install.md` - Installer command (agent runs it)
- `modules.json` - Module registry; expand for new modules
- `modules/financial-commands/` - Example module to copy for new modules

### Risks
- **Low**: Architecture is modular and clear
- **Medium**: OS-specific paths and shell commands (e.g. temp dirs, ~/.cursor) need verification on Windows/macOS/Linux
