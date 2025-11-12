# Tailwind CSS Conventions and Standards

## Utility Class Organization

Organize Tailwind utility classes in a consistent order for readability and maintainability. This convention mirrors how CSS properties are typically organized: layout, spacing, sizing, typography, visual effects, and interactions.

### Recommended Class Order

```html
<div class="
  <!-- 1. Layout & Position -->
  relative flex items-center justify-between

  <!-- 2. Display & Spacing -->
  px-6 py-4 space-x-4

  <!-- 3. Sizing -->
  w-full max-w-4xl h-auto

  <!-- 4. Typography -->
  text-base font-medium text-gray-900

  <!-- 5. Visual (background, border, shadow) -->
  bg-white border border-gray-200 rounded-lg shadow-sm

  <!-- 6. Interactive states (hover, focus, active) -->
  hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-blue-500

  <!-- 7. Transitions & animations -->
  transition-colors duration-200
">
  Content
</div>
```

**Rationale**: Consistent ordering makes scanning and modifying classes easier. Layout properties at the start establish structure, with visual and interactive properties following naturally.

### Multi-Line for Complex Components

For components with many utilities, use multi-line formatting:

```html
<button class="
  flex items-center justify-center
  px-6 py-3 space-x-2
  w-full sm:w-auto
  text-base font-semibold text-white
  bg-blue-600 border border-transparent rounded-lg shadow-md
  hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
  active:bg-blue-800
  disabled:opacity-50 disabled:cursor-not-allowed
  transition-all duration-200
">
  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
  </svg>
  <span>Add Item</span>
</button>
```

## Responsive Design Conventions

### Mobile-First Breakpoints

Always write mobile styles first, then add larger breakpoint modifications:

```html
<!-- Good: Mobile-first approach -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <!-- Single column mobile, 2 cols tablet, 4 cols desktop -->
</div>

<!-- Avoid: Desktop-first approach -->
<!-- This is less maintainable and conflicts with Tailwind philosophy -->
```

### Breakpoint Usage Strategy

Use breakpoints judiciously. Common patterns:

```html
<!-- Layout shifts -->
<aside class="w-full lg:w-64">Sidebar</aside>

<!-- Typography scaling -->
<h1 class="text-2xl md:text-3xl lg:text-4xl font-bold">Title</h1>

<!-- Spacing adjustments -->
<div class="p-4 md:p-6 lg:p-8">Content</div>

<!-- Visibility toggles -->
<button class="block lg:hidden">Mobile Menu</button>
<nav class="hidden lg:block">Desktop Nav</nav>
```

**Standard breakpoints:**
- `sm`: 640px (small tablets)
- `md`: 768px (tablets, primary breakpoint)
- `lg`: 1024px (desktops, primary breakpoint)
- `xl`: 1280px (large desktops)
- `2xl`: 1536px (extra large, rare usage)

**Convention**: Use `md` and `lg` for most responsive changes. Reserve `sm`, `xl`, and `2xl` for edge cases.

## Color System Conventions

### Semantic Color Usage

Use colors semantically and consistently across templates:

```html
<!-- Text colors -->
<h1 class="text-gray-900">Primary heading (darkest)</h1>
<p class="text-gray-700">Body text (readable)</p>
<p class="text-gray-600">Secondary text</p>
<p class="text-gray-500">Tertiary text (muted)</p>
<p class="text-gray-400">Placeholder text (subtle)</p>

<!-- Background colors -->
<div class="bg-white">Pure white surface</div>
<div class="bg-gray-50">Subtle gray background</div>
<div class="bg-gray-100">Light gray section</div>

<!-- Brand/Action colors -->
<button class="bg-blue-600 text-white">Primary action</button>
<button class="bg-gray-200 text-gray-800">Secondary action</button>

<!-- Status colors -->
<div class="bg-green-100 text-green-800">Success message</div>
<div class="bg-yellow-100 text-yellow-800">Warning message</div>
<div class="bg-red-100 text-red-800">Error message</div>
<div class="bg-blue-100 text-blue-800">Info message</div>
```

### Color Shade Guidelines

**50-200**: Backgrounds for alerts, badges, and subtle surfaces
**300-400**: Borders, icons, and disabled states
**500-600**: Primary buttons and active states (brand colors)
**700-800**: Hover states and emphasized text
**900**: Darkest text and high-contrast elements

### Color Contrast Requirements

Ensure WCAG AA compliance:

```html
<!-- Good contrast examples -->
<div class="bg-white text-gray-900">20:1 contrast</div>
<div class="bg-gray-50 text-gray-800">10.5:1 contrast</div>
<div class="bg-blue-600 text-white">8.6:1 contrast</div>

<!-- Insufficient contrast - avoid -->
<!-- bg-gray-100 text-gray-400: Only 2.8:1 -->
<!-- bg-blue-500 text-blue-200: Only 2.1:1 -->
```

## Spacing Conventions

### Consistent Spacing Scale

Use Tailwind's spacing scale consistently:

```html
<!-- Tight spacing (form elements, inline components) -->
<div class="space-y-1">...</div>  <!-- 0.25rem / 4px -->
<div class="space-y-2">...</div>  <!-- 0.5rem / 8px -->

<!-- Comfortable spacing (cards, sections) -->
<div class="space-y-4">...</div>  <!-- 1rem / 16px -->
<div class="space-y-6">...</div>  <!-- 1.5rem / 24px -->

<!-- Loose spacing (page sections, major divisions) -->
<div class="space-y-8">...</div>  <!-- 2rem / 32px -->
<div class="space-y-12">...</div> <!-- 3rem / 48px -->
```

### Padding Conventions

```html
<!-- Buttons -->
<button class="px-4 py-2">Small button</button>
<button class="px-6 py-3">Medium button (default)</button>
<button class="px-8 py-4">Large button</button>

<!-- Cards and containers -->
<div class="p-4">Compact card</div>
<div class="p-6">Standard card (default)</div>
<div class="p-8">Spacious card</div>

<!-- Page-level padding -->
<main class="px-4 md:px-6 lg:px-8">Responsive padding</main>
```

## Typography Conventions

### Font Size Hierarchy

```html
<!-- Headings -->
<h1 class="text-4xl md:text-5xl font-bold">Page title</h1>
<h2 class="text-3xl md:text-4xl font-bold">Section heading</h2>
<h3 class="text-2xl md:text-3xl font-semibold">Subsection</h3>
<h4 class="text-xl font-semibold">Minor heading</h4>
<h5 class="text-lg font-semibold">Small heading</h5>

<!-- Body text -->
<p class="text-base">Default body text (16px)</p>
<p class="text-sm">Smaller text (14px) for captions, helper text</p>
<p class="text-xs">Tiny text (12px) for labels, metadata</p>

<!-- Large text -->
<p class="text-lg">Slightly larger for emphasis</p>
<p class="text-xl">Lead paragraphs</p>
```

### Font Weight Conventions

```html
<p class="font-normal">Regular text (400)</p>
<p class="font-medium">Medium emphasis (500) - buttons, labels</p>
<p class="font-semibold">Strong emphasis (600) - headings, important text</p>
<p class="font-bold">Bold text (700) - primary headings</p>
```

**Convention**: Use `font-medium` for buttons and interactive elements, `font-semibold` for most headings, `font-bold` for page-level headings only.

### Line Height

```html
<!-- Tight for headings -->
<h1 class="text-4xl font-bold leading-tight">Heading</h1>

<!-- Normal for body text (default, can omit) -->
<p class="text-base leading-normal">Body text</p>

<!-- Relaxed for better readability in long content -->
<article class="text-base leading-relaxed">Long article text...</article>
```

## Border and Shadow Conventions

### Border Styles

```html
<!-- Standard borders -->
<div class="border border-gray-200">Subtle border</div>
<div class="border-2 border-gray-300">Emphasized border</div>

<!-- Directional borders -->
<div class="border-t border-gray-200">Top border only</div>
<div class="border-b border-gray-200">Bottom border (dividers)</div>

<!-- Focus borders -->
<input class="border border-gray-300 focus:border-blue-500">
```

### Shadow Styles

```html
<!-- Cards and surfaces -->
<div class="shadow-sm">Subtle shadow (borders alternative)</div>
<div class="shadow">Default card shadow</div>
<div class="shadow-md">Elevated card</div>
<div class="shadow-lg">Modal or prominent element</div>
<div class="shadow-xl">High elevation (rare)</div>

<!-- Focus shadows -->
<button class="focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
  Focus ring
</button>
```

## Naming Patterns for Custom Configurations

When extending Tailwind config, use semantic naming:

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        },
        success: colors.green,
        danger: colors.red,
        warning: colors.yellow
      },
      spacing: {
        '18': '4.5rem',  // Custom spacing if needed
        '88': '22rem'
      }
    }
  }
}
```

## State Variant Conventions

### Interactive States Order

Always order state variants consistently:

```html
<button class="
  bg-blue-600 text-white
  hover:bg-blue-700
  focus:outline-none focus:ring-2 focus:ring-blue-500
  active:bg-blue-800
  disabled:opacity-50 disabled:cursor-not-allowed
">
  Button
</button>
```

**Order**: default → hover → focus → active → disabled

### Group Hover Pattern

```html
<a href="#" class="group">
  <div class="bg-white group-hover:bg-gray-50">
    <h3 class="text-gray-900 group-hover:text-blue-600">Hover changes child</h3>
  </div>
</a>
```

## Comments for Complex Classes

Add HTML comments for complex or non-obvious class combinations:

```html
<!-- Custom scrollbar styling via arbitrary values -->
<div class="overflow-y-auto [&::-webkit-scrollbar]:w-2 [&::-webkit-scrollbar-thumb]:bg-gray-300">
  Content
</div>

<!-- Specific z-index for layering context -->
<div class="fixed inset-0 z-50"><!-- Above sidebar (z-40) but below notifications (z-60) -->
  Modal
</div>
```

These conventions ensure templates remain consistent, readable, and maintainable across the entire project.
