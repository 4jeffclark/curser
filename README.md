# Curser - Modular Cursor Command System

A modular system for managing and distributing Cursor AI commands and rules across projects and workstations.

## Overview

Curser provides a centralized, version-controlled repository for Cursor commands and rules that can be installed on-demand using the `/curser.install` command. This eliminates the need for manual file management and provides a consistent way to share and update AI workflow tools.

## Architecture

```
curser/
├── modules.json          # Module registry and metadata
├── curser.install.md     # Bootstrap command (copy to project .cursor/commands/)
├── modules/              # Modular command/rule packages
│   ├── workflow-commands/
│   │   ├── commands/     # .md command files
│   │   └── rules/        # .mdc rule files
│   ├── financial-commands/
│   └── ...
└── README.md
```

## Installation

1. **Manual Bootstrap**: Copy `curser.install.md` from this repo to your project's `.cursor/commands/` directory.
2. **Use the Command**: Run `/curser.install` with module specifications to install additional components.

## Module Types

### Commands
- **workflow-commands**: Development productivity and process optimization
- **debugging-commands**: Advanced troubleshooting and error analysis
- **python-commands**: Python development workflows
- **financial-commands**: Financial modeling and analysis tools

### Rules
- **python-rules**: Python coding standards and patterns
- **financial-rules**: Financial domain constraints and best practices
- **web-rules**: Web development standards

## Usage Examples

```bash
# Install specific modules
/curser.install financial-commands, python-rules

# Install by domain
/curser.install domain:financial

# List available modules
/curser.install list

# Update existing modules
/curser.install update financial-commands
```

## Global Installation

Commands and rules are installed to Cursor's global directories:
- Commands: `~/.cursor/commands/`
- Rules: `~/.cursor/rules/`

This makes them available across all projects without conflicts.

## Contributing

1. Create a new module directory under `modules/`
2. Add command files (`.md`) and rule files (`.mdc`)
3. Update `modules.json` with module metadata
4. Submit a pull request

## Module Development Guidelines

### Commands
- Use clear, descriptive filenames with kebab-case
- Include comprehensive usage instructions
- Document input requirements and output formats
- Provide examples and error handling guidance

### Rules
- Use `.mdc` extension with proper YAML frontmatter
- Include `description` and `globs` for proper activation
- Set `alwaysApply: false` for optional rules
- Document the reasoning and benefits of each rule

## Version Control

- All modules are version-controlled in this repository
- Use semantic versioning for releases
- Maintain backward compatibility when possible
- Document breaking changes in release notes
