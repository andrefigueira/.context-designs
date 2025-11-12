# Template Creation Guide

## Overview

This guide walks through creating a new template from concept to completion, ensuring consistency with project standards and best practices.

## Pre-Creation Checklist

Before starting a new template, verify:

- [ ] Template concept fills a genuine need not covered by existing templates
- [ ] Design inspiration identified (screenshots, mockups, or references)
- [ ] Target use cases clearly defined
- [ ] Color scheme and branding considerations planned
- [ ] Interactive elements identified (if any)
- [ ] Responsive behavior sketched for mobile, tablet, desktop

## Step 1: Template Planning

### Define Template Scope

Answer these questions:

**What problem does this template solve?**
Example: "Provides a modern analytics dashboard for SaaS applications"

**Who is the target user?**
Example: "Developers building data-heavy applications who need professional UI quickly"

**What are the core components?**
- Sidebar navigation
- Header with user dropdown
- Stats cards grid
- Chart placeholders
- Data table

**What interactivity is required?**
- Mobile menu toggle
- User dropdown menu
- Tab switching between views
- Sortable table headers (optional)

### Create Template Folder

```bash
# Create template directory structure
mkdir -p dashboard-analytics
cd dashboard-analytics

mkdir components
mkdir variants    # Optional: for alternative layouts
mkdir examples    # Optional: for framework integration examples
```

## Step 2: HTML Structure

### Create index.html

Start with semantic HTML structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Modern analytics dashboard template built with Tailwind CSS">
  <title>Analytics Dashboard - Free Tailwind Templates</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Alpine.js for interactivity (if needed) -->
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

  <!-- Tailwind configuration (optional customization) -->
  <script>
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
  </script>

  <!-- x-cloak style -->
  <style>
    [x-cloak] { display: none !important; }
  </style>
</head>
<body class="bg-gray-50 antialiased">
  <!-- Template content -->
</body>
</html>
```

### Build Layout Structure

Follow mobile-first responsive patterns:

```html
<body class="bg-gray-50 antialiased">
  <div x-data="{ sidebarOpen: false, userMenuOpen: false }" class="min-h-screen">

    <!-- Sidebar -->
    <aside class="fixed inset-y-0 left-0 w-64 bg-gray-900 text-white transform transition-transform duration-300 lg:translate-x-0 z-30"
           :class="sidebarOpen ? 'translate-x-0' : '-translate-x-full'">
      <!-- Sidebar content -->
    </aside>

    <!-- Main content area -->
    <div class="lg:ml-64">
      <!-- Header -->
      <header class="bg-white shadow-sm border-b border-gray-200">
        <!-- Header content -->
      </header>

      <!-- Page content -->
      <main class="p-4 md:p-6 lg:p-8">
        <!-- Main content -->
      </main>
    </div>

  </div>
</body>
```

## Step 3: Styling with Tailwind

### Apply Design System Standards

Follow established conventions from `.context/styling/`:

**Colors:**
```html
<!-- Backgrounds -->
<div class="bg-white">Cards and surfaces</div>
<div class="bg-gray-50">Page background</div>
<div class="bg-gray-900">Dark surfaces (sidebar)</div>

<!-- Text -->
<h1 class="text-gray-900">Primary headings</h1>
<p class="text-gray-700">Body text</p>
<p class="text-gray-600">Secondary text</p>
```

**Spacing:**
```html
<!-- Card spacing -->
<div class="p-6 space-y-4">
  <!-- Content with 1rem padding, 1rem vertical spacing -->
</div>

<!-- Section spacing -->
<div class="space-y-6 md:space-y-8">
  <!-- Sections with responsive spacing -->
</div>
```

**Typography:**
```html
<h1 class="text-2xl md:text-3xl font-bold text-gray-900">Page Title</h1>
<h2 class="text-xl md:text-2xl font-semibold text-gray-900">Section Heading</h2>
<p class="text-base text-gray-700">Body text</p>
```

### Implement Responsive Design

Test at multiple breakpoints:

```html
<!-- Responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-6">
  <!-- Cards adapt from stacked → 2 cols → 4 cols -->
</div>

<!-- Responsive padding -->
<main class="p-4 md:p-6 lg:p-8">
  <!-- Padding increases with screen size -->
</main>

<!-- Hide/show at breakpoints -->
<button class="lg:hidden">Mobile menu</button>
<nav class="hidden lg:block">Desktop nav</nav>
```

## Step 4: Add Interactivity

### Implement Interactive Components

Use Alpine.js for dynamic behavior:

```html
<!-- Dropdown menu -->
<div x-data="{ open: false }" class="relative">
  <button @click="open = !open" class="flex items-center">
    User Menu
  </button>

  <div x-show="open"
       @click.outside="open = false"
       x-transition
       class="absolute right-0 mt-2 w-48 bg-white rounded-lg shadow-lg">
    <a href="#" class="block px-4 py-2 hover:bg-gray-100">Profile</a>
    <a href="#" class="block px-4 py-2 hover:bg-gray-100">Settings</a>
  </div>
</div>

<!-- Mobile menu toggle -->
<div x-data="{ mobileMenuOpen: false }">
  <button @click="mobileMenuOpen = !mobileMenuOpen" class="lg:hidden">
    Toggle Menu
  </button>

  <nav x-show="mobileMenuOpen" x-transition>
    <!-- Mobile navigation -->
  </nav>
</div>
```

## Step 5: Accessibility Implementation

### Ensure WCAG Compliance

Reference `.context/components/accessibility.md` for patterns:

**Semantic HTML:**
```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="#dashboard">Dashboard</a></li>
  </ul>
</nav>

<main id="main-content">
  <h1>Page Title</h1>
</main>
```

**Keyboard Navigation:**
```html
<button class="focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
  Accessible Button
</button>
```

**ARIA Attributes:**
```html
<button aria-haspopup="true" :aria-expanded="menuOpen">
  Menu
</button>

<div role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">Modal Title</h2>
</div>
```

**Color Contrast:**
Verify all text meets 4.5:1 contrast ratio minimum using browser DevTools.

## Step 6: Component Extraction

### Identify Reusable Components

Extract components that meet criteria:
- Used in multiple locations
- Exceed 50 lines of HTML
- Have multiple variations

**Example: Extract stat card**

Create `components/stat-card.html`:
```html
<!--
  Component Name: Stat Card
  Description: Display key metrics with icon and trend indicator
  Usage Context: Dashboard KPIs and analytics summaries

  Customization:
  - Replace icon SVG path
  - Update stat value and label
  - Change trend indicator color and value

  Accessibility:
  - Semantic structure with proper heading hierarchy
  - Sufficient color contrast for all text
-->

<div class="bg-white rounded-lg shadow p-6">
  <div class="flex items-center justify-between">
    <div>
      <p class="text-sm font-medium text-gray-600">[LABEL]</p>
      <p class="text-3xl font-bold text-gray-900 mt-2">[VALUE]</p>
    </div>
    <div class="bg-blue-100 rounded-full p-3">
      <!-- [ICON SVG] -->
    </div>
  </div>
  <div class="mt-4 flex items-center text-sm">
    <span class="text-green-600 font-medium">[TREND]</span>
    <span class="text-gray-600 ml-2">[TREND_LABEL]</span>
  </div>
</div>
```

Reference component in main template with HTML comment:
```html
<!-- See components/stat-card.html -->
<!-- Replace [LABEL], [VALUE], [ICON SVG], [TREND], [TREND_LABEL] -->
```

## Step 7: Documentation

### Create README.md

```markdown
# Analytics Dashboard Template

Modern analytics dashboard built with Tailwind CSS featuring sidebar navigation, stats cards, data visualization placeholders, and responsive design.

## Features

- Responsive sidebar navigation (collapsible on mobile)
- Header with user dropdown menu
- Stats cards grid with icons and trend indicators
- Chart placeholders for data visualization
- Data table with sortable headers
- Fully responsive mobile-first design
- Dark mode support (optional)

## Usage

1. Copy `index.html` to your project
2. Ensure Tailwind CSS is installed (uses CDN by default)
3. Customize colors in Tailwind config section
4. Replace placeholder content with your data
5. Add chart library of choice (Chart.js, ApexCharts, etc.)

## Customization

### Colors

Modify the Tailwind config in `<script>` tag:

\`\`\`javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: {
          // Your brand colors here
        }
      }
    }
  }
}
\`\`\`

### Layout

- Sidebar width: Modify `w-64` class on sidebar element
- Card spacing: Adjust `gap-4` on grid containers
- Padding: Change `p-6` on cards and containers

## Components

Reusable components are extracted to `/components` folder:
- `stat-card.html` - KPI card with icon and trend
- `chart-container.html` - Chart placeholder card
- `data-table.html` - Sortable data table

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

MIT License - use freely in personal and commercial projects.
```

### Create Preview Image

Take screenshot at 1200×800px resolution showing:
- Full layout visible
- Representative of actual use case
- Good lighting/contrast
- Save as `preview.png`

## Step 8: Testing

### Testing Checklist

- [ ] **Responsive**: Test mobile (375px), tablet (768px), desktop (1440px)
- [ ] **Browsers**: Test Chrome, Firefox, Safari, Edge
- [ ] **Accessibility**: Screen reader tested (VoiceOver, NVDA)
- [ ] **Keyboard navigation**: All interactive elements accessible via Tab
- [ ] **Color contrast**: WCAG AA compliant (use DevTools checker)
- [ ] **Performance**: Page loads quickly on slow connections
- [ ] **Print**: Template prints reasonably (if applicable)

### Validation

- [ ] HTML validates (W3C Validator)
- [ ] No console errors
- [ ] All links functional (or marked as placeholders)
- [ ] Images have alt text
- [ ] Forms have associated labels

## Step 9: Final Review

Before committing template:

- [ ] Code formatted consistently
- [ ] Comments added for complex sections
- [ ] README.md complete and accurate
- [ ] Preview image created
- [ ] Components documented with headers
- [ ] Follows all conventions in `.context/styling/`
- [ ] Accessibility standards met
- [ ] Tested across breakpoints and browsers

## Step 10: Integration

Add template to repository:

```bash
# From template directory
git add .
git commit -m "Add analytics dashboard template

- Responsive sidebar navigation
- Stats cards with trend indicators
- Chart placeholders
- Data table
- Mobile-first responsive design"
```

Update root README.md to include new template in list of available templates.

## Tips for Success

1. **Start simple**: Build core layout first, add complexity gradually
2. **Test early**: Check responsive behavior throughout development
3. **Reference existing templates**: Learn from established patterns
4. **Focus on accessibility**: Build it in from the start, not as an afterthought
5. **Document as you go**: Write README sections while features are fresh
6. **Use design system**: Follow established color, spacing, and typography standards
7. **Extract components wisely**: Only extract when reusability is clear

Following this guide ensures your template integrates seamlessly with the project and provides maximum value to users.
