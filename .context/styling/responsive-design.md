# Responsive Design Patterns

## Mobile-First Philosophy

All templates adopt a mobile-first approach: start with mobile styles as the foundation, then progressively enhance for larger screens. This ensures content prioritization and optimal performance on constrained devices.

### Why Mobile-First

**Performance**: Mobile devices load fewer CSS rules initially, improving performance on bandwidth-limited connections.

**Content Priority**: Forces consideration of essential content and features first, creating better information architecture.

**Progressive Enhancement**: Larger screens receive additional features rather than smaller screens having features stripped away.

**Device Reality**: Mobile traffic often exceeds desktop, making mobile the primary experience for many users.

## Breakpoint Strategy

### Tailwind's Default Breakpoints

```
sm:  640px   (small tablets in portrait)
md:  768px   (tablets and small laptops)
lg:  1024px  (laptops and desktops)
xl:  1280px  (large desktops)
2xl: 1536px  (extra large displays)
```

### Practical Breakpoint Usage

**Primary breakpoints**: `md` (768px) and `lg` (1024px) handle most layout shifts.

**Secondary breakpoints**: `sm`, `xl`, and `2xl` for fine-tuning edge cases.

**Example layout transformation:**
```html
<!-- Mobile: Stacked layout -->
<!-- Tablet (md): 2-column grid -->
<!-- Desktop (lg): 3-column grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <div class="bg-white p-6 rounded-lg shadow">Card 1</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 2</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 3</div>
</div>
```

## Common Responsive Patterns

### Sidebar Layout

Transform sidebar from full-width mobile to fixed-width desktop:

```html
<div class="flex flex-col lg:flex-row min-h-screen">
  <!-- Sidebar: full width mobile, fixed width desktop -->
  <aside class="w-full lg:w-64 bg-gray-900 text-white p-6">
    <h2 class="text-xl font-semibold mb-6">Navigation</h2>
    <nav class="space-y-2">
      <a href="#" class="block px-4 py-2 rounded-lg bg-gray-800">Dashboard</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-800">Analytics</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-800">Settings</a>
    </nav>
  </aside>

  <!-- Main content: flexible width -->
  <main class="flex-1 bg-gray-50 p-4 md:p-6 lg:p-8">
    <h1 class="text-2xl md:text-3xl font-bold mb-6">Dashboard</h1>
    <!-- Content -->
  </main>
</div>
```

**Breakdown:**
- `flex-col`: Stack vertically on mobile
- `lg:flex-row`: Switch to horizontal layout at 1024px
- `w-full lg:w-64`: Sidebar takes full width mobile, fixed 256px desktop
- Responsive padding: `p-4 md:p-6 lg:p-8` increases with screen size

### Card Grid

Responsive card grids adapt column count based on available space:

```html
<!-- 1 column mobile → 2 columns tablet → 3 columns desktop → 4 columns large -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 md:gap-6">
  <div class="bg-white rounded-lg shadow-md overflow-hidden">
    <img src="image.jpg" alt="Product" class="w-full h-48 object-cover" />
    <div class="p-4">
      <h3 class="text-lg font-semibold text-gray-900 mb-2">Product Name</h3>
      <p class="text-gray-600 text-sm mb-4">Short description here</p>
      <button class="w-full sm:w-auto px-4 py-2 bg-blue-600 text-white rounded-lg">
        View Details
      </button>
    </div>
  </div>
  <!-- Repeat cards -->
</div>
```

**Features:**
- Progressive column addition at each breakpoint
- Gap spacing increases for larger screens
- Button full-width mobile, auto-width tablet+

### Navigation Bar

Mobile hamburger menu transforming to horizontal desktop nav:

```html
<header x-data="{ mobileMenuOpen: false }" class="bg-white shadow-sm">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-16">
      <!-- Logo -->
      <div class="flex-shrink-0">
        <img src="logo.svg" alt="Logo" class="h-8" />
      </div>

      <!-- Desktop navigation (hidden mobile) -->
      <nav class="hidden md:flex space-x-8">
        <a href="#" class="text-gray-700 hover:text-gray-900 font-medium">Dashboard</a>
        <a href="#" class="text-gray-700 hover:text-gray-900 font-medium">Analytics</a>
        <a href="#" class="text-gray-700 hover:text-gray-900 font-medium">Settings</a>
      </nav>

      <!-- Mobile menu button (hidden desktop) -->
      <button @click="mobileMenuOpen = !mobileMenuOpen"
              class="md:hidden p-2 rounded-lg hover:bg-gray-100">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </div>
  </div>

  <!-- Mobile menu (slide-down) -->
  <div x-show="mobileMenuOpen"
       x-transition:enter="transition ease-out duration-200"
       x-transition:enter-start="opacity-0 -translate-y-1"
       x-transition:enter-end="opacity-100 translate-y-0"
       class="md:hidden border-t border-gray-200">
    <nav class="px-4 py-4 space-y-2">
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-100">Dashboard</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-100">Analytics</a>
      <a href="#" class="block px-4 py-2 rounded-lg hover:bg-gray-100">Settings</a>
    </nav>
  </div>
</header>
```

**Key patterns:**
- `hidden md:flex`: Desktop nav hidden mobile, visible tablet+
- `md:hidden`: Mobile menu button hidden tablet+
- Vertical mobile nav → horizontal desktop nav
- Smooth transitions with Alpine.js

### Typography Scaling

Scale text proportionally across devices:

```html
<article class="max-w-4xl mx-auto px-4 md:px-6 py-8 md:py-12">
  <!-- Hero heading scales significantly -->
  <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold text-gray-900 mb-4 md:mb-6">
    Article Title Goes Here
  </h1>

  <!-- Subheading moderate scaling -->
  <p class="text-lg md:text-xl text-gray-600 mb-8 md:mb-12">
    Lead paragraph with introduction to the article content.
  </p>

  <!-- Body text minimal scaling -->
  <div class="prose prose-lg">
    <p class="text-base md:text-lg leading-relaxed text-gray-700">
      Body content maintains readability across all devices with subtle size adjustments.
    </p>
  </div>
</article>
```

**Scaling strategy:**
- Headings: Significant scaling (3-6 steps)
- Lead text: Moderate scaling (2-3 steps)
- Body text: Minimal scaling (0-1 steps)
- Spacing: Proportional to text size

### Form Layouts

Stack form fields mobile, multi-column desktop:

```html
<form class="space-y-6">
  <!-- Single column mobile, two columns desktop -->
  <div class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6">
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">
        First Name
      </label>
      <input type="text"
             class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500" />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">
        Last Name
      </label>
      <input type="text"
             class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500" />
    </div>
  </div>

  <!-- Full width field -->
  <div>
    <label class="block text-sm font-medium text-gray-700 mb-1">
      Email Address
    </label>
    <input type="email"
           class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500" />
  </div>

  <!-- Button: full width mobile, auto width desktop -->
  <button type="submit"
          class="w-full md:w-auto px-6 py-3 bg-blue-600 text-white font-medium rounded-lg hover:bg-blue-700">
    Submit Form
  </button>
</form>
```

### Dashboard Stats

Transform stat cards from stacked to grid layout:

```html
<!-- 1 col mobile → 2 cols tablet → 4 cols desktop -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 lg:gap-6">
  <div class="bg-white rounded-lg shadow p-4 lg:p-6">
    <div class="flex items-center justify-between">
      <div>
        <p class="text-sm font-medium text-gray-600">Total Users</p>
        <p class="text-2xl lg:text-3xl font-bold text-gray-900 mt-2">2,543</p>
      </div>
      <div class="bg-blue-100 rounded-full p-3">
        <svg class="w-6 h-6 lg:w-8 lg:h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
        </svg>
      </div>
    </div>
    <div class="mt-4 flex items-center text-sm">
      <span class="text-green-600 font-medium">+12.5%</span>
      <span class="text-gray-600 ml-2">vs last month</span>
    </div>
  </div>
  <!-- Repeat for other stats -->
</div>
```

## Container Patterns

### Max-Width Containers

Center content with responsive padding:

```html
<!-- Standard content container -->
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 lg:py-12">
  <h1 class="text-3xl font-bold mb-6">Page Title</h1>
  <!-- Content -->
</div>

<!-- Narrow content (articles, forms) -->
<div class="max-w-2xl mx-auto px-4 sm:px-6 py-8">
  <article class="prose lg:prose-lg">
    <!-- Article content -->
  </article>
</div>

<!-- Wide content (dashboards) -->
<div class="max-w-screen-2xl mx-auto px-4 md:px-6 xl:px-8 py-6">
  <!-- Dashboard widgets -->
</div>
```

**Standard max-widths:**
- `max-w-2xl` (672px): Articles, forms, focused content
- `max-w-4xl` (896px): Documentation, blog posts
- `max-w-7xl` (1280px): Standard pages (most common)
- `max-w-screen-2xl` (1536px): Dashboards, data-heavy layouts

## Image Responsiveness

### Responsive Images

```html
<!-- Full-width images with aspect ratio -->
<img src="hero.jpg"
     alt="Hero image"
     class="w-full h-64 md:h-96 lg:h-[32rem] object-cover rounded-lg" />

<!-- Avatar sizing -->
<img src="avatar.jpg"
     alt="User avatar"
     class="w-10 h-10 md:w-12 md:h-12 rounded-full object-cover" />

<!-- Card images -->
<img src="product.jpg"
     alt="Product"
     class="w-full h-48 sm:h-56 md:h-64 object-cover" />
```

### Picture Element for Art Direction

```html
<picture>
  <source media="(min-width: 1024px)" srcset="hero-desktop.jpg" />
  <source media="(min-width: 768px)" srcset="hero-tablet.jpg" />
  <img src="hero-mobile.jpg" alt="Hero" class="w-full h-auto" />
</picture>
```

## Testing Responsive Designs

### Browser DevTools

Test at these common viewports:
- 375×667 (iPhone SE, small phones)
- 414×896 (iPhone 11/12/13, standard phones)
- 768×1024 (iPad portrait)
- 1024×768 (iPad landscape, small laptops)
- 1440×900 (standard laptop)
- 1920×1080 (desktop)

### Responsive Testing Checklist

- [ ] Content readable at 320px width (smallest common viewport)
- [ ] Images scale appropriately without distortion
- [ ] Text doesn't overflow containers
- [ ] Interactive elements have adequate touch targets (44×44px minimum)
- [ ] Horizontal scrolling never required
- [ ] Navigation accessible at all breakpoints
- [ ] Forms usable on mobile devices
- [ ] Performance acceptable on mobile networks

These responsive patterns ensure templates provide excellent experiences across all device sizes while maintaining code simplicity and performance.
