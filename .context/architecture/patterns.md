# Architectural Patterns and Decisions

## Template Isolation Pattern

Each template exists as a completely isolated unit within its own directory. This architectural decision prevents coupling between templates and enables independent evolution.

### Why Template Isolation

**Independent Versioning**: Templates can be updated without affecting others. A breaking change in one dashboard template doesn't impact the e-commerce templates.

**Selective Download**: Users can download a single template folder without cloning the entire repository. A freelancer needing just an invoice template shouldn't need 50 other templates.

**Clear Ownership**: Each template has its own README, preview, and documentation. Responsibility and maintenance boundaries remain explicit.

**Framework Integration**: Different templates can demonstrate integration with different frameworks (React, Vue, Alpine.js) without conflicts.

### Implementation

```
dashboard-modern/
├── index.html              # Self-contained template
├── README.md              # Template documentation
├── preview.png            # Visual reference
└── components/            # Template-specific components
    └── sidebar.html

analytics-dashboard/       # Completely separate
├── index.html
├── README.md
├── preview.png
└── components/
```

No shared CSS files, no shared JavaScript, no cross-template dependencies. Each template includes everything needed to function independently.

## Progressive Enhancement Pattern

Templates follow progressive enhancement principles: core functionality works without JavaScript, with optional enhancements for better user experience.

### Base Layer: Semantic HTML + Tailwind

```html
<!-- Works without JavaScript -->
<nav class="bg-white shadow-sm">
  <ul class="flex space-x-4 p-4">
    <li><a href="#dashboard" class="text-blue-600 font-medium">Dashboard</a></li>
    <li><a href="#analytics" class="text-gray-600 hover:text-gray-900">Analytics</a></li>
    <li><a href="#settings" class="text-gray-600 hover:text-gray-900">Settings</a></li>
  </ul>
</nav>
```

This navigation functions as standard hyperlinks. No JavaScript required. Hover states work through CSS.

### Enhancement Layer: Alpine.js for Interactivity

```html
<!-- Enhanced with dynamic behavior -->
<nav class="bg-white shadow-sm" x-data="{ activeTab: 'dashboard' }">
  <ul class="flex space-x-4 p-4">
    <li>
      <button @click="activeTab = 'dashboard'"
              :class="activeTab === 'dashboard' ? 'text-blue-600 font-medium' : 'text-gray-600 hover:text-gray-900'">
        Dashboard
      </button>
    </li>
    <li>
      <button @click="activeTab = 'analytics'"
              :class="activeTab === 'analytics' ? 'text-blue-600 font-medium' : 'text-gray-600 hover:text-gray-900'">
        Analytics
      </button>
    </li>
  </ul>
</nav>

<!-- Tab panels -->
<div x-show="activeTab === 'dashboard'" class="p-6">Dashboard content</div>
<div x-show="activeTab === 'analytics'" class="p-6" x-cloak>Analytics content</div>
```

Now we have dynamic tab switching without page reloads. But the base structure remains accessible if JavaScript fails.

## Mobile-First Responsive Pattern

All templates build from mobile layouts upward. This ensures core content is prioritized and larger screens receive enhanced layouts.

### Pattern Implementation

```html
<!-- Mobile-first grid -->
<div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-4">
  <!-- Default: stacked on mobile -->
  <!-- md+: 2 columns on tablets -->
  <!-- lg+: 4 columns on desktop -->
  <div class="bg-white p-6 rounded-lg shadow">Card 1</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 2</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 3</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 4</div>
</div>

<!-- Mobile-first sidebar -->
<div class="flex flex-col lg:flex-row">
  <!-- Sidebar: full width on mobile, side column on desktop -->
  <aside class="w-full lg:w-64 bg-gray-900 text-white p-4">
    Navigation
  </aside>

  <!-- Main content: follows sidebar on mobile, beside it on desktop -->
  <main class="flex-1 p-6">
    Content
  </main>
</div>
```

**Rationale**: Mobile traffic often exceeds desktop. By designing mobile-first, we ensure the core experience works on constrained viewports. Enhancement for larger screens is additive, not subtractive.

## Component Composition Pattern

Components are extracted when they meet reusability, complexity, or variation criteria. Extracted components maintain self-contained documentation.

### Extraction Decision Matrix

| Criteria | Extract | Keep Inline |
|----------|---------|-------------|
| Used in 2+ places | Yes | No |
| More than 50 lines | Yes | No |
| Multiple variations | Yes | No |
| High complexity | Yes | No |
| Unique to one location | No | Yes |
| Tightly coupled to parent | No | Yes |

### Extraction Example

**Before Extraction:**
```html
<!-- Repeated stats cards inline -->
<div class="bg-white rounded-lg shadow p-6">
  <p class="text-sm text-gray-600">Total Users</p>
  <p class="text-3xl font-bold text-gray-900 mt-2">2,543</p>
  <p class="text-sm text-green-600 mt-2">+12.5%</p>
</div>

<div class="bg-white rounded-lg shadow p-6">
  <p class="text-sm text-gray-600">Revenue</p>
  <p class="text-3xl font-bold text-gray-900 mt-2">$45,231</p>
  <p class="text-sm text-green-600 mt-2">+8.2%</p>
</div>
```

**After Extraction:**
```html
<!-- components/stat-card.html -->
<div class="bg-white rounded-lg shadow p-6">
  <p class="text-sm text-gray-600">[LABEL]</p>
  <p class="text-3xl font-bold text-gray-900 mt-2">[VALUE]</p>
  <p class="text-sm text-green-600 mt-2">[CHANGE]</p>
</div>
```

**Usage in template:**
```html
<!-- Reference extracted component -->
<!-- See components/stat-card.html -->
<!-- Replace [LABEL], [VALUE], [CHANGE] with actual data -->
```

## Configuration Over Customization

Templates use inline Tailwind configuration rather than external config files, enabling standalone usage while demonstrating customization patterns.

### Inline Configuration Pattern

```html
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
        },
        fontFamily: {
          sans: ['Inter', 'system-ui', 'sans-serif']
        }
      }
    }
  }
</script>
```

**Rationale**: This approach keeps templates self-contained while showing users how to customize Tailwind. When integrating into a build process, users can transfer these configurations to their `tailwind.config.js`.

## State Management Pattern

For templates requiring state management, we prefer declarative Alpine.js patterns over imperative JavaScript.

### Declarative State Example

```html
<div x-data="{
  isOpen: false,
  activeView: 'grid',
  selectedItems: []
}">
  <!-- State-driven UI -->
  <button @click="isOpen = !isOpen">
    <span x-text="isOpen ? 'Close' : 'Open'"></span>
  </button>

  <div x-show="isOpen" x-transition>
    Content appears with state change
  </div>
</div>
```

**Decision Rationale**: Declarative state keeps template logic transparent and easily modifiable. Users unfamiliar with Alpine can still understand the state structure and modify behavior.

## Accessibility-First Pattern

Accessibility is not an afterthought but a core architectural principle. All interactive patterns include proper ARIA attributes and keyboard navigation.

```html
<!-- Accessible modal pattern -->
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
       class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
    <div class="bg-white rounded-lg p-6 max-w-md">
      <h2 class="text-xl font-semibold mb-4">Modal Title</h2>
      <p class="text-gray-600 mb-4">Modal content here</p>
      <button @click="modalOpen = false" class="px-4 py-2 bg-gray-200 rounded">
        Close
      </button>
    </div>
  </div>
</div>
```

**Key Accessibility Features:**
- `role="dialog"` and `aria-modal="true"` for screen readers
- `x-trap` to trap focus within modal
- Escape key to close
- Proper semantic structure

These architectural patterns ensure templates remain maintainable, accessible, and easy to integrate while providing flexibility for diverse use cases.
