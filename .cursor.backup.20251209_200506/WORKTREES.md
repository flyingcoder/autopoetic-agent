# Cursor Worktrees (Parallel Agents) Guide

Complete guide to using Cursor's worktree feature for parallel agents in this boilerplate system.

## What are Worktrees?

Worktrees allow you to run multiple Cursor agents in parallel, each in its own isolated Git branch. This enables:

- **Parallel Development**: Work on multiple features simultaneously
- **Best-of-N**: Run the same prompt across multiple models and compare results
- **Safe Experimentation**: Test changes without affecting your main branch
- **Independent Testing**: Each worktree can build and test independently

Reference: [Cursor Worktrees Documentation](https://cursor.com/docs/configuration/worktrees)

## Automatic Configuration

The boilerplate system automatically generates `.cursor/worktrees.json` during bootstrap:

1. **Run `/bootstrap`** in your project
2. The system detects your project type (Node.js, Python, etc.)
3. Generates appropriate worktree configuration
4. Customizes based on detected tools (package manager, database, etc.)

## Configuration File Structure

The `.cursor/worktrees.json` file defines setup commands for new worktrees:

```json
{
  "setup-worktree-unix": [
    "npm ci",
    "cp $ROOT_WORKTREE_PATH/.env .env"
  ],
  "setup-worktree-windows": [
    "npm ci",
    "copy %ROOT_WORKTREE_PATH%\\.env .env"
  ],
  "setup-worktree": [
    "npm ci",
    "echo 'Generic fallback'"
  ]
}
```

### Configuration Keys

- **`setup-worktree-unix`**: Commands for macOS/Linux (takes precedence on Unix systems)
- **`setup-worktree-windows`**: Commands for Windows (takes precedence on Windows)
- **`setup-worktree`**: Generic fallback for all operating systems

Each key accepts:
- **Array of shell commands** - executed sequentially
- **String filepath** - path to a script file relative to `.cursor/worktrees.json`

### Environment Variables

- **`$ROOT_WORKTREE_PATH`** (Unix): Path to the main working tree
- **`%ROOT_WORKTREE_PATH%`** (Windows): Path to the main working tree

Use these to copy files from your main tree to worktrees.

## Example Configurations

### Node.js with npm

```json
{
  "setup-worktree-unix": [
    "npm ci",
    "cp $ROOT_WORKTREE_PATH/.env .env"
  ],
  "setup-worktree-windows": [
    "npm ci",
    "copy %ROOT_WORKTREE_PATH%\\.env .env"
  ]
}
```

### Node.js with pnpm

```json
{
  "setup-worktree-unix": [
    "pnpm install",
    "cp $ROOT_WORKTREE_PATH/.env .env"
  ],
  "setup-worktree-windows": [
    "pnpm install",
    "copy %ROOT_WORKTREE_PATH%\\.env .env"
  ]
}
```

### Node.js with Prisma (Database Migrations)

```json
{
  "setup-worktree-unix": [
    "npm ci",
    "cp $ROOT_WORKTREE_PATH/.env .env",
    "npx prisma migrate dev"
  ],
  "setup-worktree-windows": [
    "npm ci",
    "copy %ROOT_WORKTREE_PATH%\\.env .env",
    "npx prisma migrate dev"
  ]
}
```

### Python with Virtual Environment

```json
{
  "setup-worktree-unix": [
    "python -m venv venv",
    "source venv/bin/activate && pip install -r requirements.txt",
    "cp $ROOT_WORKTREE_PATH/.env .env"
  ],
  "setup-worktree-windows": [
    "python -m venv venv",
    "venv\\Scripts\\activate && pip install -r requirements.txt",
    "copy %ROOT_WORKTREE_PATH%\\.env .env"
  ]
}
```

### With Build Step

```json
{
  "setup-worktree-unix": [
    "npm ci",
    "cp $ROOT_WORKTREE_PATH/.env .env",
    "npm run build"
  ]
}
```

### Using Script Files

For complex setups, reference script files:

```json
{
  "setup-worktree-unix": "setup-worktree-unix.sh",
  "setup-worktree-windows": "setup-worktree-windows.ps1"
}
```

Place scripts in `.cursor/` directory alongside `worktrees.json`.

## Using Worktrees

### Basic Usage

1. **Start a parallel agent** in Cursor
2. Cursor automatically creates a worktree
3. Agent works in isolation
4. Click **"Apply"** to merge changes back to your main branch
5. Click **"Keep"** to keep worktree for further work

### Best-of-N (Multiple Models)

1. Select multiple models when starting an agent
2. Each model runs in its own worktree
3. Compare solutions side-by-side
4. Choose the best solution or merge approaches
5. Apply the selected solution

### Apply Functionality

When you click "Apply":
1. Cursor attempts to cleanly merge changes
2. Changes are applied to your checked-out branch
3. For multiple applies in Best-of-N:
   - Choose "Full Overwrite" to replace all files
   - Use conflict resolution UI to merge multiple options

## Generating Worktree Configuration

### Automatic (During Bootstrap)

The `/bootstrap` command automatically generates worktree configuration:

- Detects project type (Node.js, Python, Generic)
- Detects package manager (npm, pnpm, bun, yarn)
- Detects database tools (Prisma, TypeORM, etc.)
- Detects environment files (.env, .env.local, etc.)
- Generates customized configuration

### Manual Generation

Use `/generate-worktree` to generate or update configuration:

1. Run `/generate-worktree`
2. Answer questions about your project
3. Configuration is generated or updated
4. Customize as needed

## Best Practices

### Package Managers

- **Use fast package managers** when possible:
  - `bun` - Fastest for Node.js
  - `pnpm` - Fast and efficient
  - `uv` - Fast for Python
- **Use `npm ci`** instead of `npm install` for deterministic installs
- **Avoid symlinking dependencies** - can cause issues in main worktree

### Environment Files

- **Copy environment files** from main tree to worktree
- Use `$ROOT_WORKTREE_PATH` (Unix) or `%ROOT_WORKTREE_PATH%` (Windows)
- Copy all necessary env files (.env, .env.local, etc.)

### Database Migrations

- **Run migrations in worktree setup** if your project uses databases
- Ensures worktree has proper database schema
- Use appropriate migration command for your ORM

### Build Steps

- **Include build steps** if your project requires compilation
- Ensures worktree can test and run code
- Only if necessary (some projects don't need builds)

## Troubleshooting

### Worktree Setup Fails

1. **Check setup commands** in `.cursor/worktrees.json`
2. **Verify package manager** is correct
3. **Check environment variables** are properly referenced
4. **Review Output panel** - Select "Worktrees Setup" from dropdown

### Changes Not Applying

1. **Review conflicts** in merge UI
2. **Choose merge strategy** (Full Overwrite or Merge)
3. **Check worktree status** with `git worktree list`

### Performance Issues

1. **Use fast package managers** (bun, pnpm)
2. **Avoid unnecessary build steps**
3. **Check worktree cleanup settings** in Cursor settings

### LSP Not Working

- **Note**: Cursor currently does not support LSP in worktrees
- Agents won't be able to lint files in worktrees
- This is a known limitation being worked on

## Worktree Cleanup

Cursor automatically manages worktrees:

- **Per-workspace limit**: Up to 20 worktrees per workspace
- **Automatic cleanup**: Oldest worktrees removed when limit exceeded
- **Cleanup schedule**: Configurable in settings

### Settings

```json
{
  "cursor.worktreeCleanupIntervalHours": 6,
  "cursor.worktreeMaxCount": 20
}
```

## Viewing Worktrees

### In Terminal

Run `git worktree list` to see all worktrees:

```
/.../<repo>                                  15ae12e   [main]
/Users/<you>/.cursor/worktrees/<repo>/98Zlw  15ae12e   [feat-1-98Zlw]
/Users/<you>/.cursor/worktrees/<repo>/a4Xiu  15ae12e   [feat-2-a4Xiu]
```

### In SCM Pane

Enable `git.showCursorWorktrees` setting (defaults to `false`) to visualize worktrees in the SCM pane.

## Reference

- **Official Documentation**: https://cursor.com/docs/configuration/worktrees
- **Worktree Rules**: `.cursor/rules/general/worktree-usage.mdc`, `.cursor/rules/general/worktree-config.mdc`
- **Templates**: `.cursor/templates/worktrees/`
- **Generate Command**: `/generate-worktree`

## Related Commands

- `/bootstrap` - Auto-generates worktree config
- `/generate-worktree` - Manually generate or update config
- `/generate-rule` - Create custom worktree-related rules

