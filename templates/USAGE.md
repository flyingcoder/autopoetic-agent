# Boilerplate Usage Guide

Quick reference guide for using the Cursor Rules Boilerplate.

## Initial Setup (One-Time)

### Step 1: Bootstrap
```
/bootstrap
```

**What happens:**
- Detects your project structure
- Generates foundational rules
- Creates project context
- Generates all command files

**Output:**
```
✅ Bootstrap Complete!

Generated files:
- Meta rules: rule-generator.mdc, rule-generation-guide.mdc, rule-improvement.mdc
- Project context: project-structure.mdc, tech-stack.mdc, global-patterns.mdc
- Commands: [all command files]

📋 Detected Project Structure:
- Framework: Next.js
- Language: TypeScript
- Build Tool: Next.js
- Key Libraries: [list]

🔄 IMPORTANT: Please restart Cursor to load the new rules, then run:
   /generate-category-rules
```

### Step 2: Restart Cursor
- Close Cursor completely
- Reopen Cursor
- This loads the new rules into memory

### Step 3: Generate Category Rules
```
/generate-category-rules
```

**What happens:**
- Verifies project context exists
- Generates backend rules
- Generates frontend rules
- Generates workflow rules

**Output:**
```
✅ Category Rules Generated!

Backend Rules:
- api-type-safety.mdc
- no-any.mdc
- [other backend rules]

Frontend Rules:
- alt-text.mdc
- component-patterns.mdc
- [other frontend rules]

Workflow Rules:
- user-story-format.mdc
- acceptance-criteria.mdc
- [other workflow rules]
```

## Daily Usage

### Generate a Single Rule
```
/generate-rule
```

**Flow:**
1. AI asks: What should the rule enforce?
2. AI asks: Which template? (shows list)
3. AI asks: Which category?
4. AI asks: Rule type?
5. AI generates rule file

**Example:**
```
User: /generate-rule Require error handling in API routes

AI: Which template? (type-safety/path-pattern)
User: type-safety
AI: Which category? (backend/frontend/general/workflow/meta)
User: backend
AI: Rule type? (always/manual/guideline)
User: always
[Rule generated]
```

### Generate a Feature with Rules
```
/generate-feature
```

**Flow:**
1. AI checks for project context
2. AI asks: Feature name?
3. AI asks: Feature type?
4. AI generates multiple rules for the feature

**Example:**
```
User: /generate-feature Create user authentication API

AI: Reading project context (Next.js, TypeScript)...
     Feature name: user-authentication
     Feature type: API Endpoint
     Generating rules:
     - user-authentication-type-safety.mdc
     - user-authentication-path-pattern.mdc
```

### Generate a Debugging Rule
```
/generate-debug-rule
```

**Flow:**
1. AI checks for project context (optional)
2. AI asks: What type of debugging rule?
3. AI generates rule with MCP integration

**Example:**
```
User: /generate-debug-rule Create safe debugging rule

AI: What type? (mcp-integration/project-aware/safe-practices/error-patterns)
User: safe-practices
[Rule generated with project context if available]
```

### Generate a New Command
```
/generate-command
```

**Flow:**
1. AI asks: Command name?
2. AI asks: Is this a feature command?
3. AI generates command file

## Command Quick Reference

| Command | Purpose | Prerequisites |
|---------|---------|---------------|
| `/bootstrap` | Initialize system (Phase 1) | None |
| `/generate-category-rules` | Generate category rules (Phase 2) | Bootstrap + Restart |
| `/generate-rule` | Generate single rule | Project context for categories |
| `/generate-feature` | Generate feature with rules | Project context required |
| `/generate-debug-rule` | Generate debugging rule | Project context recommended |
| `/generate-command` | Generate new command | None |

## Template Selection Guide

### When to Use Each Template

**type-safety**
- Enforcing TypeScript types
- Preventing `any` types
- API handler type safety

**format-validation**
- User story format
- Acceptance criteria format
- Regex pattern validation

**accessibility**
- Image alt text
- ARIA labels
- HTML attribute requirements

**path-pattern**
- File structure validation
- Component organization
- API route patterns

**keyword-detection**
- Logging best practices
- Memory management
- Common pattern detection

**file-structure**
- Required files
- Folder structure
- File organization

**workflow-format**
- User stories
- Acceptance criteria
- Planning documents

**rule-improvement**
- Rule monitoring
- Pattern recognition
- Improvement triggers

**project-structure**
- Framework detection
- Build tool identification
- Folder structure patterns

**tech-stack**
- Library identification
- Version enforcement
- Dependency patterns

## Common Workflows

### Adding a New Rule Type

1. Create template in `templates/rules/`
2. Update `generate-rule.md` to include new template
3. Use `/generate-rule` with new template

### Updating Project Context

1. Run `/bootstrap` again
2. Restart Cursor
3. Regenerate category rules if needed

### Creating Custom Commands

1. Use `/generate-command`
2. Follow command template structure
3. Reference existing commands for examples

## Tips

1. **Always bootstrap first** - Project context is essential
2. **Restart after bootstrap** - Rules need to load
3. **Use project context** - Rules are smarter with context
4. **Follow templates** - Consistency is key
5. **Validate rules** - Check against rule-generator.mdc

## Troubleshooting Quick Fixes

**"Project context not found"**
→ Run `/bootstrap`, then restart Cursor

**"Template not found"**
→ Check template name matches exactly (case-sensitive)

**"Rules not working"**
→ Restart Cursor to load new rules

**"Category rules not generated"**
→ Verify project context exists, restart Cursor

---

For detailed documentation, see `BOILERPLATE.md`

