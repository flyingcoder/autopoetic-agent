# Generate {{FEATURE_TYPE}}

Generate a new {{FEATURE_TYPE}} following the project's standards and best practices.

## Instructions

When this command is invoked, you should:

1. **Ask the user for:**
   - Feature name and description
   - Feature location/path
   - Required dependencies or integrations
   {{#if ADDITIONAL_PROMPTS}}
   {{#each ADDITIONAL_PROMPTS}}
   - {{this}}
   {{/each}}
   {{/if}}

2. **Detect project structure:**
   - Framework type (Next.js, React, Express, etc.)
   - Language (TypeScript, JavaScript, etc.)
   - Build tool and configuration
   - Existing patterns and conventions

3. **Generate feature files:**
   {{#if FEATURE_FILES}}
   {{#each FEATURE_FILES}}
   - `{{this.path}}` - {{this.description}}
   {{/each}}
   {{else}}
   - Main feature file
   - Tests (if applicable)
   - Documentation
   - Related cursor rules
   {{/if}}

4. **Create feature-specific cursor rules:**
   - Use templates from `templates/rules/`
   - Generate rules appropriate for the feature type
   - Place rules in correct category folder

5. **Validate and test:**
   - Check file structure
   - Validate syntax
   - Ensure dependencies are available
   - Run basic validation tests

{{#if PROJECT_SPECIFIC}}
## Project-Specific Considerations

{{PROJECT_SPECIFIC}}
{{/if}}

{{#if TEMPLATE_REFERENCE}}
## Template Reference

See `templates/rules/` for available rule templates:
- `type-safety.mdc.template` - Type checking rules
- `format-validation.mdc.template` - Format validation
- `path-pattern.mdc.template` - Path matching rules
- And more...
{{/if}}

{{#if EXAMPLE}}
## Example

{{EXAMPLE}}
{{/if}}

