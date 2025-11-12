# Interactivity Patterns

## JavaScript Philosophy

Templates prioritize progressive enhancement: core functionality works without JavaScript, with optional Alpine.js for enhanced user experience. This approach ensures templates remain accessible and functional even if JavaScript fails or is disabled.

## Alpine.js Integration

Alpine.js is the recommended JavaScript framework for adding interactivity. Its declarative syntax, small footprint (15kb), and no-build-step approach align perfectly with our template philosophy.

### Including Alpine.js

Add Alpine.js via CDN in template head:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Template Name</title>

  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Alpine.js - placed at end of head with defer -->
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body>
  <!-- Template content -->
</body>
</html>
```

**Note**: The `defer` attribute ensures Alpine.js loads after HTML parsing, preventing render blocking.

## Common Interactive Patterns

### Dropdown Menu

```html
<div x-data="{ open: false }" class="relative">
  <!-- Trigger button -->
  <button @click="open = !open"
          @click.outside="open = false"
          type="button"
          class="flex items-center px-4 py-2 bg-white border rounded-lg hover:bg-gray-50">
    <span>Options</span>
    <svg class="w-4 h-4 ml-2" :class="{ 'rotate-180': open }"
         fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
    </svg>
  </button>

  <!-- Dropdown menu -->
  <div x-show="open"
       x-transition:enter="transition ease-out duration-100"
       x-transition:enter-start="opacity-0 scale-95"
       x-transition:enter-end="opacity-100 scale-100"
       x-transition:leave="transition ease-in duration-75"
       x-transition:leave-start="opacity-100 scale-100"
       x-transition:leave-end="opacity-0 scale-95"
       class="absolute right-0 mt-2 w-56 bg-white border rounded-lg shadow-lg z-10">
    <div class="py-1">
      <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">
        Profile
      </a>
      <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">
        Settings
      </a>
      <a href="#" class="block px-4 py-2 text-sm text-red-600 hover:bg-gray-100">
        Sign Out
      </a>
    </div>
  </div>
</div>
```

**Key Alpine.js directives:**
- `x-data="{ open: false }"` - Initializes component state
- `@click="open = !open"` - Toggles dropdown on click
- `@click.outside` - Closes dropdown when clicking outside
- `x-show="open"` - Conditionally displays dropdown
- `x-transition` - Adds smooth enter/leave animations
- `:class` - Dynamic class binding for chevron rotation

### Modal Dialog

```html
<div x-data="{ modalOpen: false }">
  <!-- Trigger button -->
  <button @click="modalOpen = true"
          class="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
    Open Modal
  </button>

  <!-- Modal overlay and content -->
  <div x-show="modalOpen"
       x-cloak
       @keydown.escape.window="modalOpen = false"
       class="fixed inset-0 z-50 overflow-y-auto">
    <!-- Backdrop -->
    <div class="fixed inset-0 bg-black bg-opacity-50 transition-opacity"></div>

    <!-- Modal container -->
    <div class="flex min-h-full items-center justify-center p-4">
      <!-- Modal content -->
      <div @click.outside="modalOpen = false"
           x-trap.noscroll="modalOpen"
           class="relative bg-white rounded-lg shadow-xl max-w-md w-full p-6">
        <!-- Close button -->
        <button @click="modalOpen = false"
                class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>

        <!-- Modal header -->
        <h3 class="text-xl font-semibold text-gray-900 mb-4">
          Modal Title
        </h3>

        <!-- Modal body -->
        <p class="text-gray-600 mb-6">
          This is the modal content. You can add any HTML here including forms, images, or other components.
        </p>

        <!-- Modal footer -->
        <div class="flex justify-end space-x-3">
          <button @click="modalOpen = false"
                  class="px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300">
            Cancel
          </button>
          <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
            Confirm
          </button>
        </div>
      </div>
    </div>
  </div>
</div>
```

**Advanced features:**
- `x-trap.noscroll` - Traps focus within modal and prevents body scroll
- `@keydown.escape.window` - Closes modal with Escape key
- `x-cloak` - Hides element until Alpine initializes (prevent flash)
- `@click.outside` - Closes modal when clicking backdrop

**Required CSS for x-cloak:**
```html
<style>
  [x-cloak] { display: none !important; }
</style>
```

### Tabs Component

```html
<div x-data="{ activeTab: 'overview' }">
  <!-- Tab buttons -->
  <div class="border-b border-gray-200">
    <nav class="flex space-x-8">
      <button @click="activeTab = 'overview'"
              :class="activeTab === 'overview'
                ? 'border-blue-600 text-blue-600'
                : 'border-transparent text-gray-600 hover:text-gray-800 hover:border-gray-300'"
              class="px-1 py-4 border-b-2 font-medium text-sm transition-colors">
        Overview
      </button>

      <button @click="activeTab = 'analytics'"
              :class="activeTab === 'analytics'
                ? 'border-blue-600 text-blue-600'
                : 'border-transparent text-gray-600 hover:text-gray-800 hover:border-gray-300'"
              class="px-1 py-4 border-b-2 font-medium text-sm transition-colors">
        Analytics
      </button>

      <button @click="activeTab = 'settings'"
              :class="activeTab === 'settings'
                ? 'border-blue-600 text-blue-600'
                : 'border-transparent text-gray-600 hover:text-gray-800 hover:border-gray-300'"
              class="px-1 py-4 border-b-2 font-medium text-sm transition-colors">
        Settings
      </button>
    </nav>
  </div>

  <!-- Tab panels -->
  <div class="mt-6">
    <div x-show="activeTab === 'overview'" x-transition>
      <h3 class="text-lg font-semibold mb-2">Overview</h3>
      <p class="text-gray-600">Overview content goes here.</p>
    </div>

    <div x-show="activeTab === 'analytics'" x-transition x-cloak>
      <h3 class="text-lg font-semibold mb-2">Analytics</h3>
      <p class="text-gray-600">Analytics content goes here.</p>
    </div>

    <div x-show="activeTab === 'settings'" x-transition x-cloak>
      <h3 class="text-lg font-semibold mb-2">Settings</h3>
      <p class="text-gray-600">Settings content goes here.</p>
    </div>
  </div>
</div>
```

### Accordion Component

```html
<div x-data="{ openItem: null }" class="space-y-2">
  <!-- Accordion item 1 -->
  <div class="border border-gray-200 rounded-lg">
    <button @click="openItem = openItem === 1 ? null : 1"
            class="w-full px-6 py-4 flex items-center justify-between text-left bg-white hover:bg-gray-50 rounded-lg">
      <span class="font-medium text-gray-900">What is Tailwind CSS?</span>
      <svg class="w-5 h-5 text-gray-500 transition-transform"
           :class="{ 'rotate-180': openItem === 1 }"
           fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </button>

    <div x-show="openItem === 1"
         x-collapse
         class="px-6 pb-4 text-gray-600">
      Tailwind CSS is a utility-first CSS framework that provides low-level utility classes to build custom designs.
    </div>
  </div>

  <!-- Accordion item 2 -->
  <div class="border border-gray-200 rounded-lg">
    <button @click="openItem = openItem === 2 ? null : 2"
            class="w-full px-6 py-4 flex items-center justify-between text-left bg-white hover:bg-gray-50 rounded-lg">
      <span class="font-medium text-gray-900">How do I customize templates?</span>
      <svg class="w-5 h-5 text-gray-500 transition-transform"
           :class="{ 'rotate-180': openItem === 2 }"
           fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </button>

    <div x-show="openItem === 2"
         x-collapse
         class="px-6 pb-4 text-gray-600">
      Simply modify the Tailwind utility classes to match your design requirements. All components are fully customizable.
    </div>
  </div>
</div>
```

**Note**: `x-collapse` requires Alpine.js Collapse plugin:
```html
<script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/collapse@3.x.x/dist/cdn.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
```

### Sidebar Toggle (Mobile Menu)

```html
<div x-data="{ sidebarOpen: false }">
  <!-- Mobile menu button -->
  <button @click="sidebarOpen = !sidebarOpen"
          class="lg:hidden fixed top-4 left-4 z-50 p-2 bg-white rounded-lg shadow-lg">
    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
    </svg>
  </button>

  <!-- Overlay -->
  <div x-show="sidebarOpen"
       @click="sidebarOpen = false"
       x-transition:enter="transition-opacity ease-linear duration-300"
       x-transition:enter-start="opacity-0"
       x-transition:enter-end="opacity-100"
       x-transition:leave="transition-opacity ease-linear duration-300"
       x-transition:leave-start="opacity-100"
       x-transition:leave-end="opacity-0"
       class="fixed inset-0 bg-black bg-opacity-50 lg:hidden z-40"
       x-cloak></div>

  <!-- Sidebar -->
  <aside x-show="sidebarOpen"
         @click.outside="sidebarOpen = false"
         x-transition:enter="transition ease-in-out duration-300 transform"
         x-transition:enter-start="-translate-x-full"
         x-transition:enter-end="translate-x-0"
         x-transition:leave="transition ease-in-out duration-300 transform"
         x-transition:leave-start="translate-x-0"
         x-transition:leave-end="-translate-x-full"
         class="fixed inset-y-0 left-0 w-64 bg-gray-900 text-white p-6 lg:relative lg:translate-x-0 z-40"
         x-cloak>
    <!-- Sidebar content -->
    <nav class="space-y-2">
      <a href="#" class="block px-4 py-2 rounded-lg bg-gray-800">Dashboard</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-800">Analytics</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-800">Settings</a>
    </nav>
  </aside>
</div>
```

## Event Handling

### Click Events

```html
<!-- Simple click -->
<button @click="count++">Clicked {{ count }} times</button>

<!-- Prevent default -->
<form @submit.prevent="handleSubmit">
  <button type="submit">Submit</button>
</form>

<!-- Stop propagation -->
<div @click="handleParent">
  <button @click.stop="handleChild">Click me</button>
</div>
```

### Keyboard Events

```html
<!-- Enter key -->
<input @keydown.enter="submitForm" />

<!-- Escape key -->
<div @keydown.escape.window="closeModal">

<!-- Multiple modifiers -->
<input @keydown.ctrl.enter="saveAndClose" />
```

## Best Practices

1. **Keep state minimal**: Only track what's necessary for UI changes
2. **Use transitions**: Enhance UX with smooth Alpine.js transitions
3. **Handle edge cases**: Always close dropdowns/modals on outside clicks and Escape key
4. **Trap focus**: Use `x-trap` for modals to maintain accessibility
5. **Prevent layout shift**: Use `x-cloak` to hide elements until Alpine initializes
6. **Progressive enhancement**: Ensure core functionality works without JavaScript when possible

These patterns cover the majority of interactive needs in modern web templates while maintaining simplicity and accessibility.
