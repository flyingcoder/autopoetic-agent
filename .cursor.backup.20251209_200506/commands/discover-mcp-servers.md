# Discover MCP Servers

Intelligently discover and suggest MCP (Model Context Protocol) servers based on project context, prioritizing web development tools, then mobile development, then other technologies.

## Instructions

When this command is invoked via `/discover-mcp-servers` or when the user requests MCP server discovery, you should:

### Step 1: Analyze Project Context

1. **Read project context** (if available):
   - Read `.cursor/rules/general/project-structure.mdc` for framework and build tool
   - Read `.cursor/rules/general/tech-stack.mdc` for languages and libraries
   - Extract detected information

2. **Detect project type** (if context not available):
   - **Web Detection** (Priority 1):
     - Check for `package.json` with: Next.js, React, Vue, Angular, Express
     - Check for component libraries: Material-UI, Chakra UI, Tailwind
     - Check for testing: Playwright, Cypress, Jest
     - Check for design systems
   
   - **Mobile Detection** (Priority 2):
     - Check for `pubspec.yaml` → Flutter
     - Check for `package.json` with `react-native` → React Native
     - Check for iOS/Android native projects
   
   - **Data Science Detection**:
     - Check for Python files, Jupyter notebooks
     - Check for `requirements.txt`, `pyproject.toml`
     - Check for pandas, NumPy, scikit-learn in dependencies
     - Check for database usage (Prisma, TypeORM, Mongoose)

3. **Document detected project type:**
   - Project Type: [Web/Mobile/Data Science/Generic]
   - Framework: [detected framework]
   - Key Tools: [list detected tools]

### Step 2: Search for Relevant MCP Servers

1. **Use web search** to find MCP servers relevant to detected project type:
   - Search for: "MCP server [project type]" (e.g., "MCP server web development", "MCP server Flutter")
   - Search for: "Model Context Protocol server [framework]" (e.g., "Model Context Protocol server React")
   - Search for: "Cursor MCP [tool]" (e.g., "Cursor MCP Linear", "Cursor MCP Postgres")
   - Search for: "MCP server directory" to find official listings

2. **Reference official sources:**
   - Cursor MCP Directory: https://cursor.com/docs/context/mcp/directory
   - Model Context Protocol servers repository
   - Popular MCP server listings

3. **Categorize discovered servers** by priority tier:
   - **Tier 1 - Web Development** (if web project detected):
     - Linear MCP Server (project management)
     - Figma MCP Server (design system)
     - Browser Tools MCP Server (console/network)
     - Component Library MCP servers
     - API Testing MCP servers
   
   - **Tier 2 - Mobile Development** (if mobile project detected):
     - Flutter MCP servers
     - React Native MCP servers
     - Mobile testing MCP servers
   
   - **Tier 3 - Data Science** (if data science project detected):
     - Postgres, MySQL, MongoDB MCP servers
     - Jupyter MCP servers
     - Data visualization MCP servers
   
   - **Tier 4 - Generic/Other**:
     - File system MCP servers
     - API testing and monitoring
     - Error tracking and logging
     - Code analysis and linting

4. **Rank servers** by:
   - Relevance to project type (web projects get +10 for web servers)
   - Popularity and maintenance status
   - Documentation quality
   - Ease of setup
   - Official support

### Step 3: Present Suggestions with Priority

Present categorized suggestions to the user:

```
🌐 Web Development Tools (High Priority for your project):
⭐ Linear MCP Server
   - Project management integration
   - Use: Issue tracking, task management
   - Setup: npx -y mcp-remote https://mcp.linear.app/mcp
   - Reference: https://cursor.com/docs/cookbook/web-development

⭐ Figma MCP Server
   - Design system and mockup access
   - Use: Access designs, component specs
   - Setup: SSE transport (http://127.0.0.1:3845/sse)
   - Reference: https://help.figma.com/hc/en-us/articles/32132100833559

⭐ Browser Tools MCP Server
   - Console logs and network requests
   - Use: Verify implementations, monitor network
   - Setup: browsertools.agentdesk.ai/installation
   - Reference: https://cursor.com/docs/cookbook/web-development

📱 Mobile Development Tools:
Flutter MCP Server (if Flutter detected)
   - Flutter development workflows
   - Use: Widget development, hot reload monitoring

🗄️ Database Tools:
Postgres MCP Server (if database detected)
   - Database queries and schema inspection
   - Use: Query database, inspect schemas
   - Reference: https://cursor.com/docs/cookbook/data-science

Select which servers to configure: [interactive selection]
```

### Step 4: Interactive Server Selection

1. **Present servers** in priority order (web first, then mobile, then others)
2. **Offer presets:**
   - "Web Development Essentials" (Linear + Figma + Browser Tools)
   - "Full Web Stack" (Above + API testing + Component library)
   - "Mobile Development" (Flutter tools + Mobile testing)
   - "Data Science" (Database + Notebook execution)
   - "Custom Selection" (individual selection)

3. **For each selected server**, collect:
   - Confirmation of selection
   - Any custom configuration needed
   - Environment variables required
   - Transport method preference (if applicable)

### Step 5: Generate Configuration

1. **For each selected server:**
   - Load appropriate template from `.cursor/templates/mcp/`
   - Customize based on user input
   - Use config interpolation (${env:NAME}, ${workspaceFolder}, etc.)
   - Add to MCP configuration

2. **Generate MCP configuration:**
   - Create or update `.cursor/mcp.json` (project-specific configuration)
   - Provide instructions for global config (`~/.cursor/mcp.json`) if needed
   - Include setup instructions for each server
   - Use proper config interpolation for paths and environment variables

3. **Output configuration summary:**
   ```
   ✅ MCP Servers Configured:
   
   Selected Servers:
   - Linear MCP Server
   - Figma MCP Server
   - Browser Tools MCP Server
   
   Configuration File:
   - .cursor/mcp.json (project-specific)
   
   Next Steps:
   1. Enable servers from MCP settings (Settings → Features → Model Context Protocol)
   2. Authorize Linear (browser will open)
   3. Start Figma Dev Mode MCP Server
   4. Install Browser Tools MCP Server
   5. Verify in chat: "list all issues related to this project"
   
   Reference: .cursor/MCP.md for detailed setup instructions
   ```

## Smart Suggestions Based On Project Type

### Web Development Projects (Priority 1)

**Always suggest:**
- Linear MCP Server (project management) ⭐⭐⭐
- Figma MCP Server (design system) ⭐⭐⭐
- Browser Tools MCP Server (verification) ⭐⭐⭐

**Conditional suggestions:**
- If Next.js/React detected → Component library MCP, Storybook integration
- If API routes detected → API testing MCP servers
- If Playwright/Cypress detected → Browser automation MCP servers
- If component library detected → Design system MCP servers

### Mobile Development Projects (Priority 2)

**If Flutter detected:**
- Flutter tooling MCP servers ⭐⭐
- Mobile testing MCP servers ⭐⭐
- Platform API MCP servers ⭐

**If React Native detected:**
- React Native specific MCP servers ⭐⭐
- Metro bundler integration ⭐
- Platform bridge MCP servers ⭐

### Data Science Projects

**If Python/Jupyter detected:**
- Jupyter MCP servers ⭐⭐
- pandas/NumPy integration ⭐
- Notebook execution MCP servers ⭐⭐

**If database detected:**
- Postgres, MySQL, MongoDB MCP servers ⭐⭐
- Database query and schema inspection
- Migration tools

## Server Categories with Priority

### Tier 1 - Web Development (Highest Priority for Web Projects)

1. **Linear MCP Server** ⭐⭐⭐
   - Essential for web development
   - Project management integration
   - Issue tracking
   - Reference: https://cursor.com/docs/cookbook/web-development

2. **Figma MCP Server** ⭐⭐⭐
   - Essential for web development
   - Design system access
   - Component specifications
   - Reference: https://help.figma.com/hc/en-us/articles/32132100833559

3. **Browser Tools MCP Server** ⭐⭐⭐
   - Essential for web development
   - Console/network monitoring
   - Implementation verification
   - Reference: https://cursor.com/docs/cookbook/web-development

4. **Component Library MCP** ⭐⭐
   - If component library detected
   - Design system integration

5. **API Testing MCP** ⭐⭐
   - If API routes detected
   - API testing and monitoring

### Tier 2 - Mobile Development

1. **Flutter MCP Server** ⭐⭐
   - Flutter development workflows
   - Widget development

2. **Mobile Testing MCP** ⭐⭐
   - Device testing
   - UI testing frameworks

3. **Platform APIs MCP** ⭐
   - iOS/Android platform access

### Tier 3 - Data Science

1. **Postgres MCP Server** ⭐⭐
   - Database queries
   - Schema inspection
   - Reference: https://cursor.com/docs/cookbook/data-science

2. **Jupyter MCP Server** ⭐⭐
   - Notebook execution
   - Data analysis

3. **Other Database MCPs** ⭐
   - MySQL, MongoDB, Redis, SQLite

### Tier 4 - Generic/Other

1. **File System MCP** ⭐
2. **API Testing MCP** ⭐
3. **Error Tracking MCP** ⭐
4. **Code Analysis MCP** ⭐

## Ranking Algorithm

Score servers based on:
- **Project Type Match**: +10 for web projects (web servers), +5 for mobile (mobile servers)
- **Relevance Score**: Based on detected tools in project
- **Popularity Score**: From web search results
- **Maintenance Status**: Active repositories (+5), archived (-5)
- **Documentation Quality**: Comprehensive docs (+3), minimal docs (-2)
- **Ease of Setup**: Simple installation (+2), complex setup (-1)
- **Official Support**: Official MCP server (+5), community (+2)

## Configuration Details

### MCP Configuration Location

Based on [Cursor MCP Documentation](https://cursor.com/docs/context/mcp):
- **Project Configuration**: `.cursor/mcp.json` (project-specific tools)
- **Global Configuration**: `~/.cursor/mcp.json` (tools available everywhere)
- **Settings UI**: Settings → Features → Model Context Protocol

### Config Interpolation

Use variables in configuration:
- `${env:NAME}` - Environment variables
- `${userHome}` - Home folder path
- `${workspaceFolder}` - Project root
- `${workspaceFolderBasename}` - Project name
- `${pathSeparator}` / `${/}` - OS path separator

### Transport Methods

- **stdio**: Local execution, single user, shell command
- **SSE**: Server-Sent Events, multiple users, OAuth, URL endpoint
- **Streamable HTTP**: HTTP endpoint, multiple users, OAuth

## Reference

- Templates: `.cursor/templates/mcp/`
- MCP Rules: `.cursor/rules/general/mcp-usage.mdc`, `.cursor/rules/general/mcp-web-development.mdc`
- Documentation: `.cursor/MCP.md`
- [Cursor MCP Documentation](https://cursor.com/docs/context/mcp)
- [Cursor MCP Directory](https://cursor.com/docs/context/mcp/directory)
- [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)
- [Cursor Data Science Cookbook](https://cursor.com/docs/cookbook/data-science)
- [Cursor MCP Building Guide](https://cursor.com/docs/cookbook/building-mcp-server)

