# Design System Standards

## Design Philosophy

This design system establishes consistent visual language across all templates, inspired by modern UI patterns from shadcn/ui, Linear, and Vercel while remaining pure Tailwind CSS implementations.

### Core Principles

**Clarity**: Every element serves a purpose with clear visual hierarchy
**Consistency**: Patterns repeat predictably across templates
**Accessibility**: WCAG AA compliance minimum for all components
**Performance**: Minimal CSS with optimized Tailwind utilities
**Flexibility**: Easy customization through configuration

## Color Palette

### Neutral Colors

Gray scale forms the foundation of the design system:

```html
<!-- Backgrounds -->
<div class="bg-white">Pure white surfaces (cards, modals)</div>
<div class="bg-gray-50">Subtle backgrounds (page background, sections)</div>
<div class="bg-gray-100">Elevated backgrounds (sidebars, headers)</div>
<div class="bg-gray-900">Dark surfaces (navigation, footers)</div>

<!-- Text -->
<p class="text-gray-900">Primary text (headings, important content)</p>
<p class="text-gray-700">Body text (standard readability)</p>
<p class="text-gray-600">Secondary text (descriptions, metadata)</p>
<p class="text-gray-500">Tertiary text (timestamps, subtle labels)</p>
<p class="text-gray-400">Placeholder text (input placeholders, disabled)</p>

<!-- Borders -->
<div class="border-gray-200">Standard borders (cards, inputs)</div>
<div class="border-gray-300">Emphasized borders (focus states)</div>
```

### Brand Colors

Primary color for actions and emphasis:

```html
<!-- Default: Blue (customize via Tailwind config) -->
<button class="bg-blue-600 hover:bg-blue-700 text-white">Primary Action</button>
<a href="#" class="text-blue-600 hover:text-blue-700">Primary Link</a>
<div class="bg-blue-50 text-blue-900 border border-blue-200">Info badge</div>
```

**Shade usage:**
- 50-100: Light backgrounds for badges, alerts
- 500-600: Primary buttons, active states
- 700-800: Hover states, emphasized text

### Semantic Colors

Status and feedback colors:

```html
<!-- Success (Green) -->
<div class="bg-green-50 text-green-800 border border-green-200">
  Success message
</div>

<!-- Warning (Yellow/Amber) -->
<div class="bg-yellow-50 text-yellow-800 border border-yellow-200">
  Warning message
</div>

<!-- Error (Red) -->
<div class="bg-red-50 text-red-800 border border-red-200">
  Error message
</div>

<!-- Info (Blue) -->
<div class="bg-blue-50 text-blue-800 border border-blue-200">
  Informational message
</div>
```

## Typography System

### Font Family

Default: System font stack for optimal performance

```css
font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
```

**Optional enhancement:** Inter, Public Sans, or custom brand fonts

### Type Scale

```html
<!-- Display headings (hero sections) -->
<h1 class="text-5xl md:text-6xl font-bold">Display Large</h1>
<h1 class="text-4xl md:text-5xl font-bold">Display Medium</h1>

<!-- Page headings -->
<h1 class="text-3xl md:text-4xl font-bold">Heading 1</h1>
<h2 class="text-2xl md:text-3xl font-semibold">Heading 2</h2>
<h3 class="text-xl md:text-2xl font-semibold">Heading 3</h3>
<h4 class="text-lg font-semibold">Heading 4</h4>
<h5 class="text-base font-semibold">Heading 5</h5>

<!-- Body text -->
<p class="text-lg">Lead paragraph (large)</p>
<p class="text-base">Body text (default 16px)</p>
<p class="text-sm">Small text (14px)</p>
<p class="text-xs">Tiny text (12px)</p>
```

### Font Weights

```html
<p class="font-normal">Regular (400) - Body text</p>
<p class="font-medium">Medium (500) - Emphasis, buttons, labels</p>
<p class="font-semibold">Semibold (600) - Headings, important text</p>
<p class="font-bold">Bold (700) - Major headings only</p>
```

**Standard usage:**
- Body text: `font-normal`
- Buttons/labels: `font-medium`
- Subheadings: `font-semibold`
- Main headings: `font-bold`

### Line Height

```html
<h1 class="leading-tight">Tight (1.25) - Large headings</h1>
<p class="leading-normal">Normal (1.5) - Body text default</p>
<p class="leading-relaxed">Relaxed (1.625) - Long-form content</p>
```

## Spacing System

### Spacing Scale

Use consistent spacing units based on 4px grid:

```
0    = 0px
0.5  = 2px   (tight spacing)
1    = 4px   (minimal gaps)
2    = 8px   (compact spacing)
3    = 12px  (comfortable gaps)
4    = 16px  (standard spacing) ← Most common
5    = 20px
6    = 24px  (comfortable spacing)
8    = 32px  (section spacing)
10   = 40px
12   = 48px  (major sections)
16   = 64px  (page sections)
20   = 80px
24   = 96px  (hero sections)
```

### Spacing Patterns

**Component internal spacing:**
```html
<!-- Buttons -->
<button class="px-4 py-2">Small button</button>
<button class="px-6 py-3">Medium button (default)</button>
<button class="px-8 py-4">Large button</button>

<!-- Cards -->
<div class="p-4">Compact card</div>
<div class="p-6">Standard card (default)</div>
<div class="p-8">Spacious card</div>
```

**Vertical spacing (stack elements):**
```html
<div class="space-y-2">Tight list (form fields)</div>
<div class="space-y-4">Standard spacing (cards, sections)</div>
<div class="space-y-6">Comfortable spacing (content blocks)</div>
<div class="space-y-8">Generous spacing (page sections)</div>
```

**Horizontal spacing:**
```html
<div class="space-x-2">Compact inline (badges)</div>
<div class="space-x-4">Standard inline (nav items, buttons)</div>
<div class="space-x-6">Spacious inline (navigation)</div>
```

## Border Radius

Consistent rounding across components:

```html
<div class="rounded-none">No rounding (0px)</div>
<div class="rounded-sm">Subtle (2px) - rare</div>
<div class="rounded">Small (4px) - badges, small elements</div>
<div class="rounded-md">Medium (6px) - inputs, buttons</div>
<div class="rounded-lg">Large (8px) - cards, modals (most common)</div>
<div class="rounded-xl">Extra large (12px) - prominent cards</div>
<div class="rounded-2xl">2XL (16px) - hero sections</div>
<div class="rounded-full">Pill shape - avatars, status dots</div>
```

**Standard usage:**
- Inputs/buttons: `rounded-md` or `rounded-lg`
- Cards: `rounded-lg` or `rounded-xl`
- Badges: `rounded` or `rounded-full`
- Avatars: `rounded-full`

## Shadow System

Elevation through shadows:

```html
<!-- Subtle borders alternative -->
<div class="shadow-sm">Very subtle (border replacement)</div>

<!-- Standard elevations -->
<div class="shadow">Small elevation (cards, dropdowns)</div>
<div class="shadow-md">Medium elevation (elevated cards)</div>
<div class="shadow-lg">Large elevation (modals, popovers)</div>
<div class="shadow-xl">Extra large (prominent modals)</div>
<div class="shadow-2xl">Maximum elevation (rare)</div>

<!-- Focus rings -->
<input class="focus:ring-2 focus:ring-blue-500 focus:ring-offset-2" />
```

**Standard usage:**
- Cards: `shadow` or `shadow-md`
- Dropdowns: `shadow-lg`
- Modals: `shadow-lg` or `shadow-xl`
- Focus states: `ring-2 ring-blue-500`

## Button Styles

### Primary Button

```html
<button class="px-6 py-3 bg-blue-600 text-white font-medium rounded-lg
               hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
               active:bg-blue-800 disabled:opacity-50 disabled:cursor-not-allowed
               transition-colors duration-200">
  Primary Action
</button>
```

### Secondary Button

```html
<button class="px-6 py-3 bg-gray-200 text-gray-900 font-medium rounded-lg
               hover:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
               transition-colors duration-200">
  Secondary Action
</button>
```

### Outline Button

```html
<button class="px-6 py-3 bg-white text-gray-700 font-medium rounded-lg border border-gray-300
               hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
               transition-colors duration-200">
  Outline Button
</button>
```

### Ghost Button

```html
<button class="px-6 py-3 text-gray-700 font-medium rounded-lg
               hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-400
               transition-colors duration-200">
  Ghost Button
</button>
```

### Danger Button

```html
<button class="px-6 py-3 bg-red-600 text-white font-medium rounded-lg
               hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2
               transition-colors duration-200">
  Delete
</button>
```

## Input Styles

### Text Input

```html
<input type="text"
       class="w-full px-4 py-2 border border-gray-300 rounded-lg
              focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent
              placeholder:text-gray-400"
       placeholder="Enter text..." />
```

### Input with Error

```html
<input type="text"
       class="w-full px-4 py-2 border-2 border-red-500 rounded-lg
              focus:outline-none focus:ring-2 focus:ring-red-500"
       aria-invalid="true" />
```

### Select Dropdown

```html
<select class="w-full px-4 py-2 border border-gray-300 rounded-lg
               focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
  <option>Option 1</option>
  <option>Option 2</option>
</select>
```

## Card Styles

### Standard Card

```html
<div class="bg-white rounded-lg shadow-md border border-gray-200 overflow-hidden">
  <div class="p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-2">Card Title</h3>
    <p class="text-gray-600">Card content goes here.</p>
  </div>
</div>
```

### Interactive Card

```html
<a href="#" class="block bg-white rounded-lg shadow-md border border-gray-200 overflow-hidden
                    hover:shadow-lg hover:border-gray-300 transition-all duration-200">
  <div class="p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-2">Clickable Card</h3>
    <p class="text-gray-600">Card content goes here.</p>
  </div>
</a>
```

## Badge Styles

```html
<!-- Default badge -->
<span class="px-3 py-1 bg-gray-100 text-gray-800 text-sm font-medium rounded-full">
  Default
</span>

<!-- Primary badge -->
<span class="px-3 py-1 bg-blue-100 text-blue-800 text-sm font-medium rounded-full">
  Primary
</span>

<!-- Success badge -->
<span class="px-3 py-1 bg-green-100 text-green-800 text-sm font-medium rounded-full">
  Success
</span>

<!-- Pill badge with dot -->
<span class="inline-flex items-center px-3 py-1 bg-green-100 text-green-800 text-sm font-medium rounded-full">
  <span class="w-2 h-2 bg-green-500 rounded-full mr-2"></span>
  Active
</span>
```

## Transitions and Animations

Standard transition durations:

```html
<!-- Quick interactions (hover, focus) -->
<button class="transition-colors duration-200">Fast transition</button>

<!-- Modal/dropdown enter/exit -->
<div class="transition-all duration-300">Medium transition</div>

<!-- Page transitions or complex animations -->
<div class="transition-all duration-500">Slow transition</div>
```

**Common transition properties:**
- `transition-colors`: Background and text color changes
- `transition-all`: Multiple properties simultaneously
- `transition-transform`: Movement and scaling
- `transition-opacity`: Fade in/out effects

This design system ensures visual consistency while providing flexibility for customization across all templates.
