# Cursor Rules Boilerplate Generator

A comprehensive, AI-powered system for generating and managing Cursor rules with project awareness, self-improvement, and phased initialization.

## Quick Start

1. **Bootstrap the system:**
   ```
   /bootstrap
   ```

2. **Restart Cursor** to load new rules

3. **Generate category rules:**
   ```
   /generate-category-rules
   ```

## Overview

This boilerplate system provides:

- **AI-Powered Commands**: Use Cursor commands instead of scripts
- **Project Awareness**: Rules adapt to your project structure and tech stack
- **Phased Initialization**: Establish context before generating category rules
- **Self-Improvement**: Built-in system for continuous rule improvement
- **Template-Based**: Reusable templates for consistent rule generation
- **MCP Integration**: Support for Model Context Protocol tools

## Structure

```
.cursor/
├── rules/              # Generated Cursor rules
│   ├── meta/           # Meta rules (rule system itself)
│   ├── general/        # Cross-cutting rules
│   ├── backend/        # Backend-specific rules
│   ├── frontend/       # Frontend-specific rules
│   └── workflow/       # Workflow/process rules
├── commands/           # Cursor command files
│   ├── bootstrap.md              # Phase 1: Initialize system
│   ├── generate-category-rules.md # Phase 2: Generate category rules
│   ├── generate-rule.md          # Generate single rule
│   ├── generate-command.md       # Generate new command
│   ├── generate-feature.md       # Generate feature with rules
│   ├── generate-debug-rule.md    # Generate debugging rules
│   ├── generate-worktree.md     # Generate worktree configuration
│   ├── discover-mcp-servers.md   # Discover MCP servers
│   └── generate-mcp-config.md    # Generate MCP configuration
├── templates/          # Templates for rule/command generation
│   ├── rules/          # Rule templates (.mdc.template)
│   │   ├── type-safety.mdc.template
│   │   ├── format-validation.mdc.template
│   │   ├── accessibility.mdc.template
│   │   ├── path-pattern.mdc.template
│   │   ├── keyword-detection.mdc.template
│   │   ├── file-structure.mdc.template
│   │   └── workflow-format.mdc.template
│   ├── commands/       # Command templates
│   │   ├── command-template.md
│   │   └── feature-command-template.md
│   ├── debugging/      # Debugging helper templates
│   │   ├── mcp-debug-helper.mdc.template
│   │   ├── project-aware-debug.mdc.template
│   │   ├── safe-debug-practices.mdc.template
│   │   └── error-pattern-detection.mdc.template
│   ├── worktrees/      # Worktree configuration templates
│   └── mcp/            # MCP configuration templates
├── worktrees.json      # Worktree configuration (auto-generated)
├── mcp.json            # MCP configuration (auto-generated)
├── README.md           # Quick-start guide
├── WORKTREES.md         # Worktree documentation
├── MCP.md              # MCP documentation
└── MCP_REGISTRY.md     # MCP server registry

Documentation:
├── .cursor/BOILERPLATE.md      # Complete documentation
└── .cursor/DOCUMENTATION.md    # System documentation
```

## Documentation

- **[.cursor/README.md](.cursor/README.md)** - Quick-start guide for the boilerplate system
- **[.cursor/BOILERPLATE.md](.cursor/BOILERPLATE.md)** - Complete documentation with all details
- **[.cursor/DOCUMENTATION.md](.cursor/DOCUMENTATION.md)** - System documentation
- **[.cursor/WORKTREES.md](.cursor/WORKTREES.md)** - Worktree (parallel agents) documentation
- **[.cursor/MCP.md](.cursor/MCP.md)** - MCP (Model Context Protocol) documentation
- **[.cursor/MCP_REGISTRY.md](.cursor/MCP_REGISTRY.md)** - MCP server registry

## Usage

### Initial Setup (One-Time)

1. **Bootstrap:**
   ```
   /bootstrap
   ```
   Detects project structure and generates foundational rules.

2. **Restart Cursor** to load new rules

3. **Generate category rules:**
   ```
   /generate-category-rules
   ```
   Generates backend, frontend, and workflow rules with full project context.

### Daily Usage

### Generating Rules

Use the Cursor command to create new cursor rules from templates:

In Cursor chat, type: `/generate-rule`

Or mention: "generate a cursor rule" or "create a rule"

The AI will:
1. Ask you to select a template from available options
2. Prompt for rule details (name, category, type, etc.)
3. Collect template-specific information
4. Load the template from `.cursor/templates/rules/`
5. Replace placeholders with your input
6. Validate the generated rule
7. Write the rule to the appropriate category folder

**Available Templates:**
- `type-safety` - Type checking rules (TypeScript, API types)
- `format-validation` - Regex-based format validation
- `accessibility` - HTML/JSX attribute checks
- `path-pattern` - File path matching rules
- `keyword-detection` - Keyword-based guidance rules
- `file-structure` - File organization rules
- `workflow-format` - User story, acceptance criteria templates

**Categories:**
- `backend/` - API, server, database rules
- `frontend/` - Components, UI, styling rules
- `general/` - Cross-cutting concerns
- `workflow/` - Process rules
- `meta/` - Rules about the rule system

### Generating Commands

Create new Cursor command files:

In Cursor chat, type: `/generate-command`

The AI will:
1. Ask if it's a feature command or regular command
2. Collect command details
3. Load the appropriate template from `.cursor/templates/commands/`
4. Replace placeholders with your input
5. Generate the command file in `.cursor/commands/`

### Generating Features

Scaffold features with automatic rule generation:

In Cursor chat, type: `/generate-feature`

The AI will:
1. Detect project structure (framework, language, build tool)
2. Prompt for feature details (name, type, path)
3. Generate appropriate cursor rules based on:
   - Project type (Next.js, React, Express, etc.)
   - Feature type (API endpoint, component, etc.)
   - Language (TypeScript/JavaScript)
4. Load templates from `.cursor/templates/rules/`
5. Create multiple rules (type-safety, path-pattern, accessibility if frontend)
6. Write all rules to appropriate category folders

### Generating Debugging Rules

Create debugging helper rules with MCP integration:

In Cursor chat, type: `/generate-debug-rule`

The AI will:
1. Ask for debugging rule type (mcp-integration, project-aware, safe-practices, error-patterns)
2. Detect project structure
3. Load template from `.cursor/templates/debugging/`
4. Replace placeholders with project-specific information
5. Generate the rule in `.cursor/rules/general/`

## Template System

### Rule Templates

Templates use placeholder syntax: `{{PLACEHOLDER_NAME}}`

**Common Placeholders:**
- `{{RULE_NAME}}` - Name of the rule
- `{{DESCRIPTION}}` - Rule description
- `{{CATEGORY}}` - Category folder
- `{{RULE_TYPE}}` - always, manual, guideline, autoAttached
- `{{ALWAYS_APPLY}}` - true or false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition for rule activation

**Conditional Blocks:**
```handlebars
{{#if CONDITION}}
  content here
{{/if}}
```

**Loops:**
```handlebars
{{#each ARRAY}}
  {{this}}
{{/each}}
```

### Creating Custom Templates

1. Create a new `.mdc.template` file in `.cursor/templates/rules/`
2. Use placeholder syntax for variables
3. Follow the structure of existing templates
4. The Cursor commands will automatically detect and use new templates
5. Update `.cursor/commands/generate-rule.md` if you want to document the new template

## Debugging Helpers

### MCP Integration

The debugging templates support MCP (Model Context Protocol) tool integration:

- **mcp-debug-helper.mdc.template**: MCP tool references and safe debugging practices
- **project-aware-debug.mdc.template**: Project structure detection for debugging
- **safe-debug-practices.mdc.template**: Safety guidelines and checklists
- **error-pattern-detection.mdc.template**: Common error pattern detection

All templates are located in `.cursor/templates/debugging/`

### Using Debugging Templates

1. Use `/generate-debug-rule` command in Cursor chat
2. Select a debugging template type
3. The AI will detect your project structure
4. Configure MCP tools (if applicable) - the AI will prompt for this
5. The generated rule will be customized for your project type

## Project Awareness

The Cursor commands automatically detect project structure by:

- Reading `package.json` to identify framework (Next.js, React, Express, etc.)
- Checking for `tsconfig.json` to detect TypeScript
- Analyzing build configuration files (next.config.js, vite.config.js, etc.)
- Identifying language (TypeScript/JavaScript)
- Determining build tool (Webpack, Vite, Next.js, etc.)

This information is used to:
- Generate appropriate rule types
- Suggest correct file patterns
- Apply framework-specific best practices
- Customize debugging rules for your project

## Validation

All generated rules are validated against:

- YAML frontmatter presence
- Required fields (description, type, when condition)
- Rule type validity
- Category folder correctness

Rules must pass validation before being written to disk.

## Best Practices

1. **Use Templates**: Don't create rules from scratch - use templates
2. **Be Specific**: Use specific glob patterns instead of `/**`
3. **Add Descriptions**: Always include meaningful descriptions
4. **Test Rules**: Validate rules work as expected after generation
5. **Document**: Add comments for complex conditions

## Troubleshooting

### Template Not Found
- Ensure template file exists in `.cursor/templates/rules/` (or appropriate subdirectory)
- Check filename matches exactly (case-sensitive)

### Validation Errors
- Review error messages
- Check required fields are filled
- Ensure rule type is valid

### Project Detection Issues
- Verify `package.json` exists
- Check for TypeScript configuration files
- Review project structure

## Contributing

To add new templates:

1. Create template file in appropriate directory (`.cursor/templates/rules/`, `.cursor/templates/debugging/`, `.cursor/templates/mcp/`, etc.)
2. Use standard placeholder syntax (`{{PLACEHOLDER_NAME}}`)
3. Add template to documentation in the appropriate command file
4. Test by using the Cursor command with the new template

## Cursor Commands Reference

All generators are implemented as Cursor commands (see https://cursor.com/docs):

- `/generate-rule` - Generate cursor rules from templates
- `/generate-command` - Generate new Cursor command files
- `/generate-feature` - Generate features with automatic rule creation
- `/generate-debug-rule` - Generate debugging rules with MCP integration

Commands are located in `.cursor/commands/` and provide instructions to the AI agent.

## Documentation Files

- **[.cursor/README.md](.cursor/README.md)** - Quick-start guide
  - System overview
  - Available commands
  - Quick reference

- **[.cursor/BOILERPLATE.md](.cursor/BOILERPLATE.md)** - Complete system documentation
  - Overview and quick start
  - System architecture
  - Commands reference
  - Templates reference
  - Project context system
  - Self-improvement system
  - Best practices
  - Troubleshooting

- **[.cursor/DOCUMENTATION.md](.cursor/DOCUMENTATION.md)** - System documentation
  - Detailed system information
  - Architecture details
  - Implementation guides

- **[.cursor/WORKTREES.md](.cursor/WORKTREES.md)** - Worktree documentation
  - Parallel agent support
  - Configuration guide
  - Best practices

- **[.cursor/MCP.md](.cursor/MCP.md)** - MCP documentation
  - Model Context Protocol guide
  - Server setup instructions
  - Web development workflows

- **[.cursor/MCP_REGISTRY.md](.cursor/MCP_REGISTRY.md)** - MCP server registry
  - Available MCP servers
  - Configuration examples
  - Server discovery

## See Also

- `.cursor/rules/meta/rule-generator.mdc` - Rule validation rules
- `.cursor/rules/meta/rule-generation-guide.mdc` - Rule generation guide
- `.cursor/rules/meta/rule-improvement.mdc` - Self-improvement system
- `.cursor/commands/` - All Cursor command files
- `.cursor/templates/` - All template files (rules, commands, debugging, worktrees, mcp)
- [Cursor Documentation](https://cursor.com/docs) - Official Cursor documentation for commands, MCP, and more

