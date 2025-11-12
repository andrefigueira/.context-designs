# Architecture Overview

## Template Organization Pattern

Each template in this repository follows a standardized folder structure that balances isolation with discoverability. This architectural decision ensures templates remain independent while sharing common documentation patterns.

### Standard Template Structure

```
template-name/
├── index.html              # Primary template file
├── README.md              # Template-specific guide
├── preview.png            # Visual reference (1200x800px)
├── components/            # Extracted reusable pieces
│   ├── sidebar.html
│   ├── header.html
│   └── card.html
├── variants/              # Alternative layouts (optional)
│   └── alternative.html
└── examples/              # Integration examples (optional)
    ├── react-example.jsx
    └── vue-example.vue
```

### Why Folder-Per-Template

**Isolation Benefits:**
- Templates never conflict or share dependencies
- Users can download single folders without cloning entire repository
- Testing and validation happens independently per template
- Version control history remains clear for each template's evolution

**Discoverability Benefits:**
- Root directory provides instant template browsing
- Each folder name describes the template purpose clearly
- Preview images enable visual selection before diving into code
- README files offer context without opening HTML

### File Naming Conventions

**Primary Files:**
- `index.html` - Always the main entry point for consistency
- `README.md` - Template documentation following standard structure
- `preview.png` - Screenshot at 1200x800px resolution

**Component Files:**
- Use descriptive kebab-case names: `user-dropdown.html`, `stats-card.html`
- One component per file for maximum reusability
- Self-contained with all necessary Tailwind classes

**Variant Files:**
- Descriptive suffixes indicating differences: `index-dark.html`, `index-compact.html`
- Optional - only when meaningful alternatives exist

## HTML Structure Standards

### Semantic Markup

All templates prioritize semantic HTML5 elements:

```html
<!-- Good: Semantic structure -->
<nav class="bg-white shadow-sm">
  <div class="max-w-7xl mx-auto px-4">
    <ul class="flex space-x-8">
      <li><a href="#" class="text-gray-700 hover:text-gray-900">Dashboard</a></li>
    </ul>
  </div>
</nav>

<!-- Avoid: Generic divs when semantic elements fit -->
<div class="nav-container">
  <div class="nav-items">
    <div class="nav-item">Dashboard</div>
  </div>
</div>
```

**Rationale:** Semantic HTML improves accessibility, SEO, and code maintainability. Screen readers understand structure better, and developers can scan code more efficiently.

### Document Structure

Every template HTML file follows this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Template Name - Free Tailwind Templates</title>

  <!-- Tailwind CSS via CDN for standalone usage -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Optional: Tailwind config for custom theme -->
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            // Custom colors here
          }
        }
      }
    }
  </script>
</head>
<body class="bg-gray-50 antialiased">
  <!-- Template content -->
</body>
</html>
```

**CDN vs Build Process:** Templates use Tailwind CDN for maximum portability. Users integrating into existing projects will naturally replace CDN with their build process.

## Responsive Design Architecture

### Mobile-First Approach

All layouts start with mobile styles, then add complexity at larger breakpoints:

```html
<!-- Mobile-first responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <div class="bg-white p-6 rounded-lg shadow">Card 1</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 2</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 3</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 4</div>
</div>
```

### Breakpoint Strategy

Standard breakpoints align with Tailwind defaults:
- `sm`: 640px - Small tablets
- `md`: 768px - Tablets and small laptops
- `lg`: 1024px - Desktops
- `xl`: 1280px - Large desktops
- `2xl`: 1536px - Extra large screens

**Design Decision:** Use `md` and `lg` breakpoints most frequently. These cover the majority of layout shifts. Reserve `sm` for minor adjustments and `xl`/`2xl` for exceptional cases.

## Component Extraction Strategy

### When to Extract Components

Extract HTML segments to separate files when they meet criteria:

1. **Reusability**: Used in multiple templates or multiple locations within one template
2. **Complexity**: Component exceeds 50 lines and has clear boundaries
3. **Variations**: Multiple versions exist (different states, themes, sizes)

### Component File Format

```html
<!-- components/stat-card.html -->
<!--
  Stat Card Component

  Usage: Display key metrics in dashboard layouts

  Customization:
  - Replace icon SVG with desired icon
  - Modify stat value and label text
  - Adjust colors via Tailwind classes
-->

<div class="bg-white rounded-lg shadow p-6">
  <div class="flex items-center justify-between">
    <div>
      <p class="text-sm font-medium text-gray-600">Total Revenue</p>
      <p class="text-2xl font-semibold text-gray-900 mt-2">$45,231</p>
    </div>
    <div class="bg-blue-100 rounded-full p-3">
      <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1" />
      </svg>
    </div>
  </div>
  <div class="mt-4 flex items-center text-sm">
    <span class="text-green-600 font-medium">+12.5%</span>
    <span class="text-gray-600 ml-2">vs last month</span>
  </div>
</div>
```

**Key Elements:**
- HTML comment header with usage instructions
- Inline customization guidance
- Complete, copy-paste-ready code
- No external dependencies beyond Tailwind

This architecture ensures each template remains self-contained, easily understood, and immediately usable while maintaining consistency across the entire repository.
