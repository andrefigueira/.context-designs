# Contribution and Usage Guidelines

## Project Purpose

This repository provides free, high-quality UI templates built with Tailwind CSS. Templates are designed to be copied, customized, and integrated into any project without dependencies beyond Tailwind itself.

## Usage Rights

### License

All templates are released under MIT License:

**You CAN:**
- Use in personal projects
- Use in commercial projects
- Modify and customize freely
- Distribute modified versions
- Use in client work

**You CANNOT:**
- Hold authors liable for damages
- Use trademark or branding without permission

**Attribution:**
- Not required but appreciated
- Link back to repository if convenient

### Integration Guidelines

**For new projects:**
1. Copy template folder to your project
2. Integrate with your Tailwind build process
3. Replace CDN with local Tailwind installation
4. Customize colors and spacing via config
5. Add your content and logic

**For existing projects:**
1. Review template HTML structure
2. Extract needed components
3. Adapt to your existing patterns
4. Maintain accessibility standards
5. Test responsive behavior

## Contributing

### Who Can Contribute

Everyone! We welcome contributions from:
- Developers wanting to share templates
- Designers providing mockups
- Users reporting bugs or suggesting improvements
- Documentation writers improving guides
- Accessibility experts enhancing compliance

### What to Contribute

**New Templates:**
- Modern, professional designs
- Clear use case and target audience
- Mobile-first responsive layouts
- WCAG AA accessibility compliance
- Comprehensive documentation

**Component Improvements:**
- Bug fixes
- Accessibility enhancements
- Performance optimizations
- New variations

**Documentation:**
- Tutorial additions
- Example improvements
- Clarity enhancements
- Translation (future)

**Bug Reports:**
- Clear reproduction steps
- Browser and device information
- Expected vs actual behavior
- Screenshots if helpful

### Contribution Process

**1. Check existing work:**
```bash
# Search issues for duplicates
# Review existing templates
# Read contribution guidelines
```

**2. Fork and branch:**
```bash
git clone https://github.com/your-username/free-templates.git
cd free-templates
git checkout -b feature/dashboard-analytics
```

**3. Follow standards:**
- Read `.context/` documentation thoroughly
- Follow naming conventions
- Match coding style
- Include proper documentation
- Test across devices

**4. Create pull request:**
```
Title: Add analytics dashboard template

Description:
New analytics dashboard template featuring:
- Responsive sidebar navigation
- Stats cards with trend indicators
- Chart placeholders
- Data table with sorting
- Full mobile support

Closes #45

Screenshots:
[Include preview images]

Testing:
- [x] Tested Chrome, Firefox, Safari, Edge
- [x] Tested mobile (375px) to desktop (1440px)
- [x] Screen reader tested with VoiceOver
- [x] WCAG AA color contrast verified
- [x] All interactive elements keyboard accessible
```

**5. Address feedback:**
- Respond to review comments
- Make requested changes
- Update documentation if needed
- Re-test after modifications

### Code Quality Standards

**HTML:**
- Semantic elements
- Proper nesting and indentation
- Meaningful class organization
- Accessibility attributes

**Tailwind CSS:**
- Follow established conventions (see `.context/styling/conventions.md`)
- Use design system patterns (see `.context/styling/design-system.md`)
- Maintain consistent spacing and colors
- Optimize utility class usage

**JavaScript (if needed):**
- Prefer Alpine.js for interactivity
- Keep logic simple and declarative
- Document complex interactions
- Ensure progressive enhancement

**Accessibility:**
- WCAG 2.1 Level AA minimum
- Keyboard navigation complete
- Screen reader tested
- Color contrast verified
- ARIA attributes where appropriate

**Documentation:**
- Complete README.md
- Component documentation headers
- Customization instructions
- Browser support notes

### Review Process

**Pull requests reviewed for:**
1. **Functionality**: Template works as described
2. **Code quality**: Follows project conventions
3. **Accessibility**: Meets WCAG standards
4. **Responsiveness**: Works mobile to desktop
5. **Documentation**: Complete and accurate
6. **Testing**: Adequately tested across environments

**Timeline:**
- Initial review within 1 week
- Feedback provided with specific suggestions
- Approval after all checks pass
- Merge and release

## Project Structure Standards

### Directory Organization

```
free-templates/
├── .context/                    # Documentation as code
│   ├── substrate.md
│   ├── architecture/
│   ├── components/
│   ├── styling/
│   ├── templates/
│   └── guidelines.md
├── agents.md                    # AI agent navigation guide
├── template-name/               # Each template isolated
│   ├── index.html
│   ├── README.md
│   ├── preview.png
│   └── components/
├── README.md                    # Project overview
└── LICENSE
```

### File Naming Conventions

**Templates:**
- Use kebab-case: `dashboard-analytics`, `pricing-page`, `landing-hero`
- Descriptive and concise
- Avoid version numbers in names

**Components:**
- Use kebab-case: `stat-card.html`, `user-dropdown.html`
- Pattern: `[element]-[variant].html`

**Documentation:**
- Lowercase with hyphens: `creation-guide.md`, `responsive-design.md`

## Quality Assurance

### Pre-Submission Checklist

Before submitting template:

**Code Quality:**
- [ ] HTML validates (W3C Validator)
- [ ] No console errors or warnings
- [ ] Consistent code formatting
- [ ] Meaningful comments for complex sections
- [ ] Follows all `.context/` conventions

**Functionality:**
- [ ] All interactive elements work
- [ ] Links functional or clearly marked as placeholders
- [ ] Forms have proper validation (if applicable)
- [ ] Smooth transitions and animations

**Responsiveness:**
- [ ] Tested at 375px (mobile)
- [ ] Tested at 768px (tablet)
- [ ] Tested at 1024px (laptop)
- [ ] Tested at 1440px (desktop)
- [ ] No horizontal scrolling at any size
- [ ] Touch targets adequate (44×44px minimum)

**Accessibility:**
- [ ] Semantic HTML structure
- [ ] All images have alt text
- [ ] Forms have associated labels
- [ ] Color contrast meets WCAG AA (4.5:1)
- [ ] Keyboard navigation complete (Tab, Enter, Escape)
- [ ] Focus indicators visible
- [ ] Screen reader tested (NVDA, JAWS, or VoiceOver)
- [ ] ARIA attributes where appropriate

**Documentation:**
- [ ] README.md complete with features, usage, customization
- [ ] Component files have documentation headers
- [ ] Preview.png created (1200×800px)
- [ ] Customization instructions clear
- [ ] Browser support documented

**Testing:**
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] Mobile Safari (iOS)
- [ ] Chrome Mobile (Android)

## Community Guidelines

### Code of Conduct

**Be respectful:**
- Treat all contributors with respect
- Welcome newcomers warmly
- Provide constructive feedback
- Assume good intentions

**Be collaborative:**
- Share knowledge freely
- Help others learn
- Accept feedback gracefully
- Credit others' contributions

**Be professional:**
- Keep discussions on-topic
- Avoid inflammatory language
- Focus on technical merit
- Resolve conflicts privately

### Getting Help

**Questions about:**

**Using templates:**
- Check template README first
- Review `.context/` documentation
- Open GitHub issue with question

**Contributing:**
- Read this guidelines document
- Review `.context/templates/creation-guide.md`
- Ask in GitHub discussions

**Bugs:**
- Search existing issues first
- Provide clear reproduction steps
- Include browser and device info
- Add screenshots if helpful

## Versioning

### Semantic Versioning

Project follows semantic versioning:

**Major (1.0.0):**
- Breaking changes to existing templates
- Tailwind CSS major version updates
- Significant restructuring

**Minor (0.1.0):**
- New templates added
- New components or features
- Non-breaking enhancements

**Patch (0.0.1):**
- Bug fixes
- Documentation updates
- Minor improvements

### Template Versioning

Individual templates evolve independently:
- Breaking changes noted in template README
- Migration guides provided when needed
- Deprecated templates archived with notice

## Future Roadmap

### Planned Enhancements

**Short term:**
- Additional dashboard templates
- E-commerce components
- Landing page templates
- Form templates

**Medium term:**
- Framework integration examples (React, Vue, Svelte)
- Build process templates
- Animation library integration
- Dark mode across all templates

**Long term:**
- Template builder tool
- Component library site
- Video tutorials
- Community showcase

### Feature Requests

Submit feature requests via GitHub issues:
- Describe use case clearly
- Explain benefit to users
- Suggest implementation approach
- Note any alternative solutions

Feature requests evaluated based on:
- Alignment with project goals
- Broad applicability
- Maintenance burden
- Community interest

## Recognition

### Contributors

All contributors recognized in:
- Repository contributors page
- Release notes for their contributions
- Special recognition for significant contributions

Thank you for helping build a valuable resource for the web development community!
