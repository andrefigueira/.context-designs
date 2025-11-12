# Accessibility Patterns

## Accessibility Philosophy

Every template and component in this repository must meet WCAG 2.1 Level AA standards minimum. Accessibility is not optional or a later consideration, it is a fundamental requirement from the first line of code.

## Core Principles

### 1. Semantic HTML First

Always use appropriate semantic elements before adding ARIA attributes. Semantic HTML provides built-in accessibility features that ARIA can only approximate.

**Good: Semantic button**
```html
<button type="button" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
  Submit Form
</button>
```

**Avoid: Div styled as button**
```html
<!-- Requires extensive ARIA, keyboard handling, and focus management -->
<div role="button" tabindex="0" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
  Submit Form
</div>
```

**Rationale**: Native `<button>` elements provide keyboard navigation, focus management, and screen reader support automatically. Recreating this with ARIA is error-prone and creates maintenance burden.

### 2. Keyboard Navigation

All interactive elements must be fully usable via keyboard alone. This serves users with motor disabilities, power users, and anyone unable to use a mouse.

**Navigation pattern example:**
```html
<nav aria-label="Main navigation">
  <ul class="flex space-x-4">
    <li>
      <a href="#dashboard"
         class="px-3 py-2 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
        Dashboard
      </a>
    </li>
    <li>
      <a href="#settings"
         class="px-3 py-2 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
        Settings
      </a>
    </li>
  </ul>
</nav>
```

**Key elements:**
- `focus:ring-2` provides visible focus indicator
- `focus:outline-none` removes default outline (replaced with custom ring)
- Links are natively keyboard accessible with Tab key
- Enter activates links

### 3. Color Contrast

All text must meet WCAG AA contrast ratios:
- Normal text (< 18pt): 4.5:1 minimum
- Large text (≥ 18pt or 14pt bold): 3:1 minimum

**Tailwind classes with good contrast:**

```html
<!-- Light backgrounds -->
<div class="bg-white text-gray-900">Excellent contrast (20:1)</div>
<div class="bg-gray-50 text-gray-800">Great contrast (10.5:1)</div>
<div class="bg-blue-50 text-blue-900">Good contrast (8.7:1)</div>

<!-- Dark backgrounds -->
<div class="bg-gray-900 text-white">Excellent contrast (20:1)</div>
<div class="bg-blue-900 text-blue-50">Good contrast (9.2:1)</div>

<!-- Avoid low contrast combinations -->
<!-- ❌ Bad: bg-gray-100 text-gray-400 (2.8:1) -->
<!-- ❌ Bad: bg-blue-500 text-blue-200 (2.1:1) -->
```

**Testing**: Use browser DevTools contrast checker or online tools like WebAIM Contrast Checker.

## ARIA Patterns

### When to Use ARIA

ARIA (Accessible Rich Internet Applications) attributes enhance accessibility when semantic HTML is insufficient. Follow the first rule of ARIA: "Don't use ARIA if you can use native HTML."

### Common ARIA Patterns

**Dropdown Menu:**
```html
<div x-data="{ open: false }" class="relative">
  <button @click="open = !open"
          aria-haspopup="true"
          :aria-expanded="open"
          class="px-4 py-2 bg-white border rounded-lg">
    Options
  </button>

  <div x-show="open"
       role="menu"
       aria-orientation="vertical"
       class="absolute mt-2 bg-white border rounded-lg shadow-lg">
    <a href="#" role="menuitem" class="block px-4 py-2 hover:bg-gray-100">
      Edit Profile
    </a>
    <a href="#" role="menuitem" class="block px-4 py-2 hover:bg-gray-100">
      Settings
    </a>
  </div>
</div>
```

**Key ARIA attributes:**
- `aria-haspopup="true"` - Indicates button opens a menu
- `aria-expanded` - Dynamically shows menu state
- `role="menu"` and `role="menuitem"` - Defines menu structure
- `aria-orientation="vertical"` - Indicates menu layout

**Modal Dialog:**
```html
<div x-data="{ modalOpen: false }">
  <button @click="modalOpen = true"
          aria-haspopup="dialog"
          class="px-4 py-2 bg-blue-600 text-white rounded-lg">
    Open Modal
  </button>

  <div x-show="modalOpen"
       x-trap.noscroll="modalOpen"
       @keydown.escape.window="modalOpen = false"
       role="dialog"
       aria-modal="true"
       aria-labelledby="modal-title"
       class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-lg p-6 max-w-md">
      <h2 id="modal-title" class="text-xl font-semibold mb-4">
        Confirm Action
      </h2>
      <p class="text-gray-600 mb-6">
        Are you sure you want to proceed with this action?
      </p>
      <div class="flex justify-end space-x-3">
        <button @click="modalOpen = false"
                class="px-4 py-2 bg-gray-200 rounded-lg">
          Cancel
        </button>
        <button class="px-4 py-2 bg-blue-600 text-white rounded-lg">
          Confirm
        </button>
      </div>
    </div>
  </div>
</div>
```

**Accessibility features:**
- `role="dialog"` - Identifies modal dialog
- `aria-modal="true"` - Informs screen readers modal is modal
- `aria-labelledby` - Associates dialog with its title
- `x-trap` - Traps keyboard focus within modal
- `@keydown.escape` - Closes modal with Escape key

### Tab Component

```html
<div x-data="{ activeTab: 'overview' }">
  <div role="tablist" aria-label="Dashboard sections" class="flex border-b">
    <button @click="activeTab = 'overview'"
            role="tab"
            :aria-selected="activeTab === 'overview'"
            :tabindex="activeTab === 'overview' ? 0 : -1"
            class="px-4 py-2 border-b-2 transition-colors"
            :class="activeTab === 'overview' ? 'border-blue-600 text-blue-600' : 'border-transparent text-gray-600'">
      Overview
    </button>

    <button @click="activeTab = 'analytics'"
            role="tab"
            :aria-selected="activeTab === 'analytics'"
            :tabindex="activeTab === 'analytics' ? 0 : -1"
            class="px-4 py-2 border-b-2 transition-colors"
            :class="activeTab === 'analytics' ? 'border-blue-600 text-blue-600' : 'border-transparent text-gray-600'">
      Analytics
    </button>
  </div>

  <div role="tabpanel" x-show="activeTab === 'overview'" class="p-6">
    <h3 class="text-lg font-semibold mb-2">Overview Content</h3>
    <p class="text-gray-600">Dashboard overview information here.</p>
  </div>

  <div role="tabpanel" x-show="activeTab === 'analytics'" class="p-6" x-cloak>
    <h3 class="text-lg font-semibold mb-2">Analytics Content</h3>
    <p class="text-gray-600">Analytics data and charts here.</p>
  </div>
</div>
```

**Tab accessibility:**
- `role="tablist"` and `role="tab"` - Define tab structure
- `aria-selected` - Indicates active tab
- `tabindex` management - Only active tab receives focus
- `role="tabpanel"` - Associates content with tabs

## Form Accessibility

### Label Association

Every input must have an associated label, either visible or via `aria-label`:

```html
<!-- Visible label (preferred) -->
<div class="space-y-1">
  <label for="username" class="block text-sm font-medium text-gray-700">
    Username
  </label>
  <input type="text"
         id="username"
         name="username"
         class="w-full px-4 py-2 border rounded-lg focus:ring-2 focus:ring-blue-500">
</div>

<!-- Hidden label with aria-label (only when design requires) -->
<input type="search"
       aria-label="Search products"
       placeholder="Search..."
       class="px-4 py-2 border rounded-lg">
```

### Error Messaging

Errors must be programmatically associated with inputs:

```html
<div class="space-y-1">
  <label for="email" class="block text-sm font-medium text-gray-700">
    Email Address
  </label>
  <input type="email"
         id="email"
         name="email"
         aria-invalid="true"
         aria-describedby="email-error"
         class="w-full px-4 py-2 border-2 border-red-500 rounded-lg focus:ring-2 focus:ring-red-500">
  <p id="email-error" class="text-sm text-red-600" role="alert">
    Please enter a valid email address.
  </p>
</div>
```

**Key attributes:**
- `aria-invalid="true"` - Indicates validation error
- `aria-describedby` - Associates error message with input
- `role="alert"` - Announces error to screen readers immediately

## Focus Management

### Focus Indicators

All focusable elements must have visible focus indicators:

```html
<!-- Tailwind focus utilities -->
<button class="px-4 py-2 bg-blue-600 text-white rounded-lg
               focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
  Click Me
</button>

<a href="#" class="text-blue-600 underline
                   focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 rounded">
  Read More
</a>
```

### Skip Links

Provide skip links for keyboard users to bypass repeated content:

```html
<a href="#main-content"
   class="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4
          px-4 py-2 bg-blue-600 text-white rounded-lg z-50">
  Skip to main content
</a>

<header>
  <!-- Navigation -->
</header>

<main id="main-content" tabindex="-1">
  <!-- Main content -->
</main>
```

## Testing Checklist

Before marking any template complete, verify:

- [ ] All interactive elements keyboard accessible
- [ ] Visible focus indicators on all focusable elements
- [ ] Color contrast meets WCAG AA (4.5:1 for normal text)
- [ ] All images have alt text
- [ ] Forms have associated labels
- [ ] Errors announced to screen readers
- [ ] Modals trap focus and close with Escape
- [ ] Page landmarks identified (`<nav>`, `<main>`, `<aside>`)
- [ ] Heading hierarchy logical (h1 → h2 → h3)
- [ ] Screen reader tested (NVDA, JAWS, or VoiceOver)

Accessibility is not a feature but a requirement. These patterns ensure our templates work for everyone.
