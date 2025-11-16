# Initial Rules Added to Boilerplate

This document describes the initial rules that were added to the boilerplate system to help generators execute efficiently.

## Meta Rules (7 total)

### Core Meta Rules (from Phase 2)
1. **rule-generator.mdc** - Validates rule structure and format
2. **rule-generation-guide.mdc** - Provides templates and checklists for rule generation
3. **rule-improvement.mdc** - Self-improvement system guidelines

### Additional Meta Rules (from cursor-bk review)
4. **generate-rule-command.mdc** - Directly helps with `/generate-rule` command execution
   - Provides guidance when user requests rule generation
   - References proper templates and validation
   
5. **mdc-format.mdc** - Ensures proper format usage
   - Prevents use of deprecated `.cursorrules` format
   - Enforces modular `.mdc` format
   
6. **meta-rule.mdc** - Encourages modular rule maintenance
   - Reminds to keep rules modular and context-scoped
   
7. **scope-check.mdc** - Validates rule file placement
   - Ensures rules are in correct category folders

## General Rules (4 total)

1. **good-behaviour.mdc** - Generic best practices for code generation
   - No hard-coded data unless requested
   - Validate ideas with testing
   - Write production-ready code
   - Don't cheat on tests
   - Test before claiming functionality works

2. **log-usage.mdc** - Generic logging best practice
   - Warns against `console.log` in production
   - Encourages structured logging

3. **auto-format.mdc** - Generic formatting reminder
   - Reminds to use Prettier or equivalent for TypeScript files

4. **proactive-agent.mdc** - Helps AI be more helpful during generation
   - Encourages proactive problem-solving
   - Suggests causes, solutions, and next steps

## Workflow Rules (3 total)

1. **user-story-format.mdc** - Generic workflow format validation
   - Validates "As a [user], I want to [goal] so that [reason]" format
   
2. **acceptance-criteria.mdc** - Generic workflow format validation
   - Ensures acceptance criteria section follows user stories
   
3. **vague-language.mdc** - Helps with clear communication
   - Warns against vague words like "quickly", "somehow", "maybe"

## Rules NOT Included

The following rules from `cursor-bk` were **NOT** included because they are:
- Too project-specific (e.g., `tailwind-check.mdc`, `routing-consistency.mdc`)
- Too workflow-system-specific (e.g., mode-based rules like `implement-main.mdc`, `mode-transition.mdc`)
- Too context-dependent (e.g., `memory-management.mdc`, `changelog.mdc`)

These can be generated later using `/generate-rule` when needed for specific projects.

## Total Initial Rules

- **Meta Rules**: 7 (3 core + 4 additional)
- **General Rules**: 4
- **Workflow Rules**: 3
- **Total**: 14 initial rules

These rules provide a solid foundation for the boilerplate system and help generators execute efficiently by:
1. Ensuring proper rule format and structure
2. Providing code quality guidelines
3. Supporting workflow documentation standards
4. Encouraging proactive problem-solving

