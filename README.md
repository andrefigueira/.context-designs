# Free Tailwind Templates

A curated collection of modern, production-ready UI templates built entirely with Tailwind CSS. Inspired by the design excellence of shadcn/ui but implemented in pure Tailwind without dependencies on React or component libraries.

## Built with Claude Code

These templates showcase what you can build when you combine Tailwind CSS with [Claude Code](https://claude.com/claude-code), Anthropic's official CLI assistant. Every template in this collection was created using Claude Code, demonstrating how AI can accelerate UI development without sacrificing quality or control.

### Why Claude Code for UI Development?

**Rapid Prototyping**: Go from concept to working UI in minutes. Describe your vision and Claude Code builds it using Tailwind best practices.

**Design System Consistency**: Claude Code maintains your design patterns and conventions across components automatically.

**Accessibility Built-In**: Get WCAG AA compliant markup from the start, not as an afterthought.

**No Framework Lock-In**: Claude Code excels at pure HTML + Tailwind, giving you maximum portability.

**Learn While You Build**: See how experienced developers structure Tailwind code through real examples.

### How These Templates Were Made

Each template started with a conversation:

```
"Build a modern dashboard with sidebar, stats cards, and charts"
"Create a fintech landing page with hero, features, and CTAs"
```

Claude Code then:
1. Structured semantic HTML with proper accessibility
2. Applied Tailwind utilities following design best practices
3. Added Alpine.js for interactivity where needed
4. Ensured mobile responsiveness from 320px up
5. Created comprehensive documentation

The result? Production-ready code that you can understand, modify, and ship immediately.

### Try It Yourself

Want to create your own templates? Install [Claude Code](https://docs.claude.com/en/docs/claude-code) and try prompts like:

- "Build a pricing page with three tiers and a comparison table"
- "Create a blog layout with card grid and sidebar"
- "Design an e-commerce product page with image gallery"
- "Make a contact form with validation and success states"

Claude Code will handle the boilerplate, maintain consistency, and let you focus on making it uniquely yours.

### Powered by .context

This project uses the [.context methodology](https://github.com/andrefigueira/.context/) for documentation as code. The `.context/` directory contains structured documentation that Claude Code uses to understand project conventions, design patterns, and coding standards.

This approach creates a feedback loop where:
1. You define your design system and conventions in `.context/`
2. Claude Code reads and follows these standards automatically
3. Your codebase maintains consistency across all templates
4. Documentation stays synchronized with implementation

The `.context` folder acts as a substrate for AI collaboration, making Claude Code an extension of your development process rather than just a code generator. Check out the [.context repository](https://github.com/andrefigueira/.context/) to learn how to implement this in your own projects.

## Philosophy

**Pure Tailwind Approach**: No framework lock-in. Use with React, Vue, Svelte, Alpine.js, or vanilla JavaScript.

**Zero Dependencies**: Nothing beyond Tailwind CSS itself (and optional Alpine.js for interactivity).

**Full Control**: Complete visibility into every style and behavior. No abstractions to fight.

**Modern Design**: Clean, minimalist aesthetics following contemporary design principles with proper accessibility.

## Available Templates

### Modern Dashboard
**Path**: `dashboard-modern/`

A professional analytics dashboard featuring:
- Responsive sidebar navigation (collapsible on mobile)
- Stats cards with trend indicators
- Interactive ApexCharts visualizations (area and donut charts)
- Data table with status badges
- User dropdown menu
- Full mobile responsiveness
- WCAG AA accessibility compliance

**Technologies**: Tailwind CSS 3.x, Alpine.js 3.x, ApexCharts

**Use Cases**: SaaS dashboards, admin panels, analytics interfaces, data-heavy applications

[View Template →](dashboard-modern/)

### Fintech Landing Page
**Path**: `landing-page-fintech/`

A sleek, modern marketing landing page designed for fintech and financial services:
- Eye-catching hero section with animated phone mockup
- Sticky navigation with scroll effects
- Stats section for social proof
- Feature grid with hover animations
- Multiple CTA sections
- Smooth animations and transitions
- Full mobile responsiveness
- Modern gradient designs

**Technologies**: Tailwind CSS 3.x, Alpine.js 3.x

**Use Cases**: Fintech startups, banking apps, payment processors, SaaS products, financial services, crypto platforms

[View Template →](landing-page-fintech/)

## Getting Started

### Quick Start

1. **Browse templates** in their respective folders
2. **Open `index.html`** in your browser to preview
3. **Copy the template** to your project
4. **Customize** colors, content, and styling via Tailwind utilities

### Integration

Each template is self-contained and ready to use:

```bash
# Copy template to your project
cp -r dashboard-modern /path/to/your/project

# Open and customize
cd /path/to/your/project
open index.html
```

### Production Use

For production, replace CDN links with proper Tailwind installation:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

Configure `tailwind.config.js` with your content paths and build for production.

## Project Structure

```
free-templates/
├── .context/                    # Documentation as code
│   ├── substrate.md            # Project overview
│   ├── architecture/           # Template organization patterns
│   ├── components/             # Component patterns and standards
│   ├── styling/                # Design system and conventions
│   ├── templates/              # Creation and maintenance guides
│   └── guidelines.md           # Contribution guidelines
├── agents.md                   # AI agent navigation guide
├── dashboard-modern/           # Modern dashboard template
│   ├── index.html
│   ├── README.md
│   ├── preview.png
│   └── components/
├── landing-page-fintech/       # Fintech landing page template
│   ├── index.html
│   ├── README.md
│   └── components/
├── README.md                   # This file
└── LICENSE
```

## Features

- ✅ **Framework Agnostic**: Works with any JavaScript framework or none at all
- ✅ **Mobile-First**: Responsive design from 320px to 4K displays
- ✅ **Accessible**: WCAG 2.1 Level AA compliance minimum
- ✅ **Modern Design**: Contemporary aesthetics following current best practices
- ✅ **Production Ready**: Copy, customize, and deploy
- ✅ **Well Documented**: Comprehensive README and inline documentation
- ✅ **Component Based**: Extracted reusable components in each template
- ✅ **No Build Required**: Uses CDN for instant preview (build process optional)

## Design Principles

### Clarity
Every element serves a purpose with clear visual hierarchy

### Consistency
Patterns repeat predictably across all templates

### Accessibility
WCAG AA compliance is a requirement, not an option

### Performance
Minimal CSS with optimized Tailwind utilities

### Flexibility
Easy customization through Tailwind configuration

## Technology Stack

**Core:**
- Tailwind CSS v3.x (utility-first CSS framework)
- HTML5 (semantic markup)
- CSS3 (custom properties for theming)

**Optional Enhancements:**
- Alpine.js for interactive components
- ApexCharts for data visualization
- Heroicons for icon system

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Documentation

Comprehensive documentation is available in the `.context/` directory:

- **Getting Started**: See `.context/substrate.md` for project overview
- **Creating Templates**: See `.context/templates/creation-guide.md`
- **Component Patterns**: See `.context/components/patterns.md`
- **Styling Conventions**: See `.context/styling/conventions.md`
- **Design System**: See `.context/styling/design-system.md`
- **Contributing**: See `.context/guidelines.md`

## Customization

All templates are built to be easily customized:

### Colors

Update Tailwind configuration in template HTML:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        }
      }
    }
  }
}
```

### Typography

Add custom fonts via Google Fonts or local hosting, then update config:

```javascript
fontFamily: {
  sans: ['Inter', 'system-ui', 'sans-serif']
}
```

### Spacing & Layout

Modify utility classes directly in HTML or extend Tailwind config:

```javascript
spacing: {
  '18': '4.5rem',
  '88': '22rem'
}
```

## Contributing

We welcome contributions! Please see `.context/guidelines.md` for detailed contribution guidelines.

### Quick Contribution Checklist

- [ ] Follow established conventions in `.context/`
- [ ] Ensure WCAG AA accessibility compliance
- [ ] Test across multiple browsers and devices
- [ ] Include comprehensive README
- [ ] Extract reusable components
- [ ] Provide preview screenshot

## Roadmap

### Short Term
- Additional dashboard variations
- E-commerce templates
- Landing page templates
- Form templates

### Medium Term
- Framework integration examples (React, Vue, Svelte)
- Dark mode across all templates
- Animation enhancements
- Component library expansion

### Long Term
- Template builder tool
- Component library website
- Video tutorials
- Community showcase

## License

MIT License - use freely in personal and commercial projects with no attribution required (though always appreciated).

See [LICENSE](LICENSE) file for full details.

## Credits

- **Design Inspiration**: shadcn/ui, Linear, Stripe Dashboard, Vercel
- **Icons**: [Heroicons](https://heroicons.com/)
- **CSS Framework**: [Tailwind CSS](https://tailwindcss.com/)
- **JavaScript**: [Alpine.js](https://alpinejs.dev/)
- **Charts**: [ApexCharts](https://apexcharts.com/)

## Support

- **Documentation**: Review `.context/` files for comprehensive guides
- **Issues**: Report bugs via GitHub issues
- **Questions**: Open a GitHub discussion
- **Contributions**: See contribution guidelines

## Acknowledgments

This project follows the [.context methodology](https://github.com/andrefigueira/.context/) for documentation as code, ensuring living documentation that evolves with the project.

---

**Made with ❤️ for the web development community**

Start building beautiful interfaces today. No dependencies. No complexity. Just pure Tailwind CSS.
