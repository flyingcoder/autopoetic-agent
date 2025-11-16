# Generate Cursor Rule

Generate a new cursor rule from templates following the project's standards and validation requirements.

## Instructions

When this command is invoked via `/generate-rule` or when the user requests rule generation, you should:

**IMPORTANT - Project Context Check:**
- If the user wants to generate rules for `backend/`, `frontend/`, or `workflow/` categories:
  - First check if `.cursor/rules/general/project-structure.mdc` exists
  - First check if `.cursor/rules/general/tech-stack.mdc` exists
  - If these files don't exist, inform the user: "❌ Project context not found. Please run `/bootstrap` first to establish project context, then restart Cursor. After restart, you can generate category-specific rules."
  - If they exist, read them to understand the project structure and use that context when generating rules

1. **Ask the user for:**
   - What should the rule enforce? (e.g., "require error handling in API routes", "enforce TypeScript strict mode")
   - Which template to use? (type-safety, format-validation, accessibility, path-pattern, keyword-detection, file-structure, workflow-format, rule-improvement, project-structure, tech-stack)
   - Which category? (backend/frontend/general/workflow/meta)
   - Rule type? (always/manual/guideline/autoAttached)

2. **Load the appropriate template from:**
   - `.cursor/templates/rules/[template-name].mdc.template`

3. **Reference these files for validation:**
   - Template guide: `.cursor/rules/meta/rule-generation-guide.mdc`
   - Validation rules: `.cursor/rules/meta/rule-generator.mdc`
   - Rule improvement: `.cursor/rules/meta/rule-improvement.mdc` (for self-improvement guidelines)

4. **Replace template placeholders with user-provided values:**
   - `{{RULE_NAME}}` - Descriptive rule name
   - `{{DESCRIPTION}}` - Rule description
   - `{{CATEGORY}}` - Category folder
   - `{{RULE_TYPE}}` - Rule type
   - `{{ALWAYS_APPLY}}` - true or false
   - `{{GLOBS}}` - File pattern globs (optional)
   - `{{WHEN_CONDITION}}` - When condition
   - Template-specific placeholders (MUST_CONTAIN, PATTERN, ERROR_MESSAGE, etc.)
   
   **If generating backend/frontend/workflow rules:**
   - Reference project context from `.cursor/rules/general/project-structure.mdc` and `.cursor/rules/general/tech-stack.mdc`
   - Use detected framework, language, and tech stack in rule messages
   - Customize file patterns based on detected project structure

5. **Generate the rule file:**
   - Filename: `[rule-name].mdc` (lowercase, hyphenated)
   - Location: `.cursor/rules/[category]/[rule-name].mdc`
   - Ensure directory exists before writing

6. **Validation checklist (ensure all are met):**
   - ✓ YAML frontmatter with `---` delimiters
   - ✓ Description field included
   - ✓ Appropriate globs pattern (or omit if alwaysApply: true)
   - ✓ alwaysApply explicitly set
   - ✓ Rule name in double quotes
   - ✓ Rule type specified
   - ✓ When condition defined
   - ✓ Error/warn/message/valid field included
   - ✓ File placed in correct category folder

7. **After generation:**
   - Show the user the generated rule file path
   - Display a preview of the generated content
   - Confirm the rule follows validation requirements

## Available Templates

- **type-safety**: Type checking rules (TypeScript, API types)
- **format-validation**: Regex-based format validation
- **accessibility**: HTML/JSX attribute checks
- **path-pattern**: File path matching rules
- **keyword-detection**: Keyword-based guidance rules
- **file-structure**: File organization rules
- **workflow-format**: User story, acceptance criteria templates
- **rule-improvement**: Rule improvement and monitoring rules (for self-improvement system)
- **project-structure**: Project structure detection and documentation
- **tech-stack**: Tech stack identification and enforcement

## Category Placement

- `backend/` - API, server, database rules
- `frontend/` - Components, UI, styling rules
- `general/` - Cross-cutting concerns (memory, modes, behavior)
- `workflow/` - Process rules (user stories, planning, tasks)
- `meta/` - Rules about the rule system itself

## Rule Types

- `always`: Enforced automatically, blocks violations
- `manual`: Reminder/guideline, doesn't block
- `guideline`: Best practice suggestion
- `autoAttached`: Auto-attached in specific contexts

## Example Usage

User: `/generate-rule Create a rule that requires all API routes to have error handling`

You should:
1. Select `type-safety` or `path-pattern` template
2. Ask for category (backend)
3. Ask for rule type (always)
4. Collect template-specific details
5. Generate the rule file
6. Show the result
