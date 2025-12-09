# Generate Feature with Cursor Rules

Generate a new feature with automatic cursor rule generation. This command detects project structure and creates appropriate rules.

## Instructions

When this command is invoked via `/generate-feature` or when the user requests feature generation, you should:

**IMPORTANT - Project Context Required:**
- First check if `.cursor/rules/general/project-structure.mdc` exists
- First check if `.cursor/rules/general/tech-stack.mdc` exists
- **If these files don't exist:**
  - Stop and inform the user: "❌ Project context not found. Please run `/bootstrap` first to establish project context, then restart Cursor. After restart, you can generate features with full project awareness."
  - Do not proceed with feature generation
- **If they exist:**
  - Read both files to extract project context:
    - Detected framework (Next.js, React, Express, etc.)
    - Detected language (TypeScript/JavaScript)
    - Detected build tool (Webpack, Vite, Next.js, etc.)
    - Key libraries and dependencies
    - Project structure patterns
  - Use this context for all rule generation

1. **Read project context from existing rules:**
   - Read `.cursor/rules/general/project-structure.mdc` for framework, build tool, folder structure
   - Read `.cursor/rules/general/tech-stack.mdc` for languages, libraries, versions
   - Extract detected information to use in rule generation

2. **Ask the user for:**
   - Feature name
   - Feature type (e.g., "API Endpoint", "React Component", "Utility Function")
   - Feature path (optional, relative to project root)

3. **Generate appropriate cursor rules:**
   - Use templates from `.cursor/templates/rules/`
   - Determine category based on feature type:
     - API/Endpoint → `backend/`
     - Component/Page → `frontend/`
     - Utility/General → `general/`
   - Generate rules based on project context (from project-structure.mdc and tech-stack.mdc):
     - If TypeScript detected: Generate type-safety rules
     - If frontend framework detected: Generate accessibility rules
     - All features: Generate path-pattern rules using detected project structure
   - Reference detected framework, language, and tech stack in rule messages
   - Use appropriate file patterns based on detected project structure

4. **Load templates and replace placeholders:**
   - Load appropriate template from `.cursor/templates/rules/[template-name].mdc.template`
   - Replace placeholders with:
     - Feature name
     - Category
     - Project-specific patterns
     - Appropriate file extensions (.ts, .tsx, .js, .jsx)

5. **Write rule files:**
   - Generate 2-3 rules per feature (type-safety, path-pattern, accessibility if frontend)
   - Filename: `[feature-name]-[rule-type].mdc`
   - Location: `.cursor/rules/[category]/[feature-name]-[rule-type].mdc`
   - Ensure category directory exists

6. **After generation:**
   - List all generated rules
   - Show file paths
   - Provide next steps for feature implementation
   - Mention MCP tools for safe debugging if needed

## Project Context

The command uses project context from:
- `.cursor/rules/general/project-structure.mdc` - Contains detected:
  - Framework (Next.js, React, Express, Vue, etc.)
  - Build Tool (Webpack, Vite, Next.js, etc.)
  - Folder structure patterns
- `.cursor/rules/general/tech-stack.mdc` - Contains detected:
  - Language (TypeScript or JavaScript)
  - Key libraries and dependencies
  - Versions and tech stack patterns

**Note**: Project context must be established first via `/bootstrap` command.

## Rule Generation Logic

1. **Type Safety Rule** (if TypeScript):
   - Template: `type-safety.mdc.template`
   - Enforce no `any` types
   - Target appropriate file extensions

2. **Path Pattern Rule**:
   - Template: `path-pattern.mdc.template`
   - Validate feature file structure
   - Provide guidance messages

3. **Accessibility Rule** (if frontend):
   - Template: `accessibility.mdc.template`
   - Enforce alt text, ARIA labels, etc.

## Example Usage

User: `/generate-feature Create a user authentication API endpoint`

You should:
1. Detect project (e.g., Next.js with TypeScript)
2. Ask for feature name: "user-authentication"
3. Confirm feature type: "API Endpoint"
4. Generate rules:
   - `user-authentication-type-safety.mdc` (backend)
   - `user-authentication-path-pattern.mdc` (backend)
5. Show generated files and next steps

## MCP Integration

When generating debugging-related rules, reference:
- MCP tools for safe file inspection
- Project-aware debugging templates in `.cursor/templates/debugging/`
- Safe debugging practices

## Reference

- Cursor Commands: https://cursor.com/docs
- MCP Documentation: https://cursor.com/docs
- See `templates/README.md` for template system details

