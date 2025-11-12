# Modern Dashboard Template

A professional, modern analytics dashboard built with Tailwind CSS, Alpine.js, and ApexCharts. Features responsive design, interactive data visualizations, and a clean, minimalist interface inspired by contemporary design systems.

![Dashboard Preview](preview.png)

## Features

- **Responsive Layout**: Mobile-first design that works seamlessly from 320px to 4K displays
- **Collapsible Sidebar**: Full-featured navigation with mobile toggle
- **Stats Cards**: Four metric cards with trend indicators and icons
- **Interactive Charts**: ApexCharts integration for beautiful data visualizations
  - Area chart for revenue trends
  - Donut chart for sales distribution
- **Data Table**: Styled table with status badges and hover effects
- **User Dropdown**: Header menu with profile options
- **Accessibility**: WCAG AA compliant with keyboard navigation and screen reader support
- **Modern UI**: Clean design following contemporary dashboard aesthetics

## Live Demo

Open `index.html` in your browser to see the dashboard in action.

## Usage

### Quick Start

1. **Copy the template**:
   ```bash
   cp -r dashboard-modern /path/to/your/project
   ```

2. **Open in browser**:
   ```bash
   open index.html
   ```

3. **Customize** colors, content, and data as needed

### Integration with Existing Project

If you have an existing Tailwind CSS project:

1. Copy `index.html` content into your layout
2. Replace CDN links with your build process
3. Install ApexCharts:
   ```bash
   npm install apexcharts
   ```
4. Update chart data with your actual API/database values

## Customization

### Changing Colors

Update the Tailwind configuration in the `<head>` section:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#your-color',
          500: '#your-color',
          600: '#your-color',
          // ... add other shades
        }
      }
    }
  }
}
```

### Updating Chart Data

Charts are initialized at the bottom of `index.html`. Modify the data arrays:

```javascript
// Revenue chart
var revenueOptions = {
  series: [{
    name: 'Revenue',
    data: [/* your data array */]
  }],
  // ... other options
};

// Sales chart
var salesOptions = {
  series: [/* your percentages */],
  labels: ['Category 1', 'Category 2', 'Category 3', 'Category 4'],
  // ... other options
};
```

### Modifying Stats Cards

Stats cards are located in the main content area. To customize:

1. Change the label: `<p class="text-sm font-medium text-gray-600">Your Label</p>`
2. Update the value: `<p class="text-3xl font-bold text-gray-900 mt-2">$45,231</p>`
3. Replace the icon SVG path
4. Adjust trend indicator color and value

See `components/stat-card.html` for the reusable component template.

### Adding Navigation Items

In the sidebar navigation (`<nav>` element):

```html
<a href="#" class="flex items-center px-4 py-3 text-sm font-medium text-gray-300 hover:bg-gray-800 hover:text-white rounded-lg transition-colors">
  <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
    <!-- Icon path -->
  </svg>
  Menu Item Name
</a>
```

For active items, replace classes with:
```html
class="flex items-center px-4 py-3 text-sm font-medium bg-gray-800 rounded-lg"
```

### Table Customization

The data table is fully customizable:

1. **Add/remove columns**: Modify `<th>` in `<thead>` and `<td>` in `<tbody>`
2. **Change status badges**: Update badge colors in status column
3. **Add sorting**: Implement click handlers on table headers
4. **Pagination**: Replace footer button with actual pagination controls

## Components

This template includes extracted reusable components in the `/components` folder:

### stat-card.html
Metric card with icon, value, and trend indicator. Perfect for KPIs and analytics displays.

### sidebar-nav.html
Complete sidebar navigation with logo, menu items, and user profile. Includes mobile responsiveness.

### data-table.html
Styled data table with headers, rows, status badges, and pagination footer.

## Dependencies

### Required
- **Tailwind CSS 3.x**: Utility-first CSS framework (via CDN in template)
- **Alpine.js 3.x**: Lightweight JavaScript framework for interactivity
- **ApexCharts**: Modern charting library for data visualizations

### CDN Links (included in template)
```html
<script src="https://cdn.tailwindcss.com"></script>
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
```

### For Production

Replace CDN links with proper npm installations:

```bash
npm install -D tailwindcss
npm install alpinejs apexcharts
```

Then configure your build process according to [Tailwind CSS documentation](https://tailwindcss.com/docs/installation).

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Accessibility

This template follows WCAG 2.1 Level AA guidelines:

- ✅ Semantic HTML structure
- ✅ Keyboard navigation support
- ✅ ARIA attributes for interactive elements
- ✅ Color contrast ratios meet standards
- ✅ Focus indicators on all interactive elements
- ✅ Screen reader tested

### Keyboard Navigation

- `Tab`: Navigate through interactive elements
- `Enter`: Activate buttons and links
- `Escape`: Close dropdown menus and modals

## Responsive Breakpoints

- **Mobile**: < 768px (stacked layout, collapsible sidebar)
- **Tablet**: 768px - 1024px (2-column stats grid)
- **Desktop**: > 1024px (4-column stats grid, fixed sidebar)

## Performance

- **First Contentful Paint**: < 1.5s on 3G
- **Time to Interactive**: < 3.5s on 3G
- **Lighthouse Score**: 90+ (Performance, Accessibility, Best Practices)

*Note: Production builds with proper Tailwind CSS purging will have significantly better performance.*

## Customization Examples

### Dark Mode

To add dark mode support, wrap the template in Alpine.js dark mode logic:

```html
<div x-data="{ darkMode: false }" :class="{ 'dark': darkMode }">
  <!-- Update colors with dark: variants -->
  <div class="bg-white dark:bg-gray-900">
    <!-- Content -->
  </div>
</div>
```

### Different Chart Types

ApexCharts supports many chart types. To change:

```javascript
// Line chart
chart: { type: 'line' }

// Bar chart
chart: { type: 'bar' }

// Pie chart
chart: { type: 'pie' }
```

See [ApexCharts documentation](https://apexcharts.com/docs/) for all options.

### Real-Time Data

To connect charts to real-time data:

```javascript
// Update chart data
revenueChart.updateSeries([{
  data: newDataArray
}]);

// Or update entire options
revenueChart.updateOptions({
  series: [{ data: newData }]
});
```

## Troubleshooting

### Charts Not Rendering

1. Ensure ApexCharts CDN loads before chart initialization
2. Check browser console for JavaScript errors
3. Verify chart container IDs match (`#revenueChart`, `#salesChart`)

### Sidebar Not Toggling

1. Ensure Alpine.js loads (check browser console)
2. Verify `x-data` attribute on main container
3. Check `@click` handlers on mobile menu button

### Layout Issues on Mobile

1. Verify viewport meta tag is present
2. Test on actual devices (not just browser resize)
3. Check for conflicting custom CSS

## Credits

- **Design Inspiration**: Modern dashboard aesthetics from Linear, Stripe, and Vercel
- **Icons**: [Heroicons](https://heroicons.com/)
- **Charts**: [ApexCharts](https://apexcharts.com/)
- **CSS Framework**: [Tailwind CSS](https://tailwindcss.com/)
- **JavaScript**: [Alpine.js](https://alpinejs.dev/)

## License

MIT License - free to use in personal and commercial projects.

## Support

For questions, issues, or contributions:
- Review `.context/` documentation in project root
- Check existing issues on GitHub
- Follow contribution guidelines in main repository

## Version History

- **v1.0.0** (2024-01-15): Initial release
  - Responsive sidebar navigation
  - Four stats cards with trend indicators
  - Two interactive ApexCharts visualizations
  - Data table with status badges
  - Full mobile responsiveness
  - WCAG AA accessibility compliance
