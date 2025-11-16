# Generate Category Rules

Generate backend, frontend, and workflow rules with full project context awareness. This is Phase 2 of the setup process and requires project context to be established first.

## Instructions

When this command is invoked via `/generate-category-rules` or when the user requests category rule generation, you should:

### Step 1: Verify Project Context Exists

**CRITICAL**: Before proceeding, verify that project context rules exist:

1. Check for `.cursor/rules/general/project-structure.mdc`
2. Check for `.cursor/rules/general/tech-stack.mdc`

**If these files don't exist:**
- Stop and inform the user: "❌ Project context not found. Please run `/bootstrap` first to establish project context."
- Do not proceed with category rule generation

**If these files exist:**
- Read both files to extract:
  - Detected framework
  - Detected language (TypeScript/JavaScript)
  - Detected build tool
  - Key libraries and dependencies
  - Project structure patterns

### Step 2: Generate Backend Rules

Using the detected project context, generate backend rules:

1. **Determine backend technology:**
   - Check if Next.js API routes (`pages/api/` or `app/api/`)
   - Check for Express, Fastify, or other backend frameworks
   - Check for database libraries (Prisma, TypeORM, etc.)
   - Check for API libraries (tRPC, GraphQL, REST)

2. **Generate backend rules using templates:**
   - **api-type-safety.mdc** (if API routes detected):
     - Template: `.cursor/templates/rules/type-safety.mdc.template`
     - Enforce proper API handler types
     - Use detected framework patterns (Next.js, Express, etc.)
   
   - **no-any.mdc** (if TypeScript detected):
     - Template: `.cursor/templates/rules/type-safety.mdc.template`
     - Enforce no `any` types in backend code
   
   - **database-patterns.mdc** (if database library detected):
     - Template: `.cursor/templates/rules/path-pattern.mdc.template` or `.cursor/templates/rules/keyword-detection.mdc.template`
     - Enforce database query patterns based on detected library

3. **Place in**: `.cursor/rules/backend/`

### Step 3: Generate Frontend Rules

Using the detected project context, generate frontend rules:

1. **Determine frontend technology:**
   - Check detected framework (Next.js, React, Vue, etc.)
   - Check for UI libraries (Tailwind, Material-UI, etc.)
   - Check for state management (Redux, Zustand, etc.)

2. **Generate frontend rules using templates:**
   - **alt-text.mdc**:
     - Template: `.cursor/templates/rules/accessibility.mdc.template`
     - Enforce alt text on images
   
   - **component-patterns.mdc** (if React/Next.js detected):
     - Template: `.cursor/templates/rules/path-pattern.mdc.template`
     - Enforce component structure patterns
   
   - **styling-patterns.mdc** (if Tailwind/CSS framework detected):
     - Template: `.cursor/templates/rules/keyword-detection.mdc.template`
     - Enforce styling patterns based on detected framework

3. **Place in**: `.cursor/rules/frontend/`

### Step 4: Generate Workflow Rules

Generate workflow rules that apply to the project:

1. **Generate workflow rules using templates:**
   - **user-story-format.mdc**:
     - Template: `.cursor/templates/rules/workflow-format.mdc.template`
     - Enforce user story format
   
   - **acceptance-criteria.mdc**:
     - Template: `.cursor/templates/rules/workflow-format.mdc.template`
     - Enforce acceptance criteria format
   
   - **testable-format.mdc**:
     - Template: `.cursor/templates/rules/workflow-format.mdc.template`
     - Enforce testable format for criteria

2. **Place in**: `.cursor/rules/workflow/`

### Step 5: Reference Project Context

When generating each rule:
- Reference the detected framework in rule messages
- Use appropriate file patterns based on detected structure
- Include framework-specific best practices
- Reference tech stack information from project-structure.mdc and tech-stack.mdc

### Step 6: Validate Generated Rules

For each generated rule:
- Ensure it follows `.cursor/rules/meta/rule-generator.mdc` requirements
- Verify YAML frontmatter is correct
- Check that rule type, when condition, and message/error are present
- Ensure file is in correct category folder

### Step 7: Output Summary

After generating all category rules, output:

```
✅ Category Rules Generated!

Backend Rules:
- [list of generated backend rules]

Frontend Rules:
- [list of generated frontend rules]

Workflow Rules:
- [list of generated workflow rules]

📋 Rules generated using project context:
- Framework: [detected framework]
- Language: [TypeScript/JavaScript]
- Build Tool: [detected build tool]

All rules are now active and will guide development based on your project structure.
```

## Important Notes

1. **Project Context Required**: This command MUST NOT run without project context
2. **Use Detected Info**: Always reference project-structure.mdc and tech-stack.mdc when generating rules
3. **Framework-Specific**: Generate rules that match the detected framework and tech stack
4. **Template-Based**: Use templates from `.cursor/templates/rules/` for consistency

## Reference

- Project Context: `.cursor/rules/general/project-structure.mdc` and `.cursor/rules/general/tech-stack.mdc`
- Templates: `.cursor/templates/rules/`
- Validation: `.cursor/rules/meta/rule-generator.mdc`
- Cursor Documentation: https://cursor.com/docs

