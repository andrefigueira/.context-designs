# Leads Report Dashboard

A comprehensive CRM/sales dashboard template for tracking leads, pipeline metrics, and sales performance. Built with Tailwind CSS and ApexCharts.

## Features

- **Responsive sidebar navigation** with collapsible menu items
- **5 KPI cards** displaying pipeline value, lead-to-deal rate, contacted leads, qualified leads, and hot leads
- **Sales revenue chart** with monthly bar visualization
- **Customer segmentation** breakdown with visual distribution
- **Channel performance** tracking (Facebook, Twitter, Google, Instagram)
- **Leads by status** with progress bars for pipeline stages
- **Web visits chart** with historical trend line
- **Favorites section** for quick access to companies and contacts
- **Saved searches** with color-coded categories
- **Upgrade prompt** for free trial users
- **Fully responsive** design (mobile to desktop)

## Usage

Simply open `index.html` in your browser. All dependencies are loaded via CDN, so no build process is required.

## Customization

### Update KPI Values

Edit the KPI card values in the main content area (around line 300):

```html
<p class="text-3xl font-bold text-gray-900">$485,000</p>
```

### Modify Chart Data

**Sales Revenue Chart** (around line 730):
```javascript
data: [0, 0, 0, 0, 1630000, 0, 0, 0, 0, 0, 0, 0]
```

**Web Visits Chart** (around line 765):
```javascript
data: [650, 680, 620, ...]
```

### Change Colors

Update the Tailwind config in the `<head>` section:

```javascript
tailwind.config = {
    theme: {
        extend: {
            colors: {
                primary: {
                    // Your custom colors
                }
            }
        }
    }
}
```

### Add/Remove Navigation Items

Edit the sidebar navigation section (around line 50) to add or remove menu items.

## Components

The dashboard includes these reusable patterns:

- **Stat Cards**: KPI metrics with trend indicators
- **Progress Bars**: Visual representation of leads by status
- **Horizontal Bar Chart**: Sales revenue by month
- **Line Chart**: Web visits trend over time
- **Segmentation Bar**: Customer distribution visualization
- **Channel List**: Performance metrics with icons

## Dependencies

- **Tailwind CSS 3.x** (via CDN)
- **Alpine.js 3.x** (via CDN) - for sidebar toggle and dropdowns
- **ApexCharts** (via CDN) - for data visualizations

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Accessibility

- Semantic HTML5 structure
- ARIA labels on interactive elements
- Keyboard navigation support
- Color contrast meets WCAG AA standards

## Performance

- Minimal JavaScript footprint
- CDN-hosted dependencies
- Optimized chart rendering
- No build process required

## License

Free to use for personal and commercial projects.
