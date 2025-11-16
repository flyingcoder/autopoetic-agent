# Generate Debugging Rule

Generate a debugging helper rule with MCP integration support. These rules help with safe, project-aware debugging practices.

## Instructions

When this command is invoked via `/generate-debug-rule` or when the user requests debugging rule generation, you should:

**IMPORTANT - Project Context Recommended:**
- First check if `.cursor/rules/general/project-structure.mdc` exists
- First check if `.cursor/rules/general/tech-stack.mdc` exists
- **If these files exist:**
  - Read both files to extract project context
  - Use detected framework, language, and tech stack for better rule generation
- **If they don't exist:**
  - You can still generate debugging rules, but recommend running `/bootstrap` first for project-aware rules
  - For basic debugging rules (safe-practices, error-patterns), project context is optional

1. **Ask the user for:**
   - What type of debugging rule? (mcp-integration, project-aware, safe-practices, error-patterns)
   - Specific error patterns to detect (if applicable)

2. **Load the appropriate template from:**
   - `.cursor/templates/debugging/mcp-debug-helper.mdc.template`
   - `.cursor/templates/debugging/project-aware-debug.mdc.template`
   - `.cursor/templates/debugging/safe-debug-practices.mdc.template`
   - `.cursor/templates/debugging/error-pattern-detection.mdc.template`

3. **Use project context (if available):**
   - Read `.cursor/rules/general/project-structure.mdc` for framework and build tool
   - Read `.cursor/rules/general/tech-stack.mdc` for language and libraries
   - Use this information to customize debugging rules

4. **Replace template placeholders:**
   - `{{DESCRIPTION}}` - Rule description
   - `{{PROJECT_TYPE}}` - Detected project type
   - `{{FRAMEWORK}}` - Framework name
   - `{{LANGUAGE}}` - Language (TypeScript/JavaScript)
   - `{{BUILD_TOOL}}` - Build tool
   - `{{MCP_TOOLS}}` - MCP tool references (if applicable)
   - `{{ERROR_PATTERNS}}` - Error patterns to detect
   - Additional template-specific placeholders

5. **Generate the rule file:**
   - Filename: `[debug-rule-name].mdc`
   - Location: `.cursor/rules/general/[debug-rule-name].mdc` (debugging rules go in general/)
   - Ensure directory exists before writing

6. **After generation:**
   - Show the generated rule file path
   - Display a preview
   - Explain MCP integration points
   - Provide usage guidance

## Available Debugging Templates

- **mcp-debug-helper**: MCP tool integration and references
- **project-aware-debug**: Project structure detection for debugging
- **safe-debug-practices**: Safety guidelines and checklists
- **error-pattern-detection**: Common error pattern detection

## MCP Integration

When generating MCP-integrated rules:
- Reference MCP tools available in the project
- Use safe file inspection patterns
- Include project-aware context gathering
- Follow MCP best practices from https://cursor.com/docs

## Project-Aware Debugging

The rules should:
- Detect project type automatically
- Use appropriate file patterns for the framework
- Reference framework-specific debugging practices
- Include safe debugging checklists

## Example Usage

User: `/generate-debug-rule Create a rule for safe debugging with MCP tools`

You should:
1. Select `mcp-debug-helper` template
2. Detect project structure
3. Collect MCP tool information (if available)
4. Generate the rule with project-specific context
5. Show the result

## Reference

- Cursor Commands: https://cursor.com/docs
- MCP Documentation: https://cursor.com/docs
- See `.cursor/templates/debugging/` for all debugging templates

