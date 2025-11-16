# Templates Reference

Complete reference for all templates in the boilerplate system.

## Template System Overview

Templates use placeholder syntax for variable substitution:
- `{{PLACEHOLDER_NAME}}` - Simple replacement
- `{{#if CONDITION}}...{{/if}}` - Conditional blocks
- `{{#each ARRAY}}...{{/each}}` - Loops

## Rule Templates

Location: `templates/rules/*.mdc.template`

### `type-safety.mdc.template`

**Purpose**: Type checking rules (TypeScript, API types)

**Use for**:
- Enforcing TypeScript types
- Preventing `any` types
- API handler type safety
- Type pattern validation

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - always/manual/guideline/autoAttached
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{MUST_CONTAIN}}` - Pattern that must be present
- `{{MUST_NOT_CONTAIN}}` - Pattern that must not be present
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message
- `{{INFO_MESSAGE}}` - Info message
- `{{CONDITION}}` - Optional condition

**Example usage**:
- "Avoid 'any' Type" rule
- "API Type Safety" rule
- "Strict Type Checking" rule

### `format-validation.mdc.template`

**Purpose**: Regex-based format validation

**Use for**:
- User story format validation
- Acceptance criteria format
- Code format patterns
- Document format validation

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{PATTERN}}` - Regex pattern to match
- `{{NEXT_BLOCK_PATTERN}}` - Pattern for next block
- `{{NEXT_BLOCK_MUST_CONTAIN}}` - Required content in next block
- `{{VALID_MESSAGE}}` - Success message
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "User Story Format" rule
- "Acceptance Criteria Format" rule
- "Testable Format" rule

### `accessibility.mdc.template`

**Purpose**: HTML/JSX attribute checks

**Use for**:
- Image alt text requirements
- ARIA label requirements
- Form label requirements
- Semantic HTML requirements

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{ELEMENT_PATTERN}}` - HTML element pattern (e.g., "<img ")
- `{{REQUIRED_ATTRIBUTE}}` - Required attribute (e.g., "alt=")
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "Accessibility: Alt Text" rule
- "ARIA Labels Required" rule
- "Form Labels Required" rule

### `path-pattern.mdc.template`

**Purpose**: File path matching rules

**Use for**:
- Component structure validation
- API route patterns
- File organization
- Directory structure

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{CONDITION}}` - Optional condition
- `{{MESSAGE}}` - Guidance message
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "Component Path Pattern" rule
- "API Route Pattern" rule
- "File Structure" rule

### `keyword-detection.mdc.template`

**Purpose**: Keyword-based guidance rules

**Use for**:
- Logging best practices
- Memory management
- Common pattern detection
- Code quality guidance

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{KEYWORD_1}}` - First keyword
- `{{KEYWORD_2}}` - Second keyword (optional)
- `{{KEYWORD_3}}` - Third keyword (optional)
- `{{MESSAGE}}` - Guidance message
- `{{WARNING_MESSAGE}}` - Warning message
- `{{INFO_MESSAGE}}` - Info message

**Example usage**:
- "Log Usage" rule
- "Memory Management" rule
- "Error Handling" rule

### `file-structure.mdc.template`

**Purpose**: File organization rules

**Use for**:
- Required files validation
- Folder structure validation
- File existence checks
- Directory organization

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{CONDITION}}` - Condition (e.g., file.exists("path"))
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "Memory Bank Check" rule
- "Mode Folder Structure" rule
- "Required Files" rule

### `workflow-format.mdc.template`

**Purpose**: User story, acceptance criteria templates

**Use for**:
- User story format validation
- Acceptance criteria format
- Planning document format
- Task format validation

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{PATTERN}}` - Pattern to match
- `{{NEXT_BLOCK_PATTERN}}` - Next block pattern
- `{{NEXT_BLOCK_MUST_CONTAIN}}` - Required in next block
- `{{MUST_NOT_CONTAIN}}` - Pattern to avoid
- `{{VALID_MESSAGE}}` - Success message
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message
- `{{CHECKLIST}}` - Array of checklist items
- `{{CHECKLIST_ITEMS}}` - Checklist items array

**Example usage**:
- "User Story Format" rule
- "Acceptance Criteria" rule
- "Effort Estimation" rule

### `rule-improvement.mdc.template`

**Purpose**: Rule improvement and monitoring rules

**Use for**:
- Rule improvement triggers
- Pattern recognition
- Rule quality monitoring
- Improvement guidelines

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{PATTERN}}` - Pattern to detect
- `{{MESSAGE}}` - Guidance message
- `{{CHECKLIST}}` - Checklist array
- `{{CHECKLIST_ITEMS}}` - Checklist items

**Example usage**:
- "Rule Improvement Triggers" rule
- "Pattern Recognition" rule
- "Rule Quality Checks" rule

### `project-structure.mdc.template`

**Purpose**: Project structure detection and documentation

**Use for**:
- Framework detection
- Build tool identification
- Folder structure patterns
- Project organization

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{CONDITION}}` - Optional condition
- `{{MESSAGE}}` - Guidance message
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "Project Structure Detection" rule
- "Framework Identification" rule
- "Build Tool Detection" rule

### `tech-stack.mdc.template`

**Purpose**: Tech stack identification and enforcement

**Use for**:
- Library identification
- Version enforcement
- Dependency patterns
- Tech stack documentation

**Placeholders**:
- `{{RULE_NAME}}` - Rule name
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{PATTERN}}` - Pattern to match
- `{{MUST_NOT_CONTAIN}}` - Pattern to avoid
- `{{MESSAGE}}` - Guidance message
- `{{ERROR_MESSAGE}}` - Error message
- `{{WARNING_MESSAGE}}` - Warning message

**Example usage**:
- "Tech Stack Identification" rule
- "Library Version" rule
- "Dependency Patterns" rule

## Debugging Templates

Location: `templates/debugging/*.mdc.template`

### `mcp-debug-helper.mdc.template`

**Purpose**: MCP tool integration and references

**Placeholders**:
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{MCP_TOOLS}}` - Array of MCP tools
- `{{PROJECT_TYPE}}` - Detected project type
- `{{FRAMEWORK}}` - Framework name
- `{{LANGUAGE}}` - Language (TypeScript/JavaScript)
- `{{BUILD_TOOL}}` - Build tool

### `project-aware-debug.mdc.template`

**Purpose**: Project structure detection for debugging

**Placeholders**:
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{CONDITION}}` - Condition
- `{{PROJECT_TYPE}}` - Project type
- `{{FRAMEWORK}}` - Framework
- `{{LANGUAGE}}` - Language
- `{{BUILD_TOOL}}` - Build tool
- `{{PROJECT_SPECIFIC_TIPS}}` - Project-specific debugging tips

### `safe-debug-practices.mdc.template`

**Purpose**: Safety guidelines and checklists

**Placeholders**:
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition

### `error-pattern-detection.mdc.template`

**Purpose**: Common error pattern detection

**Placeholders**:
- `{{DESCRIPTION}}` - Rule description
- `{{RULE_TYPE}}` - Rule type
- `{{ALWAYS_APPLY}}` - true/false
- `{{GLOBS}}` - File pattern globs
- `{{WHEN_CONDITION}}` - When condition
- `{{ERROR_PATTERNS}}` - Error patterns to detect
- `{{ERROR_PATTERN_NAME}}` - Pattern name
- `{{ERROR_PATTERN_1}}` - First pattern
- `{{ERROR_PATTERN_2}}` - Second pattern (optional)
- `{{ERROR_PATTERN_3}}` - Third pattern (optional)
- `{{LIKELY_CAUSES}}` - Array of likely causes
- `{{MCP_TOOLS}}` - Array of MCP tools

## Command Templates

Location: `templates/commands/*.md`

### `command-template.md`

**Purpose**: Regular Cursor command template

**Placeholders**:
- `{{COMMAND_NAME}}` - Command name
- `{{COMMAND_DESCRIPTION}}` - Command description
- `{{INSTRUCTIONS}}` - Array of instruction steps
- `{{REFERENCE_FILES}}` - Array of reference files
- `{{TEMPLATE_STRUCTURE}}` - Template structure
- `{{TEMPLATE_LANGUAGE}}` - Template language
- `{{CATEGORY_PLACEMENT}}` - Array of category placements
- `{{VALIDATION_CHECKLIST}}` - Array of validation items
- `{{ADDITIONAL_SECTIONS}}` - Array of additional sections
- `{{EXAMPLE}}` - Example usage

### `feature-command-template.md`

**Purpose**: Feature scaffolding command template

**Placeholders**:
- `{{FEATURE_TYPE}}` - Type of feature
- `{{ADDITIONAL_PROMPTS}}` - Array of additional prompts
- `{{FEATURE_FILES}}` - Array of feature files
- `{{PROJECT_SPECIFIC}}` - Project-specific considerations
- `{{TEMPLATE_REFERENCE}}` - Template reference
- `{{EXAMPLE}}` - Example usage

## Template Selection Guide

### By Rule Purpose

**Type Safety** → `type-safety.mdc.template`
**Format Validation** → `format-validation.mdc.template`
**Accessibility** → `accessibility.mdc.template`
**File Organization** → `path-pattern.mdc.template` or `file-structure.mdc.template`
**Guidance/Reminders** → `keyword-detection.mdc.template`
**Workflow Documents** → `workflow-format.mdc.template`
**Project Detection** → `project-structure.mdc.template` or `tech-stack.mdc.template`
**Rule Improvement** → `rule-improvement.mdc.template`

### By Category

**Backend Rules**:
- `type-safety` - API types, database types
- `path-pattern` - API routes, server structure
- `keyword-detection` - Error handling, logging

**Frontend Rules**:
- `accessibility` - Alt text, ARIA labels
- `type-safety` - Component types
- `path-pattern` - Component structure

**General Rules**:
- `file-structure` - Required files
- `keyword-detection` - Best practices
- `path-pattern` - Global patterns

**Workflow Rules**:
- `workflow-format` - User stories, acceptance criteria
- `format-validation` - Document formats

**Meta Rules**:
- `rule-improvement` - Rule monitoring
- `project-structure` - Project detection
- `tech-stack` - Tech stack identification

## Creating Custom Templates

1. **Create template file** in appropriate directory
2. **Use standard placeholders** (`{{PLACEHOLDER_NAME}}`)
3. **Follow existing template structure**
4. **Document placeholders** in template comments
5. **Update command files** to reference new template
6. **Test template** with `/generate-rule`

## Template Best Practices

1. **Use descriptive placeholders**: Clear, self-documenting names
2. **Include all options**: Support both error and warning messages
3. **Make conditionals optional**: Use `{{#if}}` for optional content
4. **Document placeholders**: Add comments explaining each placeholder
5. **Keep templates focused**: One template, one purpose
6. **Test thoroughly**: Validate with various inputs

---

For usage examples, see [USAGE.md](USAGE.md)
For system architecture, see [ARCHITECTURE.md](ARCHITECTURE.md)

