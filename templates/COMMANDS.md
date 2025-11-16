# Commands Reference

Complete reference for all Cursor commands in the boilerplate system.

## Command Overview

| Command | Phase | Purpose | Prerequisites |
|---------|-------|---------|---------------|
| `/bootstrap` | 1 | Initialize system | None |
| `/generate-category-rules` | 2 | Generate category rules | Bootstrap + Restart |
| `/generate-rule` | - | Generate single rule | Context for categories |
| `/generate-feature` | - | Generate feature with rules | Context required |
| `/generate-debug-rule` | - | Generate debugging rule | Context recommended |
| `/generate-command` | - | Generate new command | None |

## `/bootstrap`

**Phase**: 1 (Initialization)

**Purpose**: Initialize the boilerplate system and establish project context

**When to use**: 
- First time setup
- Resetting the system
- Updating project context

**What it does**:
1. Detects project structure (reads package.json, tsconfig.json, config files)
2. Generates meta rules (rule-generator, rule-generation-guide, rule-improvement)
3. Generates project context rules (project-structure, tech-stack, global-patterns)
4. Generates all command files
5. Outputs restart instruction

**Output files**:
- `.cursor/rules/meta/rule-generator.mdc`
- `.cursor/rules/meta/rule-generation-guide.mdc`
- `.cursor/rules/meta/rule-improvement.mdc`
- `.cursor/rules/general/project-structure.mdc`
- `.cursor/rules/general/tech-stack.mdc`
- `.cursor/rules/general/global-patterns.mdc`
- `.cursor/commands/*.md` (all command files)

**After running**: 
- **MUST restart Cursor** to load new rules
- Then run `/generate-category-rules`

**Example**:
```
User: /bootstrap

AI: Detecting project structure...
     Reading package.json...
     Detected: Next.js, TypeScript, Next.js build tool
     Generating meta rules...
     Generating project context rules...
     ✅ Bootstrap complete! Please restart Cursor, then run /generate-category-rules
```

## `/generate-category-rules`

**Phase**: 2 (Category Generation)

**Purpose**: Generate backend, frontend, and workflow rules with full project context

**Prerequisites**:
- Must run `/bootstrap` first
- Must restart Cursor after bootstrap
- Project context must exist

**When to use**:
- After bootstrap and restart
- When you want all category rules generated at once

**What it does**:
1. Verifies project context exists
2. Reads project context rules
3. Generates backend rules (using detected backend tech)
4. Generates frontend rules (using detected frontend framework)
5. Generates workflow rules (using project patterns)

**Output files**:
- `.cursor/rules/backend/*.mdc` (backend rules)
- `.cursor/rules/frontend/*.mdc` (frontend rules)
- `.cursor/rules/workflow/*.mdc` (workflow rules)

**Example**:
```
User: /generate-category-rules

AI: Verifying project context...
     ✓ project-structure.mdc found
     ✓ tech-stack.mdc found
     Reading project context: Next.js, TypeScript
     Generating backend rules...
     - api-type-safety.mdc
     - no-any.mdc
     Generating frontend rules...
     - alt-text.mdc
     - component-patterns.mdc
     Generating workflow rules...
     - user-story-format.mdc
     ✅ Category rules generated!
```

## `/generate-rule`

**Phase**: Any (after bootstrap)

**Purpose**: Generate a single cursor rule from templates

**Prerequisites**:
- For `backend/`, `frontend/`, or `workflow/` categories: Project context required
- For `general/` or `meta/` categories: No prerequisites

**When to use**:
- Creating a specific rule
- Adding a custom rule
- Extending existing rules

**Flow**:
1. AI checks if category requires project context
2. AI asks for rule details
3. AI loads template
4. AI replaces placeholders
5. AI validates rule
6. AI writes rule file

**Available templates**:
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

**Example**:
```
User: /generate-rule Require error handling in API routes

AI: Which template? (type-safety/path-pattern)
User: type-safety
AI: Which category? (backend/frontend/general/workflow/meta)
User: backend
AI: Rule type? (always/manual/guideline/autoAttached)
User: always
AI: [Generates rule with project context]
     ✅ Rule generated: .cursor/rules/backend/api-error-handling.mdc
```

## `/generate-feature`

**Phase**: Any (after bootstrap)

**Purpose**: Generate a feature with automatic rule generation

**Prerequisites**: 
- Project context **required** (from `/bootstrap`)

**When to use**:
- Creating a new feature
- Need feature-specific rules
- Want automatic rule generation

**Flow**:
1. AI checks for project context
2. AI reads project context
3. AI asks for feature details
4. AI generates multiple rules for the feature
5. AI uses project context to customize rules

**What it generates**:
- Type safety rules (if TypeScript)
- Path pattern rules
- Accessibility rules (if frontend)
- Feature-specific rules

**Example**:
```
User: /generate-feature Create user authentication API endpoint

AI: Reading project context (Next.js, TypeScript)...
     Feature name: user-authentication
     Feature type: API Endpoint
     Generating rules:
     - user-authentication-type-safety.mdc (backend)
     - user-authentication-path-pattern.mdc (backend)
     ✅ Feature rules generated!
```

## `/generate-debug-rule`

**Phase**: Any (after bootstrap recommended)

**Purpose**: Generate debugging helper rules with MCP integration

**Prerequisites**: 
- Project context **recommended** (optional for basic rules)

**When to use**:
- Need debugging guidelines
- Want MCP integration
- Need error pattern detection

**Available templates**:
- `mcp-debug-helper` - MCP tool integration
- `project-aware-debug` - Project structure detection
- `safe-debug-practices` - Safety guidelines
- `error-pattern-detection` - Error pattern detection

**Flow**:
1. AI checks for project context (optional)
2. AI asks for debugging rule type
3. AI loads template
4. AI uses project context if available
5. AI generates rule

**Example**:
```
User: /generate-debug-rule Create safe debugging rule

AI: What type? (mcp-integration/project-aware/safe-practices/error-patterns)
User: safe-practices
AI: Using project context (Next.js, TypeScript)...
     Generating rule...
     ✅ Rule generated: .cursor/rules/general/safe-debug-practices.mdc
```

## `/generate-command`

**Phase**: Any

**Purpose**: Generate a new Cursor command file

**Prerequisites**: None

**When to use**:
- Creating custom commands
- Extending command system
- Adding project-specific commands

**Flow**:
1. AI asks for command details
2. AI asks if it's a feature command
3. AI loads appropriate template
4. AI generates command file

**Templates**:
- `command-template.md` - Regular command
- `feature-command-template.md` - Feature command

**Example**:
```
User: /generate-command Create command to scaffold database migrations

AI: Is this a feature command? (y/n)
User: y
AI: Feature type: Database Migration
     [Generates command file]
     ✅ Command generated: .cursor/commands/generate-migration.md
```

## Command Dependencies

```
bootstrap
  ↓
[Restart Cursor]
  ↓
generate-category-rules
  ↓
[Rules active]

generate-rule (for categories)
  ↓
[Requires project context]

generate-feature
  ↓
[Requires project context]

generate-debug-rule
  ↓
[Recommends project context]

generate-command
  ↓
[No dependencies]
```

## Command Best Practices

1. **Follow the phases**: Bootstrap → Restart → Category Rules
2. **Check prerequisites**: Verify project context before category generation
3. **Use appropriate templates**: Match template to rule purpose
4. **Validate output**: Check generated rules against validation requirements
5. **Restart when needed**: Restart Cursor after bootstrap and major changes

## Error Messages

**"Project context not found"**
- **Cause**: Project context rules don't exist
- **Solution**: Run `/bootstrap` first, then restart Cursor

**"Template not found"**
- **Cause**: Template name doesn't match
- **Solution**: Check template name (case-sensitive), list available templates

**"Validation failed"**
- **Cause**: Rule doesn't meet requirements
- **Solution**: Review validation errors, fix missing fields

**"Category rules not generated"**
- **Cause**: Project context missing or Cursor not restarted
- **Solution**: Run `/bootstrap`, restart Cursor, then try again

---

For detailed usage examples, see [USAGE.md](USAGE.md)
For system architecture, see [ARCHITECTURE.md](ARCHITECTURE.md)

