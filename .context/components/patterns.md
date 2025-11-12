# Component Patterns and Structure

## Component Definition

In this project, a component is a reusable HTML segment with Tailwind styling that encapsulates a specific UI pattern. Unlike framework components, these are pure HTML templates meant for copying and customization.

## Component File Structure

Every component file follows a standardized format with documentation header and implementation:

```html
<!--
  Component Name: Button Primary

  Description: Primary action button with hover and focus states

  Usage Context: Use for main call-to-action buttons in forms, modals, and hero sections

  Customization:
  - Change bg-blue-600 to your brand color
  - Adjust px-6 py-3 for different sizes
  - Modify text-base for font size variations

  Accessibility:
  - Includes focus ring for keyboard navigation
  - Sufficient color contrast (WCAG AA)
  - Works with screen readers without additional markup

  Examples:
  - Submit buttons in forms
  - Primary CTA in hero sections
  - Confirmation actions in modals
-->

<button type="button"
        class="px-6 py-3 bg-blue-600 text-white font-medium rounded-lg
               hover:bg-blue-700 focus:outline-none focus:ring-2
               focus:ring-blue-500 focus:ring-offset-2
               transition-colors duration-200">
  Button Text
</button>
```

### Header Documentation Requirements

Every component must include:

**Component Name**: Clear, descriptive identifier used in filenames and references

**Description**: One-line explanation of purpose and primary use case

**Usage Context**: When and where to use this component appropriately

**Customization**: Specific Tailwind classes users should modify for their needs

**Accessibility**: Key accessibility features and considerations

**Examples**: Concrete use cases demonstrating appropriate usage

## Component Categories

### Layout Components

Structural components that organize content and establish page hierarchy.

**Example: Two-Column Layout**
```html
<!--
  Component Name: Two-Column Layout
  Description: Responsive two-column layout with sidebar and main content
  Usage Context: Dashboard pages, admin interfaces, documentation sites
-->

<div class="flex flex-col lg:flex-row min-h-screen">
  <!-- Sidebar: full width on mobile, fixed width on desktop -->
  <aside class="w-full lg:w-64 bg-gray-900 text-white">
    <div class="p-4">
      <h2 class="text-xl font-semibold mb-4">Navigation</h2>
      <!-- Sidebar content -->
    </div>
  </aside>

  <!-- Main content: flexible width -->
  <main class="flex-1 bg-gray-50 p-6">
    <!-- Page content -->
  </main>
</div>
```

### Navigation Components

Components for site and app navigation including menus, breadcrumbs, and pagination.

**Example: Sidebar Navigation**
```html
<!--
  Component Name: Sidebar Navigation
  Description: Vertical navigation menu with active state and icons
  Usage Context: Application sidebars, dashboard navigation
-->

<nav class="space-y-1" aria-label="Main navigation">
  <!-- Active item -->
  <a href="#"
     class="flex items-center px-4 py-3 text-sm font-medium text-white bg-gray-800 rounded-lg"
     aria-current="page">
    <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
    </svg>
    Dashboard
  </a>

  <!-- Inactive items -->
  <a href="#"
     class="flex items-center px-4 py-3 text-sm font-medium text-gray-300 hover:bg-gray-800 hover:text-white rounded-lg transition-colors">
    <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
    </svg>
    Analytics
  </a>
</nav>
```

### Data Display Components

Components for presenting information including cards, tables, stats, and charts.

**Example: Stat Card**
```html
<!--
  Component Name: Stat Card
  Description: Display key metrics with label, value, and trend indicator
  Usage Context: Dashboard KPIs, analytics overviews, metric summaries
-->

<div class="bg-white rounded-lg shadow p-6">
  <div class="flex items-center justify-between">
    <div class="flex-1">
      <p class="text-sm font-medium text-gray-600">Total Revenue</p>
      <p class="text-3xl font-bold text-gray-900 mt-2">$45,231</p>
    </div>
    <div class="bg-blue-100 rounded-full p-3">
      <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1" />
      </svg>
    </div>
  </div>
  <div class="mt-4 flex items-center text-sm">
    <svg class="w-4 h-4 text-green-500 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18" />
    </svg>
    <span class="text-green-600 font-medium">12.5%</span>
    <span class="text-gray-600 ml-2">vs last month</span>
  </div>
</div>
```

### Form Components

Input components including text fields, selects, checkboxes, and form layouts.

**Example: Input Field**
```html
<!--
  Component Name: Text Input
  Description: Labeled text input with validation states
  Usage Context: Forms, search fields, user input collection
-->

<div class="space-y-1">
  <label for="email" class="block text-sm font-medium text-gray-700">
    Email Address
  </label>
  <input type="email"
         id="email"
         name="email"
         placeholder="you@example.com"
         class="w-full px-4 py-2 border border-gray-300 rounded-lg
                focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent
                placeholder:text-gray-400"
         aria-describedby="email-description">
  <p id="email-description" class="text-sm text-gray-500">
    We'll never share your email with anyone else.
  </p>
</div>

<!-- Error state variation -->
<div class="space-y-1">
  <label for="email-error" class="block text-sm font-medium text-gray-700">
    Email Address
  </label>
  <input type="email"
         id="email-error"
         name="email"
         class="w-full px-4 py-2 border-2 border-red-500 rounded-lg
                focus:outline-none focus:ring-2 focus:ring-red-500"
         aria-invalid="true"
         aria-describedby="email-error-message">
  <p id="email-error-message" class="text-sm text-red-600">
    Please enter a valid email address.
  </p>
</div>
```

### Feedback Components

Components for user feedback including alerts, toasts, modals, and loading states.

**Example: Alert Component**
```html
<!--
  Component Name: Alert
  Description: Informational alert with icon and dismiss button
  Usage Context: Success messages, warnings, errors, informational notices
-->

<!-- Success alert -->
<div class="bg-green-50 border border-green-200 rounded-lg p-4" role="alert">
  <div class="flex items-start">
    <svg class="w-5 h-5 text-green-600 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
    </svg>
    <div class="ml-3 flex-1">
      <h3 class="text-sm font-medium text-green-800">Successfully saved!</h3>
      <p class="text-sm text-green-700 mt-1">Your changes have been saved to the database.</p>
    </div>
    <button type="button" class="ml-3 text-green-600 hover:text-green-800">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
      </svg>
    </button>
  </div>
</div>
```

## Component Extraction Guidelines

### When to Extract

Apply the three-criteria rule:

1. **Reusability**: Component appears in 2+ locations or templates
2. **Complexity**: Component exceeds 50 lines of HTML
3. **Variations**: Multiple versions exist (sizes, colors, states)

### Extraction Process

1. **Identify the component**: Locate repeated or complex HTML segment
2. **Document thoroughly**: Write complete header documentation
3. **Create component file**: Save to `components/component-name.html`
4. **Replace instances**: Reference component in original template
5. **Test variations**: Ensure customization points work as documented

## Component Naming Conventions

Use kebab-case filenames that describe purpose and variant:

- `button-primary.html` - Primary action button
- `card-stat.html` - Statistics card
- `nav-sidebar.html` - Sidebar navigation
- `input-text.html` - Text input field
- `modal-confirm.html` - Confirmation modal

Pattern: `[element]-[variant].html` or `[element]-[purpose].html`

## Component Customization Points

Every component should have clear customization points. Mark these in documentation:

**Color Customization**: Which classes control color scheme
**Size Customization**: Which classes control dimensions
**Content Customization**: Which text/icons to replace
**Behavior Customization**: Which Alpine.js data to modify

This standardized approach ensures components remain discoverable, understandable, and easily customizable across all templates.
