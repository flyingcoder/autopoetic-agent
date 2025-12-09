# Generate Cursor Command

Generate a new Cursor command file from templates. Cursor commands are markdown files in `.cursor/commands/` that provide instructions to the AI agent.

## Instructions

When this command is invoked via `/generate-command` or when the user requests command generation, you should:

1. **Ask the user for:**
   - Command name (e.g., "Generate Feature", "Setup Project")
   - Command description
   - Is this a feature command? (y/n)
   - Additional details based on command type

2. **Load the appropriate template from:**
   - Regular command: `.cursor/templates/commands/command-template.md`
   - Feature command: `.cursor/templates/commands/feature-command-template.md`

3. **Replace template placeholders:**
   - `{{COMMAND_NAME}}` - Name of the command
   - `{{COMMAND_DESCRIPTION}}` - Description
   - `{{INSTRUCTIONS}}` - Array of instruction steps
   - `{{REFERENCE_FILES}}` - Array of reference file paths
   - `{{FEATURE_TYPE}}` - Type of feature (if feature command)
   - `{{FEATURE_FILES}}` - Array of feature files (if feature command)
   - Additional placeholders as needed

4. **Generate the command file:**
   - Filename: `[command-name].md` (lowercase, hyphenated)
   - Location: `.cursor/commands/[command-name].md`
   - Ensure directory exists before writing

5. **After generation:**
   - Show the user the generated command file path
   - Display a preview of the generated content
   - Explain how to use the command (via `/command-name` in chat)

## Command Structure

Cursor commands are markdown files that:
- Provide clear instructions to the AI agent
- Use structured sections (Instructions, Reference Files, Examples)
- Can reference other files and templates
- Guide the AI through multi-step processes

## Example Usage

User: `/generate-command Create a command to scaffold new API endpoints`

You should:
1. Ask if it's a feature command (yes)
2. Collect feature type (API Endpoint)
3. Load `feature-command-template.md`
4. Replace placeholders with user input
5. Generate the command file
6. Show the result

## Reference

- Cursor Commands Documentation: https://cursor.com/docs
- See existing commands in `.cursor/commands/` for examples

