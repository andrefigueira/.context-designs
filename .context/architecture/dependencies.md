# Dependencies and Tooling

## Core Dependency Philosophy

This project maintains a minimal dependency footprint to maximize accessibility and reduce maintenance burden. The single required dependency is Tailwind CSS itself, with all other tools being optional enhancements.

### Primary Dependency: Tailwind CSS

**Version**: 3.x or higher

**Why Tailwind CSS:**
- Utility-first approach enables rapid UI development
- Excellent documentation and community support
- Highly customizable through configuration
- Built-in responsive design system
- PurgeCSS integration for production optimization
- No runtime overhead

Templates work with both CDN and build-process implementations of Tailwind, providing flexibility for different project types.

## CDN vs Build Process

### CDN Implementation (Template Default)

All templates include Tailwind via CDN for maximum portability:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Template Name</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Optional: Inline configuration -->
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#f0f9ff',
              500: '#3b82f6',
              900: '#1e3a8a'
            }
          }
        }
      }
    }
  </script>
</head>
<body>
  <!-- Template content -->
</body>
</html>
```

**CDN Benefits:**
- Zero build setup required
- Instant preview in browser
- Easy to share and demonstrate
- No Node.js or npm required
- Perfect for learning and prototyping

**CDN Limitations:**
- Larger file size (no PurgeCSS)
- No custom plugin support
- Limited configuration options
- Not suitable for production

### Build Process Implementation (Production Use)

For production integration, users should replace CDN with proper Tailwind installation:

```bash
# Install Tailwind
npm install -D tailwindcss

# Initialize configuration
npx tailwindcss init
```

**tailwind.config.js:**
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{html,js,jsx,ts,tsx}",
    "./templates/**/*.html"
  ],
  theme: {
    extend: {
      colors: {
        brand: {
          50: '#f0f9ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        }
      }
    }
  },
  plugins: []
}
```

**Production Benefits:**
- Optimized file size (typically 5-10kb gzipped)
- Custom plugin support
- Advanced configuration options
- Better performance

## Optional Dependencies

### Alpine.js (Recommended for Interactivity)

**Version**: 3.x

Alpine.js provides reactive interactivity with minimal overhead:

```html
<!-- Include Alpine.js -->
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

<!-- Example: Dropdown component -->
<div x-data="{ open: false }" class="relative">
  <button @click="open = !open" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
    Toggle Menu
  </button>

  <div x-show="open" @click.outside="open = false"
       class="absolute mt-2 w-48 bg-white rounded-lg shadow-lg">
    <a href="#" class="block px-4 py-2 hover:bg-gray-100">Option 1</a>
    <a href="#" class="block px-4 py-2 hover:bg-gray-100">Option 2</a>
  </div>
</div>
```

**Why Alpine.js:**
- Lightweight (15kb min+gzip)
- Declarative syntax similar to Vue
- No build step required
- Perfect for progressive enhancement
- Excellent documentation

**When to Use:**
- Dropdowns and modals
- Tabs and accordions
- Form validation
- Dynamic filtering
- Any interactive component

### Icon Libraries

**Heroicons (Recommended):**
```html
<!-- Outline icon -->
<svg class="w-6 h-6 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
        d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
</svg>
```

**Lucide Icons (Alternative):**
```html
<script src="https://unpkg.com/lucide@latest"></script>
<i data-lucide="home" class="w-6 h-6 text-gray-600"></i>
<script>lucide.createIcons();</script>
```

**Icon Strategy:**
- Use inline SVG for Heroicons (no dependency)
- Use Lucide for larger icon sets (one dependency)
- Always include `class` for sizing and coloring
- Prefer outline style for consistency

## Development Tools

### Live Server (Optional)

For local development with file watching:

```bash
# VS Code extension
# Install "Live Server" by Ritwick Dey

# Or use Python
python -m http.server 8000

# Or use Node.js
npx serve .
```

### Browser DevTools

Essential for template development:
- Chrome/Edge DevTools for responsive testing
- Firefox for accessibility inspection
- Tailwind CSS IntelliSense (VS Code extension)

## Version Control

### Git Configuration

Recommended `.gitignore` for this project:

```gitignore
# Dependencies
node_modules/

# Build outputs
dist/
build/

# Editor directories
.vscode/
.idea/

# OS files
.DS_Store
Thumbs.db

# Environment files
.env
.env.local
```

## Dependency Update Strategy

**Tailwind CSS Updates:**
- Monitor releases at https://github.com/tailwindlabs/tailwindcss
- Test templates with major version updates
- Update CDN links and documentation
- Verify no breaking changes in utility classes

**Alpine.js Updates:**
- Follow semantic versioning
- Minor updates are generally safe
- Major updates require testing all interactive components

**Policy**: Update dependencies quarterly or when security issues arise. Test all templates after updates to ensure compatibility.

This minimal dependency approach ensures templates remain accessible, maintainable, and easy to integrate into any project regardless of existing tooling choices.
