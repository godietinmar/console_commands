# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Spanish-language console commands reference repository containing organized command collections for different technologies, frameworks, and operating systems. The goal is to provide a quick and easy-to-use reference for developers and system administrators.

## Project Structure

```
all_console_commands/
├── os/                     # Operating Systems
│   ├── linux/              # Linux commands (basic_commands.md)
│   ├── windows/             # Windows commands (pending)
│   └── macos/               # macOS commands (pending)
├── programming_languages/   # Programming Languages
│   ├── python/              # Python commands (python_commands.md)
│   ├── javascript/          # JavaScript commands (javascript_commands.md)
│   └── ...                  # Other languages
├── frameworks/             # Frameworks
│   ├── web/                # Web frameworks (pending)
│   └── backend/            # Backend frameworks (pending)
├── dev_tools/             # Development Tools
│   ├── git/               # Git commands (git_commands.md)
│   ├── docker/            # Docker commands (docker_commands.md)
│   └── ...                # Other dev tools
├── databases/            # Databases
│   ├── sql/              # SQL databases (mysql_commands.md)
│   └── nosql/            # NoSQL databases (pending)
└── web_cloud/           # Web Servers and Cloud
    ├── aws/             # AWS commands (pending)
    └── azure/           # Azure commands (pending)
```

## Key Files

- **README.md**: Main project documentation in Spanish explaining structure and contribution guidelines
- **INDEX.md**: Quick links index to all command sections with navigation structure

## Content Format

All command files follow a consistent Markdown structure:

```markdown
# [Command Name]

## Descripción
Brief description of what the command does.

## Sintaxis
```bash
command [options] [arguments]
```

## Opciones Comunes
- `-option1`: Description of option 1
- `-option2`: Description of option 2

## Ejemplos
```bash
# Example 1: Description
command -option1 value

# Example 2: Description
command -option2 value
```

## Notas
- Additional information or tips about command usage
- Special behaviors or warnings
```

## Available Command References

### Completed Sections
- **Linux Basic Commands** (`os/linux/basic_commands.md`): File navigation, text handling, system management, networking, compression
- **Git Commands** (`dev_tools/git/git_commands.md`): Complete Git workflow from basic operations to advanced features
- **Docker Commands** (`dev_tools/docker/docker_commands.md`): Container management and Docker operations
- **Python Commands** (`programming_languages/python/python_commands.md`): Python interpreter, package management, development tools, testing, profiling
- **JavaScript Commands** (`programming_languages/javascript/javascript_commands.md`): Node.js, npm, development tools, browser console API
- **MySQL Commands** (`databases/sql/mysql_commands.md`): Database operations and SQL commands

### Pending Sections
- Windows/macOS commands
- Web frameworks
- Backend frameworks  
- NoSQL databases
- Cloud services (AWS, Azure)

## Working with This Repository

### No Build System
This is a documentation-only repository with no build, test, or compilation steps required. All files are Markdown documentation.

### Content Language
All documentation is written in Spanish. When contributing or modifying content:
- Maintain Spanish language throughout
- Use consistent terminology for technical concepts
- Follow the established format for command documentation

### Adding New Commands
1. Identify the appropriate category/directory
2. Follow the standard format shown above
3. Include clear descriptions, syntax, common options, and practical examples
4. Update INDEX.md with links to new content
5. Ensure examples are tested and accurate

### File Organization
- Each technology/tool gets its own .md file within the appropriate category
- Use descriptive filenames (e.g., `git_commands.md`, `docker_commands.md`)
- Maintain the hierarchical directory structure
- Group related commands logically within each file

## Contribution Guidelines

When working with this repository:
- Maintain consistency with existing file formats
- Provide clear, practical examples for each command
- Verify command accuracy before adding
- Organize commands in the appropriate category
- Update navigation files (INDEX.md) when adding new sections