# Generate MCP Configuration

Generate or update `.cursor/mcp.json` configuration file for MCP (Model Context Protocol) servers, prioritizing web development tools.

## Instructions

When this command is invoked via `/generate-mcp-config` or when the user requests MCP configuration generation, you should:

### Step 1: Check Existing Configuration

1. **Check if `.cursor/mcp.json` exists:**
   - If it exists, ask user: "MCP configuration already exists. Do you want to update it or create a new one?"
   - If updating, read existing configuration to preserve customizations
   - If creating new, proceed with fresh generation

2. **Check for global config:**
   - Mention that global config can be at `~/.cursor/mcp.json`
   - Ask if they want project-specific (`.cursor/mcp.json`) or global config

### Step 2: Detect Project Context (Optional but Recommended)

**If project context exists:**
- Read `.cursor/rules/general/project-structure.mdc` for framework and build tool
- Read `.cursor/rules/general/tech-stack.mdc` for package manager and dependencies
- Use detected information to customize configuration

**If project context doesn't exist:**
- Detect project type by checking for:
  - `package.json` → Node.js/Web project
  - `pubspec.yaml` → Flutter project
  - `requirements.txt` or `pyproject.toml` → Python project
  - Otherwise → Generic project

### Step 3: Ask User for Configuration Details

1. **Project Type** (if not detected):
   - Web Development (Priority 1)
   - Mobile Development (Priority 2)
   - Data Science
   - Generic/Other

2. **Server Selection** (present in priority order):
   - **Web Development Servers** (if web project or selected):
     - Linear MCP Server
     - Figma MCP Server
     - Browser Tools MCP Server
     - Component Library MCP
     - API Testing MCP
   
   - **Mobile Development Servers** (if mobile project or selected):
     - Flutter MCP Server
     - Mobile Testing MCP
     - Platform APIs MCP
   
   - **Data Science Servers** (if data science or selected):
     - Postgres MCP Server
     - Jupyter MCP Server
     - Other database MCPs
   
   - **Generic Servers**:
     - File System MCP
     - API Testing MCP
     - Error Tracking MCP

3. **For each selected server**, ask for:
   - **Transport method**: stdio, SSE, or HTTP
   - **Command/URL**: Based on transport method
   - **Required environment variables**: List what's needed
   - **Additional configuration**: Custom args, headers, etc.

### Step 4: Select and Load Template

1. **Select appropriate template:**
   - Web Development: `.cursor/templates/mcp/mcp-web-base-template.json`
   - Individual servers: `.cursor/templates/mcp/mcp-[server]-template.json`
   - Mobile: `.cursor/templates/mcp/mcp-mobile-base-template.json`
   - Data Science: `.cursor/templates/mcp/mcp-datascience-base-template.json`
   - Generic: `.cursor/templates/mcp/mcp-stdio-template.json` or `mcp-http-template.json`

2. **Load template content**

### Step 5: Customize Configuration

1. **For stdio servers:**
   - Replace command if different (npx, node, python, etc.)
   - Replace args with user-provided or detected values
   - Add environment variables using `${env:NAME}` interpolation
   - Add envFile if needed: `${workspaceFolder}/.env`
   - Use path interpolation: `${workspaceFolder}`, `${userHome}`, etc.

2. **For HTTP/SSE servers:**
   - Replace URL with user-provided URL
   - Add headers if needed (using `${env:NAME}` for tokens)
   - Configure authentication

3. **Use config interpolation:**
   - `${env:NAME}` for environment variables
   - `${workspaceFolder}` for project root
   - `${userHome}` for home directory
   - `${workspaceFolderBasename}` for project name
   - `${pathSeparator}` for OS path separator

4. **Preserve existing customizations** (if updating):
   - Keep any custom servers that don't conflict
   - Merge new servers with existing ones
   - Maintain existing environment variable references

### Step 6: Generate mcp.json

1. **Create JSON structure:**
   ```json
   {
     "mcpServers": {
       "server-name": {
         "command": "npx",
         "args": ["-y", "mcp-server"],
         "env": {
           "API_KEY": "${env:API_KEY}"
         },
         "envFile": "${workspaceFolder}/.env"
       }
     }
   }
   ```

2. **Validate JSON structure:**
   - Ensure valid JSON syntax
   - Ensure `mcpServers` object exists
   - Check for proper transport method (command for stdio, url for HTTP/SSE)
   - Verify config interpolation syntax
   - Check for proper environment variable usage

3. **Write to `.cursor/mcp.json`** (project config)
   - Or provide instructions for `~/.cursor/mcp.json` (global config)

### Step 7: Output Summary

After generation, output:

```
✅ MCP Configuration Generated!

📄 Configuration File: .cursor/mcp.json

📋 Configured Servers:
- Linear MCP Server (stdio)
- Figma MCP Server (SSE)
- Browser Tools MCP Server (stdio)

⚙️ Configuration Details:
- Project-specific configuration (`.cursor/mcp.json`)
- Uses config interpolation (${env:NAME}, ${workspaceFolder})
- Environment variables required: DATABASE_URL, API_KEY

🌳 Next Steps:
1. Enable servers from MCP settings:
   - Settings → Features → Model Context Protocol
   - Toggle servers on/off as needed
2. Set up environment variables:
   - Create .env file with required variables
   - Or set in your shell environment
3. Authorize servers (if required):
   - Linear: Browser will open for OAuth
   - Figma: Start Figma Dev Mode MCP Server
4. Verify in chat:
   - "list all issues related to this project" (Linear)
   - "get designs of current selection in Figma" (Figma)

📚 Reference: .cursor/MCP.md for detailed setup instructions
🔗 Official Docs: https://cursor.com/docs/context/mcp
```

## Template Customization Examples

### Web Development Essentials

```json
{
  "mcpServers": {
    "Linear": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.linear.app/mcp"]
    },
    "Figma": {
      "url": "http://127.0.0.1:3845/sse"
    },
    "browser-tools": {
      "command": "npx",
      "args": ["-y", "@agentdesk/browser-tools-mcp"]
    }
  }
}
```

### Postgres with Environment Variable

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

### Flutter with Path Interpolation

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

### HTTP Server with Headers

```json
{
  "mcpServers": {
    "api-server": {
      "url": "https://api.example.com/mcp",
      "headers": {
        "Authorization": "Bearer ${env:API_TOKEN}"
      }
    }
  }
}
```

## Validation Checklist

Before completing, verify:
- ✓ Valid JSON syntax
- ✓ `mcpServers` object exists
- ✓ Each server has proper transport (command for stdio, url for HTTP/SSE)
- ✓ Config interpolation uses correct syntax (${env:NAME}, ${workspaceFolder}, etc.)
- ✓ Environment variables use `${env:NAME}` format (not hardcoded)
- ✓ Paths use interpolation when appropriate
- ✓ Server names are descriptive
- ✓ No hardcoded secrets or sensitive data

## Configuration Locations

Based on [Cursor MCP Documentation](https://cursor.com/docs/context/mcp):

- **Project Configuration**: `.cursor/mcp.json` (project-specific tools)
- **Global Configuration**: `~/.cursor/mcp.json` (tools available everywhere)
- **Settings UI**: Settings → Features → Model Context Protocol

**Decision**: Generate project-specific config (`.cursor/mcp.json`) by default, provide option for global config.

## Reference

- Templates: `.cursor/templates/mcp/`
- MCP Rules: `.cursor/rules/general/mcp-config.mdc`
- Documentation: `.cursor/MCP.md`
- [Cursor MCP Documentation](https://cursor.com/docs/context/mcp)
- [Cursor MCP Directory](https://cursor.com/docs/context/mcp/directory)
- Config Interpolation: `${env:NAME}`, `${workspaceFolder}`, `${userHome}`, etc.

