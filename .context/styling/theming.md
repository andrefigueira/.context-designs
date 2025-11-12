# Theming and Customization

## Color System Architecture

Templates use a semantic color system that separates brand colors from functional colors, enabling easy customization while maintaining consistency.

### Brand Color Configuration

Define brand colors through Tailwind configuration:

```html
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          // Primary brand color
          primary: {
            50: '#eff6ff',
            100: '#dbeafe',
            200: '#bfdbfe',
            300: '#93c5fd',
            400: '#60a5fa',
            500: '#3b82f6',  // Base brand color
            600: '#2563eb',
            700: '#1d4ed8',
            800: '#1e40af',
            900: '#1e3a8a',
            950: '#172554'
          },
          // Secondary brand color (optional)
          secondary: {
            50: '#f8fafc',
            500: '#64748b',
            900: '#0f172a'
          }
        }
      }
    }
  }
</script>
```

**Usage in templates:**
```html
<!-- Primary actions -->
<button class="bg-primary-600 hover:bg-primary-700 text-white px-4 py-2 rounded-lg">
  Primary Button
</button>

<!-- Links and accents -->
<a href="#" class="text-primary-600 hover:text-primary-700">Learn more</a>

<!-- Backgrounds and badges -->
<div class="bg-primary-50 text-primary-900 px-3 py-1 rounded-full text-sm">
  New Feature
</div>
```

### Functional Color System

Use semantic naming for functional colors:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        success: {
          50: '#f0fdf4',
          100: '#dcfce7',
          500: '#22c55e',
          700: '#15803d',
          900: '#14532d'
        },
        warning: {
          50: '#fffbeb',
          100: '#fef3c7',
          500: '#f59e0b',
          700: '#b45309',
          900: '#78350f'
        },
        error: {
          50: '#fef2f2',
          100: '#fee2e2',
          500: '#ef4444',
          700: '#b91c1c',
          900: '#7f1d1d'
        },
        info: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          700: '#1d4ed8',
          900: '#1e3a8a'
        }
      }
    }
  }
}
```

**Functional color usage:**
```html
<!-- Success alert -->
<div class="bg-success-50 border border-success-200 text-success-900 rounded-lg p-4">
  <p class="font-medium">Success!</p>
  <p class="text-success-700">Your changes have been saved.</p>
</div>

<!-- Error state -->
<input class="border-error-500 focus:ring-error-500" />
<p class="text-error-600 text-sm mt-1">This field is required.</p>

<!-- Warning banner -->
<div class="bg-warning-50 border-l-4 border-warning-500 p-4">
  <p class="text-warning-900 font-medium">Warning</p>
  <p class="text-warning-700">Your subscription expires in 3 days.</p>
</div>
```

## Dark Mode Implementation

Implement dark mode using Tailwind's `dark:` variant with class-based strategy:

### Configuration

```html
<script>
  tailwind.config = {
    darkMode: 'class',  // Enable class-based dark mode
    theme: {
      extend: {
        // Custom dark mode colors if needed
      }
    }
  }
</script>
```

### Dark Mode Toggle

```html
<div x-data="{ darkMode: $persist(false).as('darkMode') }"
     :class="{ 'dark': darkMode }">

  <!-- Dark mode toggle button -->
  <button @click="darkMode = !darkMode"
          class="p-2 rounded-lg bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600">
    <!-- Sun icon (show in dark mode) -->
    <svg x-show="darkMode" class="w-5 h-5 text-gray-800 dark:text-gray-200"
         fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
    </svg>

    <!-- Moon icon (show in light mode) -->
    <svg x-show="!darkMode" class="w-5 h-5 text-gray-600"
         fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
    </svg>
  </button>

  <!-- Page content with dark mode styles -->
  <div class="bg-white dark:bg-gray-900 min-h-screen">
    <header class="bg-white dark:bg-gray-800 shadow-sm dark:shadow-gray-700 border-b border-gray-200 dark:border-gray-700">
      <h1 class="text-2xl font-bold text-gray-900 dark:text-white p-6">
        Dashboard
      </h1>
    </header>

    <main class="p-6">
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md dark:shadow-gray-700 p-6">
        <h2 class="text-xl font-semibold text-gray-900 dark:text-white mb-4">
          Card Title
        </h2>
        <p class="text-gray-600 dark:text-gray-300">
          Card content that adapts to dark mode automatically.
        </p>
      </div>
    </main>
  </div>
</div>
```

**Requires Alpine Persist plugin:**
```html
<script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/persist@3.x.x/dist/cdn.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
```

### Dark Mode Color Strategy

**Background colors:**
```html
<div class="bg-white dark:bg-gray-900">Page background</div>
<div class="bg-gray-50 dark:bg-gray-800">Section background</div>
<div class="bg-white dark:bg-gray-800">Card background</div>
```

**Text colors:**
```html
<h1 class="text-gray-900 dark:text-white">Primary heading</h1>
<p class="text-gray-700 dark:text-gray-300">Body text</p>
<p class="text-gray-600 dark:text-gray-400">Secondary text</p>
<p class="text-gray-500 dark:text-gray-500">Muted text</p>
```

**Border colors:**
```html
<div class="border border-gray-200 dark:border-gray-700">
  Card with dark mode border
</div>
```

**Interactive elements:**
```html
<button class="bg-blue-600 hover:bg-blue-700 dark:bg-blue-500 dark:hover:bg-blue-600 text-white">
  Button maintains contrast in both modes
</button>

<a href="#" class="text-blue-600 hover:text-blue-700 dark:text-blue-400 dark:hover:text-blue-300">
  Link with dark mode variant
</a>
```

### Dark Mode Best Practices

1. **Test contrast**: Ensure WCAG AA compliance in both modes
2. **Adjust shadows**: Dark mode needs different shadow opacity
3. **Icon colors**: Use `text-gray-600 dark:text-gray-400` for icons
4. **Images**: Consider filter or different images for dark mode
5. **Avoid pure black**: Use `bg-gray-900` instead of `bg-black` for better readability

## Typography Customization

### Custom Fonts

Load custom fonts via Google Fonts or local hosting:

```html
<head>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'system-ui', 'sans-serif'],
            heading: ['Inter', 'system-ui', 'sans-serif']
          }
        }
      }
    }
  </script>
</head>

<body class="font-sans antialiased">
  <h1 class="font-heading font-bold">Heading with custom font</h1>
  <p class="font-sans">Body text with Inter font</p>
</body>
```

### Typography Scale Customization

```javascript
tailwind.config = {
  theme: {
    extend: {
      fontSize: {
        '2xs': ['0.625rem', { lineHeight: '0.75rem' }],
        '3xl': ['2rem', { lineHeight: '2.375rem' }],
        '4xl': ['2.5rem', { lineHeight: '2.875rem' }],
        '5xl': ['3.25rem', { lineHeight: '3.75rem' }]
      }
    }
  }
}
```

## Spacing Customization

Add project-specific spacing values:

```javascript
tailwind.config = {
  theme: {
    extend: {
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
        '128': '32rem'
      }
    }
  }
}
```

## Border Radius Customization

Define brand-specific border radius scale:

```javascript
tailwind.config = {
  theme: {
    extend: {
      borderRadius: {
        '4xl': '2rem',
        '5xl': '3rem'
      }
    }
  }
}
```

**Usage:**
```html
<div class="rounded-4xl">Extra rounded card</div>
<button class="rounded-lg">Standard button (0.5rem)</button>
<img class="rounded-full" />
```

## Component Theming Example

Complete themed card component:

```html
<div class="bg-white dark:bg-gray-800 rounded-lg shadow-md dark:shadow-gray-700 border border-gray-200 dark:border-gray-700 overflow-hidden">
  <!-- Card header with brand color accent -->
  <div class="border-l-4 border-primary-500 p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
        Revenue Overview
      </h3>
      <span class="px-3 py-1 bg-primary-50 dark:bg-primary-900 text-primary-700 dark:text-primary-300 text-sm font-medium rounded-full">
        +12.5%
      </span>
    </div>

    <p class="text-3xl font-bold text-gray-900 dark:text-white mb-2">
      $45,231
    </p>

    <p class="text-sm text-gray-600 dark:text-gray-400">
      vs $40,205 last month
    </p>
  </div>

  <!-- Card body -->
  <div class="p-6 bg-gray-50 dark:bg-gray-900">
    <button class="w-full px-4 py-2 bg-primary-600 hover:bg-primary-700 dark:bg-primary-500 dark:hover:bg-primary-600 text-white font-medium rounded-lg transition-colors">
      View Details
    </button>
  </div>
</div>
```

## Customization Workflow

When customizing templates for a brand:

1. **Define brand colors** in Tailwind config with full shade palette
2. **Replace primary color references** throughout template
3. **Test dark mode** if implemented, adjusting color variants
4. **Customize typography** if brand uses specific fonts
5. **Adjust spacing** if brand guidelines require different scales
6. **Update border radius** to match brand style (sharp vs rounded)
7. **Test accessibility** ensuring contrast ratios meet WCAG standards

This theming system provides flexibility while maintaining consistency across templates and supporting both light and dark modes effortlessly.
