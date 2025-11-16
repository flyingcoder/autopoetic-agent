# {{COMMAND_NAME}}

{{COMMAND_DESCRIPTION}}

## Instructions

When this command is invoked, you should:

{{#if INSTRUCTIONS}}
{{#each INSTRUCTIONS}}
{{@index}}. {{this}}
{{/each}}
{{else}}
1. Follow the steps outlined below
2. Reference relevant documentation
3. Validate outputs before completion
{{/if}}

{{#if REFERENCE_FILES}}
## Reference Files

{{#each REFERENCE_FILES}}
- {{this}}
{{/each}}
{{/if}}

{{#if TEMPLATE_STRUCTURE}}
## Template Structure

```{{TEMPLATE_LANGUAGE}}
{{TEMPLATE_STRUCTURE}}
```
{{/if}}

{{#if CATEGORY_PLACEMENT}}
## Category Placement

{{#each CATEGORY_PLACEMENT}}
- `{{this.path}}` - {{this.description}}
{{/each}}
{{/if}}

{{#if VALIDATION_CHECKLIST}}
## Validation Checklist

{{#each VALIDATION_CHECKLIST}}
- ✓ {{this}}
{{/each}}
{{/if}}

{{#if ADDITIONAL_SECTIONS}}
{{#each ADDITIONAL_SECTIONS}}
## {{this.title}}

{{this.content}}
{{/each}}
{{/if}}

{{#if EXAMPLE}}
## Example

{{EXAMPLE}}
{{/if}}

