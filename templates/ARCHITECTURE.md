# Boilerplate Architecture

Technical architecture and design decisions for the Cursor Rules Boilerplate system.

## Design Principles

1. **AI-First**: Use Cursor commands instead of scripts
2. **Project-Aware**: Rules adapt to project structure
3. **Phased Initialization**: Context before content
4. **Template-Based**: Consistent rule generation
5. **Self-Improving**: Built-in improvement system

## System Components

### 1. Command System

**Location**: `.cursor/commands/`

**Purpose**: AI instructions for rule generation

**Commands**:
- `bootstrap.md` - Phase 1 initialization
- `generate-category-rules.md` - Phase 2 category generation
- `generate-rule.md` - Single rule generation
- `generate-feature.md` - Feature with rules
- `generate-debug-rule.md` - Debugging rules
- `generate-command.md` - New command generation

**How it works**:
- Commands are markdown files with instructions
- AI reads commands when invoked via `/command-name`
- Commands reference templates and existing rules
- Commands enforce prerequisites (project context)

### 2. Template System

**Location**: `templates/rules/`, `templates/debugging/`, `templates/commands/`

**Purpose**: Reusable rule and command templates

**Template Format**:
- Uses placeholder syntax: `{{PLACEHOLDER_NAME}}`
- Supports conditionals: `{{#if CONDITION}}...{{/if}}`
- Supports loops: `{{#each ARRAY}}...{{/each}}`

**Template Types**:
- Rule templates (`.mdc.template`)
- Command templates (`.md`)
- Debugging templates (`.mdc.template`)

### 3. Project Context System

**Location**: `.cursor/rules/general/project-structure.mdc`, `tech-stack.mdc`

**Purpose**: Store detected project information

**Context Rules**:
- `project-structure.mdc` - Framework, build tool, folder structure
- `tech-stack.mdc` - Language, libraries, versions
- `global-patterns.mdc` - Common patterns

**How it works**:
1. Bootstrap detects project structure
2. Generates context rules with detected info
3. Category rules read context during generation
4. Rules reference context in messages and patterns

### 4. Meta Rules System

**Location**: `.cursor/rules/meta/`

**Purpose**: Rules about the rule system itself

**Meta Rules**:
- `rule-generator.mdc` - Rule validation
- `rule-generation-guide.mdc` - Generation guide
- `rule-improvement.mdc` - Self-improvement system

**How it works**:
- Meta rules validate generated rules
- Provide guidelines for rule creation
- Enable self-improvement process

### 5. Self-Improvement System

**Location**: `.cursor/rules/meta/rule-improvement.mdc`

**Purpose**: Continuous rule improvement

**Components**:
- Improvement triggers
- Analysis process
- Pattern recognition
- Quality checks
- Deprecation process

**How it works**:
- Monitors codebase for patterns
- Suggests rule improvements
- Provides guidelines for updates
- Tracks rule effectiveness

## Data Flow

### Phase 1: Bootstrap Flow

```
User runs /bootstrap
    ↓
AI reads project files (package.json, tsconfig.json, etc.)
    ↓
AI detects project structure
    ↓
AI generates meta rules
    ↓
AI generates project context rules (with detected info)
    ↓
AI generates all command files
    ↓
User restarts Cursor
    ↓
Rules loaded into Cursor memory
```

### Phase 2: Category Generation Flow

```
User runs /generate-category-rules
    ↓
AI verifies project context exists
    ↓
AI reads project context rules
    ↓
AI extracts detected info (framework, language, etc.)
    ↓
AI generates backend rules (using context)
    ↓
AI generates frontend rules (using context)
    ↓
AI generates workflow rules (using context)
    ↓
Rules active and project-aware
```

### Rule Generation Flow

```
User runs /generate-rule
    ↓
AI checks if category rule (backend/frontend/workflow)
    ↓
If category: AI checks for project context
    ↓
AI asks for rule details
    ↓
AI loads template
    ↓
AI replaces placeholders (with project context if available)
    ↓
AI validates rule
    ↓
AI writes rule file
```

## Project Detection Algorithm

### Detection Steps

1. **Read package.json**
   - Check `dependencies` and `devDependencies`
   - Identify framework (next, react, express, vue)
   - Identify language (typescript, javascript)
   - Identify build tool (webpack, vite)
   - List key libraries

2. **Read Config Files**
   - `tsconfig.json` → TypeScript
   - `next.config.js` → Next.js
   - `vite.config.js` → Vite
   - Other framework configs

3. **Detect Folder Structure**
   - Check for `pages/`, `app/`, `components/`
   - Identify routing structure
   - Identify component organization

4. **Generate Context**
   - Create project-structure.mdc with detected info
   - Create tech-stack.mdc with detected info
   - Create global-patterns.mdc with common patterns

## Template Processing

### Placeholder Replacement

**Simple Replacement**:
```
{{RULE_NAME}} → "API Type Safety"
```

**Conditional Blocks**:
```
{{#if CONDITION}}
  content here
{{/if}}
```

**Loops**:
```
{{#each ARRAY}}
  {{this}}
{{/each}}
```

### Template Selection

**Rule Templates**:
- Selected by user or determined by rule type
- Located in `templates/rules/`
- Named: `[template-name].mdc.template`

**Command Templates**:
- Selected by command type
- Located in `templates/commands/`
- Named: `[template-name].md`

## Validation System

### Rule Validation

**Validated Against**:
- `.cursor/rules/meta/rule-generator.mdc`

**Checks**:
- YAML frontmatter present
- Description field included
- Rule type specified
- When condition defined
- Error/warn/message field present
- Correct category folder

### Context Validation

**Before Category Generation**:
- Verify project-structure.mdc exists
- Verify tech-stack.mdc exists
- Read and parse context rules

## Error Handling

### Missing Prerequisites

**Project Context Missing**:
- Error message: "❌ Project context not found. Please run `/bootstrap` first..."
- Action: Stop generation, instruct user

**Template Not Found**:
- Error message: "Template not found: [name]"
- Action: List available templates

**Validation Failure**:
- Error message: List validation errors
- Action: Show what's missing, don't write file

## Extension Points

### Adding New Templates

1. Create template file in appropriate directory
2. Use standard placeholder syntax
3. Update command files to reference new template
4. Document template usage

### Adding New Commands

1. Create command file in `.cursor/commands/`
2. Follow command template structure
3. Reference existing commands for examples
4. Document command usage

### Customizing Project Detection

1. Modify bootstrap.md detection logic
2. Add new config file checks
3. Update project-structure.mdc template
4. Test with various project types

## Performance Considerations

### Template Loading
- Templates are small files, loaded on-demand
- No caching needed (fast file reads)

### Project Detection
- Reads only necessary files (package.json, configs)
- Single pass detection
- Minimal file I/O

### Rule Generation
- Generates one rule at a time
- Validates before writing
- No batch processing needed

## Security Considerations

### File System Access
- Only reads project files (package.json, configs)
- Only writes to `.cursor/` directory
- No execution of code
- No network access

### Template Safety
- Templates are static files
- Placeholder replacement is text-based
- No code injection possible

## Future Enhancements

### Potential Additions
1. Rule versioning system
2. Rule migration tools
3. Rule effectiveness metrics
4. Automated rule suggestions
5. Rule conflict detection
6. Multi-project support

### Integration Opportunities
1. CI/CD integration
2. Code review integration
3. IDE plugin support
4. Rule marketplace
5. Community templates

---

**Architecture Version**: 1.0.0
**Last Updated**: 2024

