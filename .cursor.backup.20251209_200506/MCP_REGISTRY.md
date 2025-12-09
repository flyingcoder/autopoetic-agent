# MCP Server Registry

Reference registry of MCP servers organized by category, with web development servers prioritized.

## Web Development (Priority 1)

### Linear MCP Server ⭐⭐⭐

**Essential for web development** - Project management integration.

- **Transport**: stdio
- **Command**: `npx -y mcp-remote https://mcp.linear.app/mcp`
- **Setup**: Requires OAuth authorization
- **Use Cases**: Issue tracking, task management, project requirements
- **Reference**: [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)

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

### Figma MCP Server ⭐⭐⭐

**Essential for web development** - Design system and mockup access.

- **Transport**: SSE
- **URL**: `http://127.0.0.1:3845/sse`
- **Setup**: Requires local Figma Dev Mode MCP Server installation
- **Use Cases**: Design system access, component specifications, design tokens
- **Reference**: [Figma Dev Mode MCP Server Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)

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

### Browser Tools MCP Server ⭐⭐⭐

**Essential for web development** - Console logs and network request monitoring.

- **Transport**: stdio
- **Command**: `npx -y @agentdesk/browser-tools-mcp`
- **Setup**: Follow installation at browsertools.agentdesk.ai
- **Use Cases**: Console monitoring, network request tracking, implementation verification
- **Reference**: [Cursor Web Development Cookbook](https://cursor.com/docs/cookbook/web-development)

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

### Component Library MCP Server

**For component library integration** - Design system component access.

- **Transport**: stdio (varies by implementation)
- **Use Cases**: Component library integration, design system access
- **Status**: Community implementations available

### API Testing MCP Server

**For API testing** - API endpoint testing and monitoring.

- **Transport**: stdio or HTTP (varies by implementation)
- **Use Cases**: API testing, endpoint monitoring, request/response validation
- **Status**: Community implementations available

## Mobile Development (Priority 2)

### Flutter MCP Server

**For Flutter development** - Flutter-specific tooling and workflows.

- **Transport**: stdio
- **Command**: `flutter mcp-server`
- **Setup**: Requires Flutter SDK, set `FLUTTER_ROOT` environment variable
- **Use Cases**: Widget development, hot reload monitoring, widget tree inspection
- **Status**: Community implementations available

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

### Mobile Testing MCP Server

**For mobile testing** - Device testing and automation.

- **Transport**: stdio (varies by implementation)
- **Use Cases**: Device testing, UI testing frameworks, mobile app debugging
- **Status**: Community implementations available

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

### React Native MCP Server

**For React Native development** - React Native specific tooling.

- **Transport**: stdio (varies by implementation)
- **Use Cases**: React Native development, Metro bundler integration, platform bridge access
- **Status**: Community implementations available

## Data Science

### Postgres MCP Server ⭐⭐

**For database access** - Query and inspect Postgres databases.

- **Transport**: stdio
- **Command**: `npx -y @modelcontextprotocol/server-postgres ${env:DATABASE_URL}`
- **Setup**: Requires `DATABASE_URL` environment variable
- **Use Cases**: SQL queries, schema inspection, database analysis
- **Reference**: [Cursor Data Science Cookbook](https://cursor.com/docs/cookbook/data-science)

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

### MySQL MCP Server

**For MySQL database access** - Query and inspect MySQL databases.

- **Transport**: stdio
- **Command**: `npx -y @modelcontextprotocol/server-mysql ${env:DATABASE_URL}`
- **Setup**: Requires `DATABASE_URL` environment variable
- **Use Cases**: SQL queries, schema inspection
- **Status**: Community implementations available

### MongoDB MCP Server

**For MongoDB database access** - Query and inspect MongoDB databases.

- **Transport**: stdio
- **Command**: `npx -y @modelcontextprotocol/server-mongodb ${env:MONGODB_URI}`
- **Setup**: Requires `MONGODB_URI` environment variable
- **Use Cases**: Document queries, collection inspection
- **Status**: Community implementations available

### Jupyter MCP Server

**For Jupyter notebook execution** - Execute and manage Jupyter notebooks.

- **Transport**: stdio
- **Command**: `python -m jupyter_mcp_server`
- **Setup**: Requires Python and Jupyter installation
- **Use Cases**: Notebook execution, data analysis workflows
- **Status**: Community implementations available

**Configuration:**
```json
{
  "mcpServers": {
    "jupyter": {
      "command": "python",
      "args": ["-m", "jupyter_mcp_server"],
      "env": {
        "JUPYTER_PATH": "${workspaceFolder}/.jupyter"
      }
    }
  }
}
```

## Generic/Other

### File System MCP Server

**For file system access** - Read and write files within workspace.

- **Transport**: stdio
- **Command**: `npx -y @modelcontextprotocol/server-filesystem ${workspaceFolder}`
- **Setup**: Simple, no additional setup required
- **Use Cases**: File operations, workspace management
- **Status**: Official MCP server

**Configuration:**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "${workspaceFolder}"
      ]
    }
  }
}
```

### SQLite MCP Server

**For SQLite database access** - Query and inspect SQLite databases.

- **Transport**: stdio
- **Command**: `npx -y @modelcontextprotocol/server-sqlite ${workspaceFolder}/database.db`
- **Setup**: Path to SQLite database file
- **Use Cases**: SQL queries, schema inspection
- **Status**: Official MCP server

### GitHub MCP Server

**For GitHub integration** - Access GitHub repositories and issues.

- **Transport**: stdio or HTTP (varies by implementation)
- **Setup**: Requires GitHub token
- **Use Cases**: Repository access, issue management, pull request operations
- **Status**: Community implementations available

### Slack MCP Server

**For Slack integration** - Access Slack channels and messages.

- **Transport**: HTTP/SSE
- **Setup**: Requires Slack API token
- **Use Cases**: Channel access, message sending, notification management
- **Status**: Community implementations available

## Server Discovery

### Finding New MCP Servers

1. **Official Directory**: [Cursor MCP Directory](https://cursor.com/docs/context/mcp/directory)
2. **Model Context Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)
3. **GitHub**: Search for "mcp-server" repositories
4. **npm**: Search for packages with "mcp" keyword
5. **Community**: Check Cursor community forums and Discord

### Adding to Registry

When discovering new MCP servers:
1. Test the server configuration
2. Document transport method, setup requirements, and use cases
3. Add to appropriate category in this registry
4. Update templates if needed (`.cursor/templates/mcp/`)

## Priority Tiers

### Tier 1 - Web Development (Highest Priority for Web Projects)

1. Linear MCP Server ⭐⭐⭐
2. Figma MCP Server ⭐⭐⭐
3. Browser Tools MCP Server ⭐⭐⭐
4. Component Library MCP ⭐⭐
5. API Testing MCP ⭐⭐

### Tier 2 - Mobile Development

1. Flutter MCP Server ⭐⭐
2. Mobile Testing MCP ⭐⭐
3. React Native MCP ⭐⭐
4. Platform APIs MCP ⭐

### Tier 3 - Data Science

1. Postgres MCP Server ⭐⭐
2. Jupyter MCP Server ⭐⭐
3. MySQL/MongoDB MCP ⭐
4. Data Visualization MCP ⭐

### Tier 4 - Generic/Other

1. File System MCP ⭐
2. SQLite MCP ⭐
3. GitHub MCP ⭐
4. Error Tracking MCP ⭐

## Reference

- **Templates**: `.cursor/templates/mcp/`
- **Documentation**: `.cursor/MCP.md`
- **Discovery Command**: `/discover-mcp-servers`
- **Config Command**: `/generate-mcp-config`
- **Official Docs**: [Cursor MCP Documentation](https://cursor.com/docs/context/mcp)
- **MCP Directory**: [Cursor MCP Directory](https://cursor.com/docs/context/mcp/directory)

