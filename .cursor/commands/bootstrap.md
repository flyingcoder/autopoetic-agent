# Bootstrap Cursor Rules Boilerplate

Initialize the Cursor rules boilerplate system by generating foundational rules and establishing project context. This is Phase 1 of the setup process.

## Instructions

When this command is invoked via `/bootstrap` or when the user requests bootstrap initialization, you should:

### Step 1: Detect Project Structure

1. **Read project files to detect structure:**
   - Read `package.json` (if exists) to identify:
     - Framework (Next.js, React, Express, Vue, etc.)
     - Language (TypeScript/JavaScript from dependencies)
     - Build tool (Webpack, Vite, Next.js, etc.)
     - Key dependencies and libraries
   - Read `tsconfig.json` (if exists) to confirm TypeScript
   - Read `next.config.js` or `next.config.ts` (if exists) for Next.js
   - Read `vite.config.js` or `vite.config.ts` (if exists) for Vite
   - Check for other framework config files

2. **Document detected project structure:**
   - Framework: [detected framework or "unknown"]
   - Language: [TypeScript/JavaScript]
   - Build Tool: [detected build tool or "unknown"]
   - Key Libraries: [list major dependencies]

### Step 2: Generate Meta Rules First

Generate essential meta rules that other rules will reference. These must be created first:

1. **rule-generator.mdc** (`.cursor/rules/meta/rule-generator.mdc`):
   - Copy from existing `.cursor/rules/meta/rule-generator.mdc` if it exists
   - Or generate from the content you have access to
   - This enforces rule structure and format

2. **rule-generation-guide.mdc** (`.cursor/rules/meta/rule-generation-guide.mdc`):
   - Copy from existing `.cursor/rules/meta/rule-generation-guide.mdc` if it exists
   - Or generate from the content you have access to
   - This provides template and checklist for rule generation

3. **rule-improvement.mdc** (`.cursor/rules/meta/rule-improvement.mdc`):
   - Copy from existing `.cursor/rules/meta/rule-improvement.mdc` if it exists
   - Or generate from the content you have access to
   - This provides self-improvement guidelines

### Step 3: Generate Project Context Rules

Generate rules that establish project awareness. Use templates from `.cursor/templates/rules/`:

1. **project-structure.mdc** (`.cursor/rules/general/project-structure.mdc`):
   - Template: `.cursor/templates/rules/project-structure.mdc.template`
   - Replace placeholders with detected project info:
     - `{{RULE_NAME}}`: "Project Structure Detection"
     - `{{DESCRIPTION}}`: "Detects and documents project structure (framework, build tool, folder structure)"
     - `{{RULE_TYPE}}`: "guideline"
     - `{{ALWAYS_APPLY}}`: "true"
     - `{{WHEN_CONDITION}}`: "file.path contains project root or block.text contains 'project structure'"
     - `{{MESSAGE}}`: Include detected framework, language, build tool, folder structure patterns

2. **tech-stack.mdc** (`.cursor/rules/general/tech-stack.mdc`):
   - Template: `.cursor/templates/rules/tech-stack.mdc.template`
   - Replace placeholders with detected tech stack:
     - `{{RULE_NAME}}`: "Tech Stack Identification"
     - `{{DESCRIPTION}}`: "Identifies and enforces tech stack patterns (languages, libraries, versions)"
     - `{{RULE_TYPE}}`: "guideline"
     - `{{ALWAYS_APPLY}}`: "true"
     - `{{WHEN_CONDITION}}`: "file.path ends_with package.json or block.text contains 'import' or 'require'"
     - `{{MESSAGE}}`: Include detected languages, key libraries, versions, and tech stack patterns

3. **global-patterns.mdc** (`.cursor/rules/general/global-patterns.mdc`):
   - Template: `.cursor/templates/rules/keyword-detection.mdc.template`
   - Create a rule for common patterns across the project
   - Use detected project structure to customize patterns

### Step 4: Generate All Command Files

Generate all Cursor command files from templates in `.cursor/templates/commands/`:

1. **generate-rule.md** (`.cursor/commands/generate-rule.md`):
   - Copy from existing if it exists, or generate from template
   - Ensure it references project context checks

2. **generate-command.md** (`.cursor/commands/generate-command.md`):
   - Copy from existing if it exists, or generate from `.cursor/templates/commands/command-template.md`

3. **generate-feature.md** (`.cursor/commands/generate-feature.md`):
   - Copy from existing if it exists, or generate from `.cursor/templates/commands/feature-command-template.md`
   - Ensure it requires project context

4. **generate-debug-rule.md** (`.cursor/commands/generate-debug-rule.md`):
   - Copy from existing if it exists, or generate from template

5. **generate-category-rules.md** (`.cursor/commands/generate-category-rules.md`):
   - Generate new command for Phase 2 category-specific rule generation
   - This will be used after restart

6. **bootstrap.md** (`.cursor/commands/bootstrap.md`):
   - This file (already exists if command is running)

### Step 5: Ensure Directory Structure

Create necessary directories if they don't exist:
- `.cursor/rules/meta/`
- `.cursor/rules/general/`
- `.cursor/rules/backend/`
- `.cursor/rules/frontend/`
- `.cursor/rules/workflow/`
- `.cursor/commands/`

### Step 6: Generate Worktree Configuration

Generate `.cursor/worktrees.json` based on detected project structure:

1. **Determine project type:**
   - If `package.json` exists → Node.js project
   - If `requirements.txt` or `pyproject.toml` exists → Python project
   - Otherwise → Generic project

2. **Select appropriate template:**
   - Node.js: `.cursor/templates/worktrees/worktrees-nodejs.json.template`
   - Python: `.cursor/templates/worktrees/worktrees-python.json.template`
   - Generic: `.cursor/templates/worktrees/worktrees-generic.json.template`

3. **Customize based on detected tools:**
   - **Package Manager Detection:**
     - Check for `package-lock.json` → npm
     - Check for `pnpm-lock.yaml` → pnpm
     - Check for `bun.lockb` → bun
     - Check for `yarn.lock` → yarn
     - Default to `npm ci` if package.json exists
   
   - **Build Tool Detection:**
     - Next.js detected → may need build step
     - Vite detected → may need build step
     - Webpack detected → may need build step
   
   - **Database Detection:**
     - Check for Prisma (`prisma/schema.prisma`) → add `npm run db:migrate` or `npx prisma migrate dev`
     - Check for TypeORM → add migration command if detected
     - Check for other ORMs in dependencies
   
   - **Environment Files:**
     - Check for `.env`, `.env.local`, `.env.development`
     - Add copy commands for detected env files
     - Use `$ROOT_WORKTREE_PATH` (Unix) or `%ROOT_WORKTREE_PATH%` (Windows)

4. **Generate worktrees.json:**
   - Load selected template
   - Replace package manager commands if different from template default
   - Add database migration commands if detected
   - Add build commands if needed
   - Add environment file copy commands
   - Write to `.cursor/worktrees.json`

5. **Template customization examples:**
   - If pnpm detected: Replace `npm ci` with `pnpm install`
   - If bun detected: Replace `npm ci` with `bun install`
   - If Prisma detected: Add `npx prisma migrate dev` or `npm run db:migrate`
   - If Next.js detected: May add `npm run build` if needed
   - If multiple env files: Copy all detected env files

### Step 7: MCP Server Discovery (Optional)

Offer MCP server discovery based on detected project type:

1. **Detect if MCP would be useful:**
   - **Web Projects** (Next.js, React, Vue, etc.):
     - Strongly suggest: Linear, Figma, Browser Tools
     - Message: "🌐 Web development detected. Would you like to discover and configure MCP servers for Linear, Figma, and Browser Tools?"
   
   - **Mobile Projects** (Flutter, React Native):
     - Suggest: Mobile-specific MCP servers
     - Message: "📱 Mobile development detected. Would you like to discover MCP servers for mobile development?"
   
   - **Data Science Projects** (Python, Jupyter):
     - Suggest: Database and analysis MCP servers
     - Message: "📊 Data science project detected. Would you like to discover MCP servers for database access and analysis?"
   
   - **Generic Projects**:
     - Offer general MCP discovery
     - Message: "Would you like to discover MCP servers for your project?"

2. **If user wants MCP discovery:**
   - Ask: "Would you like to discover MCP servers now? (y/n)"
   - If yes:
     - Call discovery process (similar to `/discover-mcp-servers` command)
     - Present suggestions based on project type
     - Let user select servers
     - Generate `.cursor/mcp.json` if servers selected
   - If no:
     - Mention: "You can run `/discover-mcp-servers` later to set up MCP servers"

3. **MCP Discovery Process** (if user accepts):
   - Use web search to find relevant MCP servers
   - Prioritize based on project type (web first, then mobile, then others)
   - Present categorized suggestions
   - Generate configuration for selected servers
   - Include in completion message

### Step 8: Output Completion Message

After generating all files, output:

```
✅ Bootstrap Complete!

Generated files:
- Meta rules: rule-generator.mdc, rule-generation-guide.mdc, rule-improvement.mdc
- Project context: project-structure.mdc, tech-stack.mdc, global-patterns.mdc
- Commands: generate-rule.md, generate-command.md, generate-feature.md, generate-debug-rule.md, generate-category-rules.md
- Worktree config: worktrees.json

📋 Detected Project Structure:
- Framework: [detected framework]
- Language: [TypeScript/JavaScript]
- Build Tool: [detected build tool]
- Package Manager: [npm/pnpm/bun/yarn]
- Key Libraries: [list]

🌳 Worktree Configuration:
- Generated `.cursor/worktrees.json` for parallel agent support
- Configured for: [Node.js/Python/Generic]
- Includes: [dependency installation, env file copying, migrations if detected]

🔌 MCP Configuration:
{{#if MCP_SERVERS_SELECTED}}
- Generated `.cursor/mcp.json` with MCP servers:
  {{#each MCP_SERVERS}}
  - {{this.name}} ({{this.transport}})
  {{/each}}
- Next: Enable servers from Settings → Features → Model Context Protocol
{{else}}
- MCP servers not configured
- Run `/discover-mcp-servers` to set up MCP integration
{{/if}}

🔄 IMPORTANT: Please restart Cursor to load the new rules, then run:
   /generate-category-rules

This will generate backend, frontend, and workflow rules with full project context.
```

## Validation

Before completing, verify:
- All meta rules are generated
- Project context rules include detected information
- All command files are generated
- Directory structure exists
- Generated rules follow rule-generator.mdc validation requirements

## Reference

- Templates: `.cursor/templates/rules/`, `.cursor/templates/commands/`, `.cursor/templates/worktrees/`, `.cursor/templates/mcp/`
- Existing rules: `.cursor/rules/meta/` (if they exist)
- Worktree templates: `.cursor/templates/worktrees/`
- MCP templates: `.cursor/templates/mcp/`
- Cursor Documentation: https://cursor.com/docs
- Cursor Worktrees Documentation: https://cursor.com/docs/configuration/worktrees
- Cursor MCP Documentation: https://cursor.com/docs/context/mcp

