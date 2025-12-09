# Cursor Rules Boilerplate - Complete Documentation

A comprehensive, AI-powered system for generating and managing Cursor rules with project awareness, self-improvement, and phased initialization.

## Table of Contents

1. [Overview](#overview)
2. [Quick Start](#quick-start)
3. [System Architecture](#system-architecture)
4. [Commands Reference](#commands-reference)
5. [Templates Reference](#templates-reference)
6. [Project Context System](#project-context-system)
7. [Self-Improvement System](#self-improvement-system)
8. [Best Practices](#best-practices)
9. [Troubleshooting](#troubleshooting)

## Overview

This boilerplate provides a complete system for:

- **AI-Powered Rule Generation**: Use Cursor commands instead of scripts
- **Project Awareness**: Rules adapt to your project structure and tech stack
- **Phased Initialization**: Establish context before generating category rules
- **Self-Improvement**: Built-in system for continuous rule improvement
- **Template-Based**: Reusable templates for consistent rule generation
- **MCP Integration**: Support for Model Context Protocol tools

## Quick Start

### Initial Setup

1. **Bootstrap the system:**
   ```
   /bootstrap
   ```
   This will:
   - Detect your project structure
   - Generate foundational rules
   - Create project context
   - Generate all command files

2. **Restart Cursor:**
   - Close and reopen Cursor to load the new rules

3. **Generate category rules:**
   ```
   /generate-category-rules
   ```
   This generates backend, frontend, and workflow rules with full project context.

### Daily Usage

- **Generate a new rule:**
  ```
  /generate-rule
  ```

- **Generate a feature with rules:**
  ```
  /generate-feature
  ```

- **Generate a debugging rule:**
  ```
  /generate-debug-rule
  ```

- **Generate a new command:**
  ```
  /generate-command
  ```

## System Architecture

### Two-Phase Initialization

#### Phase 1: Bootstrap (`/bootstrap`)

**Purpose**: Establish project context and foundational rules

**What it does:**
1. Detects project structure (reads package.json, tsconfig.json, config files)
2. Generates meta rules (rule-generator, rule-generation-guide, rule-improvement)
3. Generates project context rules (project-structure, tech-stack, global-patterns)
4. Generates all command files
5. Outputs restart instruction

**Output:**
- `.cursor/rules/meta/` - Meta rules for rule system
- `.cursor/rules/general/project-structure.mdc` - Project structure detection
- `.cursor/rules/general/tech-stack.mdc` - Tech stack identification
- `.cursor/rules/general/global-patterns.mdc` - Global patterns
- `.cursor/commands/` - All command files

**After Phase 1**: User must restart Cursor to load new rules

#### Phase 2: Category Generation (`/generate-category-rules`)

**Purpose**: Generate category-specific rules with full project awareness

**Prerequisites:**
- Project context must exist (from Phase 1)
- Cursor must be restarted after Phase 1

**What it does:**
1. Verifies project context exists
2. Reads project context rules
3. Generates backend rules (using detected backend tech)
4. Generates frontend rules (using detected frontend framework)
5. Generates workflow rules (using project patterns)

**Output:**
- `.cursor/rules/backend/` - Backend-specific rules
- `.cursor/rules/frontend/` - Frontend-specific rules
- `.cursor/rules/workflow/` - Workflow rules

### Project Context Flow

```
Bootstrap → Project Detection → Context Rules → Restart → Category Rules
```

1. **Bootstrap** detects project structure
2. **Context Rules** are generated with detected info
3. **Restart** loads context into Cursor
4. **Category Rules** use context for intelligent generation

## Commands Reference

### `/bootstrap`

**Purpose**: Initialize the boilerplate system (Phase 1)

**When to use**: First time setup, or when resetting the system

**What it generates:**
- Meta rules (rule-generator, rule-generation-guide, rule-improvement)
- Project context rules (project-structure, tech-stack, global-patterns)
- All command files

**After running**: Restart Cursor, then run `/generate-category-rules`

**Example:**
```
User: /bootstrap

AI: Detecting project structure...
     - Framework: Next.js
     - Language: TypeScript
     - Build Tool: Next.js
     Generating foundational rules...
     ✅ Bootstrap complete! Please restart Cursor, then run /generate-category-rules
```

### `/generate-category-rules`

**Purpose**: Generate backend, frontend, and workflow rules (Phase 2)

**Prerequisites**: 
- Must run `/bootstrap` first
- Must restart Cursor after bootstrap

**What it generates:**
- Backend rules (API, database, server patterns)
- Frontend rules (components, UI, styling)
- Workflow rules (user stories, planning, tasks)

**Uses**: Project context from Phase 1

**Example:**
```
User: /generate-category-rules

AI: Verifying project context...
     Reading project structure...
     Generating backend rules for Next.js API routes...
     Generating frontend rules for React components...
     ✅ Category rules generated!
```

### `/generate-rule`

**Purpose**: Generate a single cursor rule from templates

**Project Context Check:**
- If generating `backend/`, `frontend/`, or `workflow/` rules:
  - Requires project context (from `/bootstrap`)
  - Uses project context to customize rules

**Available Templates:**
- `type-safety` - Type checking rules
- `format-validation` - Format validation
- `accessibility` - HTML/JSX attribute checks
- `path-pattern` - File path matching
- `keyword-detection` - Keyword-based guidance
- `file-structure` - File organization
- `workflow-format` - User story, acceptance criteria
- `rule-improvement` - Rule improvement rules
- `project-structure` - Project structure detection
- `tech-stack` - Tech stack identification

**Example:**
```
User: /generate-rule Create a rule that requires error handling in API routes

AI: Which template? (type-safety/path-pattern)
    Which category? (backend)
    Rule type? (always)
    [Generates rule with project context]
```

### `/generate-feature`

**Purpose**: Generate a feature with automatic rule generation

**Prerequisites**: Project context must exist (from `/bootstrap`)

**What it does:**
1. Reads project context
2. Asks for feature details
3. Generates appropriate rules based on:
   - Feature type (API, component, utility)
   - Project framework
   - Project language
   - Project structure

**Example:**
```
User: /generate-feature Create a user authentication API endpoint

AI: Reading project context (Next.js, TypeScript)...
     Feature name: user-authentication
     Generating rules:
     - user-authentication-type-safety.mdc
     - user-authentication-path-pattern.mdc
```

### `/generate-debug-rule`

**Purpose**: Generate debugging helper rules with MCP integration

**Project Context**: Recommended (optional for basic rules)

**Available Templates:**
- `mcp-debug-helper` - MCP tool integration
- `project-aware-debug` - Project structure detection
- `safe-debug-practices` - Safety guidelines
- `error-pattern-detection` - Error pattern detection

**Example:**
```
User: /generate-debug-rule Create a rule for safe debugging with MCP tools

AI: Using project context (Next.js, TypeScript)...
     Generating mcp-debug-helper rule...
```

### `/generate-command`

**Purpose**: Generate a new Cursor command file

**Templates:**
- `command-template.md` - Regular command
- `feature-command-template.md` - Feature command

**Example:**
```
User: /generate-command Create a command to scaffold database migrations

AI: Is this a feature command? (y/n)
    [Generates command file]
```

## Templates Reference

### Rule Templates (`templates/rules/`)

#### `type-safety.mdc.template`
**Use for**: Type checking rules (TypeScript, API types)
**Placeholders**: `RULE_NAME`, `DESCRIPTION`, `MUST_CONTAIN`, `MUST_NOT_CONTAIN`, `ERROR_MESSAGE`
**Example**: Enforce no `any` types, require proper API handler types

#### `format-validation.mdc.template`
**Use for**: Regex-based format validation
**Placeholders**: `RULE_NAME`, `PATTERN`, `NEXT_BLOCK_PATTERN`, `ERROR_MESSAGE`
**Example**: Validate user story format, acceptance criteria format

#### `accessibility.mdc.template`
**Use for**: HTML/JSX attribute checks
**Placeholders**: `RULE_NAME`, `ELEMENT_PATTERN`, `REQUIRED_ATTRIBUTE`, `ERROR_MESSAGE`
**Example**: Require alt text on images, ARIA labels

#### `path-pattern.mdc.template`
**Use for**: File path matching rules
**Placeholders**: `RULE_NAME`, `WHEN_CONDITION`, `MESSAGE`, `ERROR_MESSAGE`
**Example**: Enforce component structure, API route patterns

#### `keyword-detection.mdc.template`
**Use for**: Keyword-based guidance rules
**Placeholders**: `RULE_NAME`, `KEYWORD_1`, `KEYWORD_2`, `MESSAGE`
**Example**: Logging best practices, memory management guidance

#### `file-structure.mdc.template`
**Use for**: File organization rules
**Placeholders**: `RULE_NAME`, `CONDITION`, `ERROR_MESSAGE`
**Example**: Require memory files, validate mode folder structure

#### `workflow-format.mdc.template`
**Use for**: User story, acceptance criteria templates
**Placeholders**: `RULE_NAME`, `PATTERN`, `NEXT_BLOCK_PATTERN`, `CHECKLIST`
**Example**: User story format, acceptance criteria format, effort estimation

#### `rule-improvement.mdc.template`
**Use for**: Rule improvement and monitoring rules
**Placeholders**: `RULE_NAME`, `PATTERN`, `MESSAGE`, `CHECKLIST`
**Example**: Rule improvement triggers, pattern recognition

#### `project-structure.mdc.template`
**Use for**: Project structure detection and documentation
**Placeholders**: `RULE_NAME`, `WHEN_CONDITION`, `MESSAGE`
**Example**: Detect framework, build tool, folder structure

#### `tech-stack.mdc.template`
**Use for**: Tech stack identification and enforcement
**Placeholders**: `RULE_NAME`, `PATTERN`, `MUST_NOT_CONTAIN`, `MESSAGE`
**Example**: Identify languages, libraries, versions

### Debugging Templates (`templates/debugging/`)

#### `mcp-debug-helper.mdc.template`
**Use for**: MCP tool integration and references
**Placeholders**: `MCP_TOOLS`, `PROJECT_TYPE`, `FRAMEWORK`, `LANGUAGE`
**Example**: MCP debugging tools, safe file inspection

#### `project-aware-debug.mdc.template`
**Use for**: Project structure detection for debugging
**Placeholders**: `PROJECT_TYPE`, `FRAMEWORK`, `LANGUAGE`, `BUILD_TOOL`
**Example**: Context-aware error analysis, project-specific debugging

#### `safe-debug-practices.mdc.template`
**Use for**: Safety guidelines and checklists
**Placeholders**: `RULE_NAME`, `MESSAGE`, `CHECKLIST`
**Example**: Safe debugging guidelines, error handling best practices

#### `error-pattern-detection.mdc.template`
**Use for**: Common error pattern detection
**Placeholders**: `ERROR_PATTERNS`, `LIKELY_CAUSES`, `MCP_TOOLS`
**Example**: Type errors, configuration errors, common patterns

### Command Templates (`templates/commands/`)

#### `command-template.md`
**Use for**: Regular Cursor commands
**Placeholders**: `COMMAND_NAME`, `COMMAND_DESCRIPTION`, `INSTRUCTIONS`, `REFERENCE_FILES`

#### `feature-command-template.md`
**Use for**: Feature scaffolding commands
**Placeholders**: `FEATURE_TYPE`, `FEATURE_FILES`, `ADDITIONAL_PROMPTS`

## Project Context System

### What is Project Context?

Project context is established during Phase 1 (`/bootstrap`) and consists of:

1. **Project Structure** (`.cursor/rules/general/project-structure.mdc`)
   - Detected framework (Next.js, React, Express, etc.)
   - Build tool (Webpack, Vite, Next.js, etc.)
   - Folder structure patterns

2. **Tech Stack** (`.cursor/rules/general/tech-stack.mdc`)
   - Language (TypeScript/JavaScript)
   - Key libraries and dependencies
   - Versions and patterns

3. **Global Patterns** (`.cursor/rules/general/global-patterns.mdc`)
   - Common patterns across the project
   - Project-specific conventions

### How Project Context is Used

**During Rule Generation:**
- Rules reference detected framework
- File patterns match project structure
- Best practices align with tech stack
- Examples use actual project patterns

**Example:**
```
If project is Next.js + TypeScript:
- Backend rules target `pages/api/` or `app/api/`
- Frontend rules target `components/` and `pages/`
- Type safety rules enforce TypeScript patterns
- File extensions use `.ts` and `.tsx`
```

### Project Detection

The bootstrap command detects:

**From `package.json`:**
- Framework (Next.js, React, Express, Vue)
- Language (TypeScript from dependencies)
- Build tool (Webpack, Vite)
- Key dependencies

**From Config Files:**
- `tsconfig.json` → TypeScript
- `next.config.js` → Next.js
- `vite.config.js` → Vite
- Other framework configs

## Self-Improvement System

### Overview

The self-improvement system (`.cursor/rules/meta/rule-improvement.mdc`) provides guidelines for continuous rule improvement.

### Improvement Triggers

The system monitors for:

1. **New Code Patterns**
   - Technology/pattern used in 3+ files
   - Framework updates or migrations
   - Library adoption

2. **Repeated Implementations**
   - Same pattern in multiple files
   - Inconsistent approaches
   - Copy-paste code

3. **Common Errors**
   - Same bug appearing multiple times
   - Type errors that could be prevented
   - Runtime errors with patterns

4. **Best Practices**
   - Security improvements
   - Performance optimizations
   - Code quality improvements

5. **Documentation Gaps**
   - Patterns referenced but not enforced
   - External documentation to codify
   - Team conventions not captured

### Rule Analysis Process

1. **Compare new code with existing rules**
   - Review `.cursor/rules/` for coverage
   - Identify patterns to standardize
   - Check for consistent error handling

2. **Identify patterns to standardize**
   - Search for repeated code blocks (3+ occurrences)
   - Find similar function implementations
   - Document library usage patterns

3. **Extract examples from actual code**
   - Use real code examples
   - Note file locations and context
   - Identify edge cases

### When to Add/Modify/Deprecate Rules

**Add New Rules When:**
- New technology/pattern in 3+ files
- Common bugs could be prevented
- Code reviews mention same feedback
- New security/performance patterns emerge

**Modify Existing Rules When:**
- Better examples exist
- Additional edge cases discovered
- Related rules updated
- Implementation details changed

**Deprecate Rules When:**
- Pattern no longer used
- Better approach exists
- Technology replaced
- Rule causes more problems than it solves

## Best Practices

### Rule Generation

1. **Use Templates**: Always use templates from `templates/rules/`
2. **Be Specific**: Use specific glob patterns, not `/**`
3. **Add Descriptions**: Always include meaningful descriptions
4. **Test Rules**: Validate rules work as expected
5. **Reference Context**: Use project context when available

### Project Context

1. **Bootstrap First**: Always run `/bootstrap` before generating category rules
2. **Restart Required**: Always restart Cursor after bootstrap
3. **Keep Context Updated**: Re-run bootstrap if project structure changes significantly
4. **Use Context**: Reference project context in all category rules

### Rule Maintenance

1. **Regular Reviews**: Review rules monthly for effectiveness
2. **Update Examples**: Keep examples synchronized with code
3. **Deprecate Gracefully**: Mark deprecated rules, provide migration path
4. **Cross-Reference**: Link related rules

### Command Usage

1. **Follow Phases**: Use Phase 1 (bootstrap) then Phase 2 (category rules)
2. **Check Prerequisites**: Verify project context before category generation
3. **Use Appropriate Templates**: Select templates that match rule purpose
4. **Validate Output**: Check generated rules against validation requirements

## Troubleshooting

### Bootstrap Issues

**Problem**: Bootstrap doesn't detect project structure
- **Solution**: Ensure `package.json` exists in project root
- **Solution**: Check for config files (tsconfig.json, next.config.js)

**Problem**: Meta rules not generated
- **Solution**: Bootstrap should copy from existing or generate from content
- **Solution**: Check `.cursor/rules/meta/` directory exists

### Project Context Issues

**Problem**: "Project context not found" error
- **Solution**: Run `/bootstrap` first
- **Solution**: Restart Cursor after bootstrap
- **Solution**: Verify `.cursor/rules/general/project-structure.mdc` exists

**Problem**: Rules don't use project context
- **Solution**: Ensure project context rules are generated
- **Solution**: Check that rules reference context in messages

### Rule Generation Issues

**Problem**: Template not found
- **Solution**: Verify template exists in `templates/rules/`
- **Solution**: Check template name matches exactly (case-sensitive)

**Problem**: Validation errors
- **Solution**: Review error messages
- **Solution**: Check required fields are filled
- **Solution**: Ensure rule type is valid

**Problem**: Rules don't work after generation
- **Solution**: Restart Cursor to load new rules
- **Solution**: Verify rule follows `.cursor/rules/meta/rule-generator.mdc` requirements

### Category Generation Issues

**Problem**: Category rules not generated
- **Solution**: Verify project context exists
- **Solution**: Check that Cursor was restarted after bootstrap
- **Solution**: Ensure `/generate-category-rules` is run after restart

**Problem**: Rules don't match project structure
- **Solution**: Re-run `/bootstrap` to update project context
- **Solution**: Restart Cursor after updating context

## File Structure

```
lazy-dev/
├── .cursor/
│   ├── commands/
│   │   ├── bootstrap.md                    # Phase 1 initialization
│   │   ├── generate-category-rules.md      # Phase 2 category generation
│   │   ├── generate-rule.md               # Single rule generation
│   │   ├── generate-feature.md            # Feature with rules
│   │   ├── generate-debug-rule.md        # Debugging rules
│   │   └── generate-command.md            # New command generation
│   └── rules/
│       ├── meta/                          # Meta rules (generated by bootstrap)
│       ├── general/                        # General rules (includes project context)
│       ├── backend/                        # Backend rules (generated in Phase 2)
│       ├── frontend/                       # Frontend rules (generated in Phase 2)
│       └── workflow/                       # Workflow rules (generated in Phase 2)
├── templates/
│   ├── rules/                              # Rule templates
│   │   ├── type-safety.mdc.template
│   │   ├── format-validation.mdc.template
│   │   ├── accessibility.mdc.template
│   │   ├── path-pattern.mdc.template
│   │   ├── keyword-detection.mdc.template
│   │   ├── file-structure.mdc.template
│   │   ├── workflow-format.mdc.template
│   │   ├── rule-improvement.mdc.template
│   │   ├── project-structure.mdc.template
│   │   └── tech-stack.mdc.template
│   ├── debugging/                          # Debugging templates
│   │   ├── mcp-debug-helper.mdc.template
│   │   ├── project-aware-debug.mdc.template
│   │   ├── safe-debug-practices.mdc.template
│   │   └── error-pattern-detection.mdc.template
│   └── commands/                           # Command templates
│       ├── command-template.md
│       └── feature-command-template.md
└── BOILERPLATE.md                          # This documentation
```

## Reference Links

- [Cursor Documentation](https://cursor.com/docs) - Official Cursor documentation
- [Cursor Commands](https://cursor.com/docs) - Command system documentation
- [MCP Documentation](https://cursor.com/docs) - Model Context Protocol

## Support

For issues or questions:
1. Check this documentation
2. Review command files in `.cursor/commands/`
3. Check rule templates in `templates/rules/`
4. Verify project context is established

---

**Last Updated**: 2024
**Version**: 1.0.0

