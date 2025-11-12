# AI Agent Guide - Free Tailwind Templates

## Purpose

This file serves as a navigation index for AI agents working with this repository. It directs agents to relevant context documentation in the `.context/` directory based on the task at hand.

## Quick Reference Map

Use this index to locate the appropriate context files for your current task:

### Understanding the Project

**First time working with this repository?**
- Start with `.context/substrate.md` for complete project overview, philosophy, and structure

**Need to understand the codebase architecture?**
- Read `.context/architecture/overview.md` for template organization patterns
- Read `.context/architecture/dependencies.md` for Tailwind and tooling setup
- Read `.context/architecture/patterns.md` for common architectural decisions

### Creating or Modifying Templates

**Building a new template?**
- Read `.context/templates/creation-guide.md` for step-by-step template creation process
- Read `.context/styling/conventions.md` for Tailwind utility class patterns
- Read `.context/styling/responsive-design.md` for mobile-first breakpoint strategies
- Read `.context/components/patterns.md` for reusable component extraction guidelines

**Modifying an existing template?**
- Read the template's own `README.md` in its folder first
- Reference `.context/templates/maintenance.md` for update guidelines
- Check `.context/styling/conventions.md` to maintain consistency

### Working with Components

**Creating reusable components?**
- Read `.context/components/patterns.md` for component structure and documentation
- Read `.context/components/accessibility.md` for WCAG compliance patterns
- Read `.context/styling/conventions.md` for naming and organization

**Adding interactivity?**
- Read `.context/components/interactivity.md` for JavaScript integration patterns
- Reference `.context/components/state-management.md` for Alpine.js examples

### Styling and Design

**Implementing designs?**
- Read `.context/styling/conventions.md` for Tailwind utility usage standards
- Read `.context/styling/responsive-design.md` for breakpoint strategies
- Read `.context/styling/theming.md` for color palette and dark mode patterns

**Ensuring consistency across templates?**
- Read `.context/styling/design-system.md` for spacing, typography, and color standards

### Contributing and Documentation

**Contributing new templates or components?**
- Read `.context/guidelines.md` for contribution workflow and quality standards
- Read `.context/templates/creation-guide.md` for template requirements
- Follow folder structure defined in `.context/architecture/overview.md`

**Writing documentation?**
- Follow patterns established in existing `.context/` files
- Maintain 400-800 word count per file
- Include 2-3 practical code examples
- Document decision rationales

## Context File Structure

```
.context/
├── substrate.md                    # Project overview and philosophy
├── architecture/
│   ├── overview.md                # Template organization patterns
│   ├── dependencies.md            # Tailwind setup and tooling
│   └── patterns.md                # Common architectural decisions
├── components/
│   ├── patterns.md                # Component structure and extraction
│   ├── accessibility.md           # WCAG compliance patterns
│   ├── interactivity.md           # JavaScript integration
│   └── state-management.md        # Alpine.js patterns
├── styling/
│   ├── conventions.md             # Tailwind utility standards
│   ├── responsive-design.md       # Mobile-first strategies
│   ├── theming.md                 # Colors and dark mode
│   └── design-system.md           # Spacing, typography, colors
├── templates/
│   ├── creation-guide.md          # Step-by-step template creation
│   └── maintenance.md             # Updating existing templates
└── guidelines.md                  # Contribution and usage guidelines
```

## Task-Based Navigation

### Common Task Scenarios

**Scenario: "Create a new dashboard template"**
1. `.context/substrate.md` - Understand project goals
2. `.context/architecture/overview.md` - Learn template structure
3. `.context/templates/creation-guide.md` - Follow creation steps
4. `.context/styling/conventions.md` - Apply consistent styling
5. `.context/components/patterns.md` - Build reusable components

**Scenario: "Fix accessibility issues in a component"**
1. `.context/components/accessibility.md` - Review WCAG patterns
2. `.context/components/patterns.md` - Understand component structure
3. Template's specific `README.md` - Check component context

**Scenario: "Add dark mode support to a template"**
1. `.context/styling/theming.md` - Learn dark mode patterns
2. `.context/styling/design-system.md` - Review color system
3. `.context/templates/maintenance.md` - Follow update guidelines

**Scenario: "Optimize template for mobile devices"**
1. `.context/styling/responsive-design.md` - Review mobile-first patterns
2. `.context/architecture/patterns.md` - Check responsive architectural decisions
3. Template's `README.md` - Understand specific layout considerations

**Scenario: "Extract a component from a template"**
1. `.context/components/patterns.md` - Learn extraction criteria
2. `.context/architecture/overview.md` - Understand component file structure
3. `.context/styling/conventions.md` - Maintain naming consistency

## Best Practices for AI Agents

### Context Loading Strategy

1. **Always start with substrate.md** for project understanding
2. **Load relevant domain files** based on current task
3. **Reference multiple files** when tasks span domains
4. **Check template-specific READMEs** for local context

### Decision Making

When making architectural or design decisions:
1. Reference existing patterns in `.context/architecture/patterns.md`
2. Follow styling conventions from `.context/styling/conventions.md`
3. Maintain consistency with examples in substrate documentation
4. Document new patterns if they deviate from established standards

### Code Generation

When generating template or component code:
1. Follow HTML structure from `.context/architecture/overview.md`
2. Apply Tailwind patterns from `.context/styling/conventions.md`
3. Ensure accessibility per `.context/components/accessibility.md`
4. Include documentation comments per `.context/components/patterns.md`

### Quality Assurance

Before completing any task, verify:
- [ ] Code follows patterns documented in `.context/`
- [ ] Styling adheres to conventions
- [ ] Accessibility standards are met
- [ ] Documentation is updated if patterns changed
- [ ] Template folder structure matches architectural overview

## Updating This Guide

When adding new context files to `.context/`, update this agents.md file to include:
- New file location in the structure diagram
- Relevant task scenarios that should reference the new file
- Quick reference map entries for easy navigation

This ensures AI agents can efficiently locate and utilize all available context as the documentation evolves.
