# Template Maintenance Guide

## Maintenance Philosophy

Templates require ongoing maintenance to remain current, accessible, and aligned with evolving web standards and Tailwind CSS updates. This guide establishes processes for keeping templates healthy.

## Regular Maintenance Tasks

### Quarterly Reviews

Every three months, review all templates for:

**Dependency Updates:**
- Tailwind CSS version compatibility
- Alpine.js version (if used)
- CDN links still functional
- Icon library updates

**Accessibility Improvements:**
- WCAG standards evolution
- Screen reader compatibility
- Keyboard navigation enhancements
- Color contrast adjustments

**Browser Compatibility:**
- New browser versions
- CSS feature support changes
- JavaScript API updates

**Performance Optimization:**
- Unused utility classes
- Image optimization opportunities
- Loading performance

## Responding to Issues

### Bug Reports

When users report bugs:

**1. Reproduce the issue:**
```
- Browser and version
- Screen size/device
- Steps to reproduce
- Expected vs actual behavior
```

**2. Diagnose root cause:**
- Review reported section of template
- Check browser DevTools for errors
- Test across multiple browsers if needed
- Verify accessibility tools if relevant

**3. Implement fix:**
- Make minimal necessary changes
- Follow existing code conventions
- Test thoroughly across breakpoints
- Update documentation if behavior changes

**4. Document the fix:**
```
git commit -m "Fix dropdown menu not closing on mobile

- Added @click.outside directive to close menu
- Improved touch target size for mobile
- Tested on iOS Safari and Android Chrome

Fixes #123"
```

### Enhancement Requests

Evaluate enhancement requests against criteria:

**Accept if:**
- Broadly applicable across use cases
- Maintains template simplicity
- Follows project conventions
- Improves accessibility or usability

**Decline if:**
- Highly specific to one use case
- Adds significant complexity
- Conflicts with project philosophy
- Better suited as variant template

## Tailwind CSS Updates

### Minor Version Updates (3.x to 3.y)

Minor updates usually require minimal changes:

**1. Test with new version:**
```html
<!-- Update CDN link -->
<script src="https://cdn.tailwindcss.com"></script>
```

**2. Check for deprecation warnings:**
- Review Tailwind CSS changelog
- Test all templates for visual changes
- Update any deprecated utilities

**3. Verify functionality:**
- Responsive behavior unchanged
- Custom configurations still work
- No unintended style changes

### Major Version Updates (3.x to 4.x)

Major updates may require significant changes:

**1. Review breaking changes:**
- Study official migration guide
- List affected utilities across templates
- Plan migration strategy

**2. Create migration branch:**
```bash
git checkout -b migrate-tailwind-v4
```

**3. Update templates systematically:**
- One template at a time
- Test thoroughly after each update
- Document any pattern changes

**4. Update documentation:**
- Revise `.context/` files for new patterns
- Update README files
- Add migration guide if significant

## Component Updates

### When to Update Components

Update extracted components when:

**Bug discovered:**
- Fix applies to all component instances
- Update component file
- Verify all templates using component
- Document in component header comments

**Accessibility improvement:**
- New ARIA pattern identified
- Keyboard navigation enhanced
- Screen reader experience improved

**New feature needed:**
- Enhancement benefits multiple templates
- Maintains backward compatibility
- Clear documentation provided

### Component Update Process

**1. Update component file:**

```html
<!--
  Component Name: Button Primary
  Version: 1.1.0
  Last Updated: 2024-01-15

  Changelog:
  - v1.1.0: Added disabled state styling
  - v1.0.0: Initial component
-->

<button type="button"
        class="px-6 py-3 bg-blue-600 text-white font-medium rounded-lg
               hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500
               disabled:opacity-50 disabled:cursor-not-allowed
               transition-colors duration-200">
  Button Text
</button>
```

**2. Test across all templates:**
- Locate all component instances
- Verify visual consistency
- Test interactive behavior
- Check accessibility

**3. Document changes:**
- Update component header
- Add changelog entry
- Update relevant template READMEs

## Documentation Updates

### Keeping Documentation Current

Documentation in `.context/` directory requires maintenance:

**When to update:**
- New patterns established across templates
- Best practices evolve
- User feedback identifies gaps
- Breaking changes in dependencies

**Update process:**
1. Identify outdated content
2. Revise with current practices
3. Add new examples if needed
4. Verify code examples still work
5. Update last modified date

**Example documentation update:**
```markdown
<!-- .context/components/patterns.md -->

## Component Patterns and Structure

*Last updated: 2024-01-15*

<!-- Updated content with new patterns -->
```

## Performance Maintenance

### Regular Performance Checks

Monitor template performance:

**Page Load Speed:**
```bash
# Test with browser DevTools Lighthouse
# Target scores:
# - Performance: 90+
# - Accessibility: 100
# - Best Practices: 90+
```

**CSS Size:**
- CDN version: Monitor Tailwind CSS updates
- Build process: Run PurgeCSS on production builds
- Target: < 10kb gzipped for production

**Image Optimization:**
- Compress preview.png images
- Use appropriate formats (WebP with fallbacks)
- Lazy load images below fold

### Optimization Opportunities

Look for:

**Unused Utilities:**
- Complex components with redundant classes
- Deprecated utilities still in use
- Opportunities for extraction

**JavaScript Optimization:**
- Minimize Alpine.js directives
- Remove unused event listeners
- Optimize state management

## Deprecation Process

When deprecating a template or component:

**1. Announce deprecation:**
- Add notice to README
- Set deprecation date (minimum 3 months out)
- Explain reasons and alternatives

```markdown
## ⚠️ Deprecation Notice

This template is deprecated as of 2024-01-15 and will be removed on 2024-04-15.

**Reason:** Superseded by `dashboard-modern-v2` with improved accessibility.

**Migration:** See `dashboard-modern-v2/MIGRATION.md` for upgrade guide.
```

**2. Maintain during deprecation period:**
- Fix critical bugs
- Update dependencies
- No new features

**3. Archive on removal date:**
- Move to `deprecated/` directory
- Update main README
- Keep available but unsupported

## Testing After Changes

### Change Testing Checklist

After any maintenance update:

- [ ] Visual regression test (compare before/after screenshots)
- [ ] Responsive behavior (mobile, tablet, desktop)
- [ ] Interactive elements (dropdowns, modals, forms)
- [ ] Keyboard navigation
- [ ] Screen reader (test with NVDA or VoiceOver)
- [ ] Multiple browsers (Chrome, Firefox, Safari, Edge)
- [ ] Color contrast (WCAG AA compliance)
- [ ] Console clean (no errors or warnings)

### Automated Testing (Future)

Consider implementing:
- Visual regression testing (Percy, Chromatic)
- Accessibility testing (axe, Lighthouse CI)
- Link checking
- HTML validation

## Version Control Best Practices

### Commit Messages

Use clear, descriptive commit messages:

```bash
# Good examples
git commit -m "Fix sidebar z-index on mobile devices"
git commit -m "Update dropdown menu to use new Alpine.js syntax"
git commit -m "Improve color contrast in stat cards for WCAG AA"

# Template for breaking changes
git commit -m "BREAKING: Update to Tailwind CSS v4

- Migrate from JIT to new engine
- Update utility class syntax
- Test all templates for compatibility

See MIGRATION.md for upgrade guide"
```

### Branching Strategy

For significant updates:

```bash
# Feature branch for new components
git checkout -b feature/add-notification-component

# Fix branch for bugs
git checkout -b fix/modal-scroll-lock

# Update branch for maintenance
git checkout -b update/tailwind-v3.4
```

## Communication

### Changelog Maintenance

Keep CHANGELOG.md updated:

```markdown
# Changelog

## [Unreleased]
### Added
- New analytics dashboard template

### Changed
- Updated sidebar component with improved mobile navigation
- Revised color contrast in card components

### Fixed
- Modal backdrop not preventing scroll on iOS
- Dropdown menu positioning on small screens

## [1.2.0] - 2024-01-15
### Added
- Dark mode support across all templates
...
```

### User Communication

For significant changes:
- Update README with migration guides
- Add notices to affected templates
- Document breaking changes clearly
- Provide before/after examples

This maintenance process ensures templates remain high quality, accessible, and aligned with current web standards as the project evolves.
