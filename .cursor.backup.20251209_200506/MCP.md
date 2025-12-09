# Cursor MCP (Model Context Protocol) Guide

Complete guide to using MCP servers in this boilerplate system, with a focus on web development workflows, then mobile development, and extensibility for other technologies.

## What is MCP?

[Model Context Protocol (MCP)](https://cursor.com/docs/context/mcp) enables Cursor to connect to external tools and data sources. Instead of explaining your project structure repeatedly, integrate directly with your tools.

**Key Benefits:**
- Connect to databases, browsers, design tools, project management
- Reduce context switching
- Tight feedback loops
- Direct access to external systems

Reference: [Cursor MCP Documentation](https://cursor.com/docs/context/mcp)

## Web Development MCP Servers (Priority 1)

### Linear MCP Server ⭐⭐⭐

**Essential for web development** - Project management integration.

**Configuration:**
```json
{
  "mcpServers": {
    "Linear": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.linear.app/mcp"]
    }
  }
}
```

**Setup:**
1. Add to `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (global)
2. Enable from MCP settings (Settings → Features → Model Context Protocol)
3. Authorize with Linear (browser opens automatically)

**Usage:**
- "list all issues related to this project"
- Access task details and requirements
- Update issue status

**Reference**: [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)

### Figma MCP Server ⭐⭐⭐

**Essential for web development** - Design system and mockup access.

**Configuration:**
```json
{
  "mcpServers": {
    "Figma": {
      "url": "http://127.0.0.1:3845/sse"
    }
  }
}
```

**Setup:**
1. Install Figma Dev Mode MCP Server
2. Start the server locally
3. Add SSE URL to `.cursor/mcp.json`
4. Enable from MCP settings

**Usage:**
- "get designs of current selection in Figma"
- Access component specifications
- Extract design tokens (colors, spacing, typography)
- View layout measurements

**Reference**: [Figma Dev Mode MCP Server Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)

### Browser Tools MCP Server ⭐⭐⭐

**Essential for web development** - Console logs and network request monitoring.

**Configuration:**
```json
{
  "mcpServers": {
    "browser-tools": {
      "command": "npx",
      "args": ["-y", "@agentdesk/browser-tools-mcp"]
    }
  }
}
```

**Setup:**
1. Follow installation at [browsertools.agentdesk.ai/installation](https://browsertools.agentdesk.ai/installation)
2. Add to `.cursor/mcp.json`
3. Enable from MCP settings

**Usage:**
- Monitor console output
- Track network requests
- Verify implementations match designs
- Debug runtime issues

**Reference**: [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)

## Mobile Development MCP Servers (Priority 2)

### Flutter MCP Server

**For Flutter development** - Flutter-specific tooling and workflows.

**Configuration:**
```json
{
  "mcpServers": {
    "flutter-tools": {
      "command": "flutter",
      "args": ["mcp-server"],
      "env": {
        "FLUTTER_ROOT": "${env:FLUTTER_ROOT}"
      }
    }
  }
}
```

**Setup:**
1. Ensure Flutter SDK is installed
2. Set `FLUTTER_ROOT` environment variable
3. Add to `.cursor/mcp.json`
4. Enable from MCP settings

**Usage:**
- Flutter widget development
- Hot reload monitoring
- Widget tree inspection
- Device testing

### Mobile Testing MCP Server

**For mobile testing** - Device testing and automation.

**Configuration:**
```json
{
  "mcpServers": {
    "mobile-testing": {
      "command": "npx",
      "args": ["-y", "@mobile-testing/mcp-server"]
    }
  }
}
```

## Data Science MCP Servers

### Postgres MCP Server

**For database access** - Query and inspect Postgres databases.

**Configuration:**
```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "${env:DATABASE_URL}"
      ],
      "env": {
        "DATABASE_URL": "${env:DATABASE_URL}"
      }
    }
  }
}
```

**Setup:**
1. Set `DATABASE_URL` environment variable
2. Add to `.cursor/mcp.json`
3. Enable from MCP settings

**Usage:**
- Run SQL queries directly
- Inspect table schemas
- Analyze database structure

**Reference**: [Cursor Data Science Cookbook](https://cursor.com/docs/cookbook/data-science)

## Configuration

### Configuration Locations

Based on [Cursor MCP Documentation](https://cursor.com/docs/context/mcp):

- **Project Configuration**: `.cursor/mcp.json` (project-specific tools)
- **Global Configuration**: `~/.cursor/mcp.json` (tools available everywhere)
- **Settings UI**: Settings → Features → Model Context Protocol

### Config Interpolation

Use variables in `mcp.json` values. Cursor resolves variables in: `command`, `args`, `env`, `url`, and `headers`.

**Supported syntax:**
- `${env:NAME}` - Environment variables
- `${userHome}` - Path to your home folder
- `${workspaceFolder}` - Project root (folder containing `.cursor/mcp.json`)
- `${workspaceFolderBasename}` - Name of the project root
- `${pathSeparator}` / `${/}` - OS path separator

**Examples:**

```json
{
  "mcpServers": {
    "local-server": {
      "command": "python",
      "args": ["${workspaceFolder}/tools/mcp_server.py"],
      "env": {
        "API_KEY": "${env:API_KEY}"
      },
      "envFile": "${workspaceFolder}/.env"
    }
  }
}
```

```json
{
  "mcpServers": {
    "remote-server": {
      "url": "https://api.example.com/mcp",
      "headers": {
        "Authorization": "Bearer ${env:MY_SERVICE_TOKEN}"
      }
    }
  }
}
```

### Transport Methods

Cursor supports three transport methods:

| Transport | Execution | Deployment | Users | Input | Auth |
|:----------|:----------|:-----------|:------|:------|:-----|
| **stdio** | Local | Cursor manages | Single user | Shell command | Manual (env vars) |
| **SSE** | Local/Remote | Deploy as server | Multiple users | URL to SSE endpoint | OAuth |
| **Streamable HTTP** | Local/Remote | Deploy as server | Multiple users | URL to HTTP endpoint | OAuth |

**When to use each:**
- **stdio**: Local development, single user, simple setup
- **SSE/HTTP**: Team access, shared resources, centralized server

## Using MCP in Chat

### Automatic Tool Usage

The Composer Agent automatically uses MCP tools listed under "Available Tools" when relevant. Ask for a specific tool by name or describe what you need.

### Toggling Tools

Enable or disable MCP tools directly from the chat interface:
1. Click a tool name in the tools list to toggle it
2. Disabled tools won't be loaded into context or available to Agent
3. Or use Settings → Features → Model Context Protocol

### Tool Approval

Agent asks for approval before using MCP tools by default. Click the arrow next to the tool name to see arguments.

### Auto-run

Enable auto-run for Agent to use MCP tools without asking. Works like terminal commands. Configure in Auto-run settings.

## Web Development Workflow

### Tight Feedback Loops

**MCP-Enabled Workflow:**
1. **Linear MCP**: Pull task/issue requirements
2. **Figma MCP**: Access design specifications
3. **Implementation**: Build using component library
4. **Browser Tools MCP**: Verify implementation matches design
5. **Iterate**: Quick adjustments based on browser feedback

### Component Reuse

**With MCP Integration:**
- Use Figma MCP to access component specifications
- Reference existing UI components from your component library
- Create new components by orchestrating existing UI components
- Verify in browser using Browser Tools MCP

**Best Practices:**
- Reuse existing UI components from `/src/components/ui` (or your component path)
- These are the primitives you can build with
- Only create new components when existing ones don't solve the problem
- Maintain consistency with design system via Figma MCP

## Discovering MCP Servers

### Automatic Discovery

Run `/discover-mcp-servers` to:
- Analyze your project context
- Search for relevant MCP servers
- Get prioritized suggestions (web first, then mobile, then others)
- Select servers to configure
- Generate configuration automatically

### Manual Configuration

Run `/generate-mcp-config` to:
- Generate MCP configuration manually
- Configure specific servers
- Update existing configuration
- Customize server settings

### During Bootstrap

The `/bootstrap` command offers MCP discovery:
- Detects project type (web, mobile, data science)
- Suggests relevant MCP servers
- Generates configuration if servers selected

## Security Considerations

When installing MCP servers:

- **Verify the source**: Only install MCP servers from trusted developers and repositories
- **Review permissions**: Check what data and APIs the server will access
- **Limit API keys**: Use restricted API keys with minimal required permissions
- **Audit code**: For critical integrations, review the server's source code
- **Use environment variables**: Never hardcode secrets in `mcp.json`
- **Local vs Remote**: Prefer local stdio servers for sensitive data

Remember that MCP servers can access external services and execute code on your behalf. Always understand what a server does before installation.

## Troubleshooting

### MCP Server Not Working

1. **Check MCP logs**:
   - Open Output panel (Cmd+Shift+U)
   - Select "MCP Logs" from dropdown
   - Check for connection errors, authentication issues, or server crashes

2. **Verify configuration**:
   - Check `.cursor/mcp.json` syntax
   - Verify server is enabled in Settings → Features → Model Context Protocol
   - Check environment variables are set

3. **Test server manually**:
   - Try running server command directly
   - Verify network connectivity for HTTP/SSE servers
   - Check authentication (OAuth, API keys)

### Temporarily Disable Server

1. Open Settings (Cmd+Shift+J)
2. Go to Features → Model Context Protocol
3. Click toggle next to server to enable/disable
4. Disabled servers won't load or appear in chat

### Update MCP Server

**For npm-based servers:**
1. Remove server from settings
2. Clear npm cache: `npm cache clean --force`
3. Re-add server to get latest version

**For custom servers:**
- Update local files
- Restart Cursor

### Server Crashes or Timeouts

If an MCP server fails:
- Cursor shows error message in chat
- Tool call is marked as failed
- You can retry the operation
- Check logs for details
- Other MCP servers continue working normally

## Protocol Capabilities

Cursor supports these MCP protocol capabilities:

| Feature | Support | Description |
|:--------|:--------|:------------|
| **Tools** | Supported | Functions for the AI model to execute |
| **Prompts** | Supported | Templated messages and workflows for users |
| **Resources** | Supported | Structured data sources that can be read and referenced |
| **Roots** | Supported | Server-initiated inquiries into URI or filesystem boundaries |
| **Elicitation** | Supported | Server-initiated requests for additional information from users |

## Real-World Examples

### Web Development Workflow

See [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development) for practical examples:
- Integrating Linear for project management
- Using Figma for design system access
- Browser tools for verification

### Data Science Workflow

See [Cursor Data Science Cookbook](https://cursor.com/docs/cookbook/data-science) for examples:
- Postgres database integration
- Jupyter notebook support
- Data analysis workflows

## Reference

- **Official Documentation**: [Cursor MCP Documentation](https://cursor.com/docs/context/mcp)
- **MCP Directory**: [Browse Available Servers](https://cursor.com/docs/context/mcp/directory)
- **Web Development**: [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)
- **Data Science**: [Cursor Data Science Cookbook](https://cursor.com/docs/cookbook/data-science)
- **Building MCP Servers**: [Cursor MCP Building Guide](https://cursor.com/docs/cookbook/building-mcp-server)
- **Model Context Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)

## Related Commands

- `/discover-mcp-servers` - Discover and configure MCP servers
- `/generate-mcp-config` - Generate or update MCP configuration
- `/bootstrap` - Auto-offers MCP discovery during setup

## Related Rules

- `.cursor/rules/general/mcp-usage.mdc` - MCP usage guidelines
- `.cursor/rules/general/mcp-config.mdc` - MCP configuration validation
- `.cursor/rules/general/mcp-web-development.mdc` - Web development MCP guidelines
- `.cursor/rules/general/mcp-mobile-development.mdc` - Mobile development MCP guidelines
- `.cursor/rules/frontend/web-development-workflow.mdc` - Web development workflows
- `.cursor/rules/frontend/ui-components.mdc` - Component reuse patterns

