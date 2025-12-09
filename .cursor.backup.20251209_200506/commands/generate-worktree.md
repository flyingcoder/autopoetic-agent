# Generate Worktree Configuration

Generate or update `.cursor/worktrees.json` configuration file for Cursor's parallel agent (worktree) feature.

## Instructions

When this command is invoked via `/generate-worktree` or when the user requests worktree configuration generation, you should:

### Step 1: Check Existing Configuration

1. **Check if `.cursor/worktrees.json` exists:**
   - If it exists, ask user: "Worktree configuration already exists. Do you want to update it or create a new one?"
   - If updating, read existing configuration to preserve customizations
   - If creating new, proceed with fresh generation

### Step 2: Detect Project Context (Optional but Recommended)

**If project context exists:**
- Read `.cursor/rules/general/project-structure.mdc` for framework and build tool
- Read `.cursor/rules/general/tech-stack.mdc` for package manager and dependencies
- Use detected information to customize configuration

**If project context doesn't exist:**
- Detect project type by checking for:
  - `package.json` → Node.js project
  - `requirements.txt` or `pyproject.toml` → Python project
  - Otherwise → Generic project

### Step 3: Ask User for Configuration Details

1. **Project Type** (if not detected):
   - Node.js
   - Python
   - Generic/Other

2. **Package Manager** (for Node.js projects):
   - npm
   - pnpm
   - bun
   - yarn

3. **Additional Setup Steps:**
   - Database migrations needed? (Prisma, TypeORM, etc.)
   - Build step needed? (Next.js, Vite, etc.)
   - Environment files to copy? (.env, .env.local, etc.)
   - Other custom setup commands?

### Step 4: Select and Load Template

1. **Select appropriate template:**
   - Node.js: `.cursor/templates/worktrees/worktrees-nodejs.json.template`
   - Python: `.cursor/templates/worktrees/worktrees-python.json.template`
   - Generic: `.cursor/templates/worktrees/worktrees-generic.json.template`

2. **Load template content**

### Step 5: Customize Configuration

1. **Replace package manager commands:**
   - npm: `npm ci`
   - pnpm: `pnpm install`
   - bun: `bun install`
   - yarn: `yarn install --frozen-lockfile`

2. **Add database migration commands** (if requested):
   - Prisma: `npx prisma migrate dev` or `npm run db:migrate`
   - TypeORM: `npm run migration:run` or similar
   - Custom migration command if provided

3. **Add build commands** (if requested):
   - Next.js: `npm run build` (if needed)
   - Vite: `npm run build` (if needed)
   - Custom build command if provided

4. **Add environment file copy commands:**
   - For each env file (.env, .env.local, etc.):
     - Unix: `cp $ROOT_WORKTREE_PATH/.env .env`
     - Windows: `copy %ROOT_WORKTREE_PATH%\\.env .env`

5. **Preserve existing customizations** (if updating):
   - Keep any custom commands that don't conflict
   - Merge new commands with existing ones

### Step 6: Generate worktrees.json

1. **Create JSON structure:**
   ```json
   {
     "setup-worktree-unix": [
       "command1",
       "command2"
     ],
     "setup-worktree-windows": [
       "command1",
       "command2"
     ],
     "setup-worktree": [
       "fallback command"
     ]
   }
   ```

2. **Validate JSON structure:**
   - Ensure valid JSON syntax
   - Ensure at least one setup-worktree configuration exists
   - Check for proper OS-specific commands

3. **Write to `.cursor/worktrees.json`**

### Step 7: Output Summary

After generation, output:

```
✅ Worktree Configuration Generated!

📄 File: .cursor/worktrees.json

📋 Configuration:
- Project Type: [Node.js/Python/Generic]
- Package Manager: [npm/pnpm/bun/yarn]
- Setup Commands:
  - Unix: [list commands]
  - Windows: [list commands]
  - Generic: [list commands]

🌳 Next Steps:
- Worktrees will automatically use this configuration
- Run parallel agents to test the setup
- Customize as needed for your project

📚 Reference: https://cursor.com/docs/configuration/worktrees
```

## Template Customization Examples

### Node.js with pnpm and Prisma:
```json
{
  "setup-worktree-unix": [
    "pnpm install",
    "cp $ROOT_WORKTREE_PATH/.env .env",
    "npx prisma migrate dev"
  ],
  "setup-worktree-windows": [
    "pnpm install",
    "copy %ROOT_WORKTREE_PATH%\\.env .env",
    "npx prisma migrate dev"
  ]
}
```

### Python with multiple env files:
```json
{
  "setup-worktree-unix": [
    "python -m venv venv",
    "source venv/bin/activate && pip install -r requirements.txt",
    "cp $ROOT_WORKTREE_PATH/.env .env",
    "cp $ROOT_WORKTREE_PATH/.env.local .env.local"
  ]
}
```

## Validation Checklist

Before completing, verify:
- ✓ Valid JSON syntax
- ✓ At least one setup-worktree configuration
- ✓ OS-specific commands use proper syntax
- ✓ Environment variable references are correct ($ROOT_WORKTREE_PATH for Unix, %ROOT_WORKTREE_PATH% for Windows)
- ✓ Package manager commands match detected/selected manager
- ✓ Migration commands are appropriate for detected database tool

## Reference

- Templates: `.cursor/templates/worktrees/`
- Worktree Rules: `.cursor/rules/general/worktree-usage.mdc`, `.cursor/rules/general/worktree-config.mdc`
- Cursor Worktrees Documentation: https://cursor.com/docs/configuration/worktrees
- Environment Variable: `$ROOT_WORKTREE_PATH` (Unix) or `%ROOT_WORKTREE_PATH%` (Windows)

