# Design Guidelines: Aadhaar CRM Super Admin Dashboard

## Design Approach
**System Selected:** Material Design 3 adapted for enterprise dashboards
**Rationale:** Information-dense administrative interface requiring clarity, familiar patterns, and visual hierarchy for complex data displays. Combining Material's elevation system with enterprise dashboard conventions.

## Core Design Elements

### Typography
- **Primary Font:** Inter via Google Fonts CDN
- **Hierarchy:**
  - Dashboard Title: text-2xl font-semibold
  - Section Headers: text-lg font-semibold
  - KPI Values: text-3xl font-bold
  - KPI Labels: text-sm font-medium text-gray-600
  - Body Text: text-sm font-normal
  - Chart Labels: text-xs

### Layout System
**Spacing Units:** Consistently use Tailwind units of 3, 4, 6, and 8
- Page padding: p-6 or p-8
- Card padding: p-6
- Section gaps: gap-6
- Card gaps in grids: gap-4
- Element spacing: space-y-4, space-x-3

**Grid Structure:**
- Main layout: Sidebar (240px fixed) + Content area (flex-1)
- KPI Cards Grid: grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4
- Analytics Section: grid-cols-1 lg:grid-cols-2 gap-6
- Data Tables: Full-width with horizontal scroll on mobile

### Component Library

**Navigation Sidebar:**
- Fixed left sidebar, full height, slight elevation (shadow-lg)
- Logo area at top (h-16)
- Navigation items with icons (Heroicons) + labels
- Active state: subtle background, primary accent border-l-4
- Collapsible on mobile

**KPI Cards (4 across desktop):**
- White background, rounded-lg, shadow-sm
- Icon in colored circle (top-left)
- Large metric value (text-3xl)
- Label + percentage change indicator
- Trend micro-chart or sparkline (optional visual)

**Chart Components:**
- Use Chart.js via CDN for all visualizations
- Line Charts: Enrollment trends over time
- Bar Charts: Organizational comparisons
- Donut Charts: Category distributions
- Area Charts: Cumulative metrics
- Height: h-64 to h-80 for standard charts

**Data Table:**
- Sticky header with sort indicators
- Alternating row backgrounds (stripe pattern)
- Action buttons column (right-aligned)
- Status badges (colored pills)
- Pagination controls at bottom

**Activity Feed:**
- Vertical timeline with connecting line
- Timestamp + action description
- User avatar (circular, 32px)
- Max height with overflow scroll (max-h-96)

**Filter/Search Bar:**
- Horizontal layout above main content
- Date range picker, search input, status dropdown
- Export/Download button (right-aligned)

**Top Header Bar:**
- User profile dropdown (right)
- Notification bell icon with badge
- Breadcrumb navigation (left)
- Height: h-16, border-b

### Page Structure

**Dashboard Layout Order:**
1. Top Header Bar (fixed)
2. KPI Cards Row (4 metrics)
3. Analytics Section (2-column grid):
   - Left: Enrollment Trends Line Chart
   - Right: Organizational Comparison Bar Chart
4. Recent Activity Section (2-column):
   - Left: Real-time Activity Feed
   - Right: Top Performing Organizations Table
5. Detailed Data Table (full-width)

### Icons
Use Heroicons via CDN exclusively for:
- Navigation items (outline variant)
- KPI card icons (solid variant in colored backgrounds)
- Action buttons (outline, 16px)
- Status indicators

### Images
**No hero images required** - This is a functional dashboard, not a marketing interface. Focus entirely on data visualization and clarity.

### Visual Hierarchy
- Use elevation (shadow-sm, shadow-md) to separate card layers
- Primary data uses larger typography and bold weights
- Supporting data in muted gray tones
- Color-code metrics: Green (positive), Red (negative), Blue (neutral)
- Rounded corners: rounded-lg for cards, rounded-full for badges/avatars

### Interactive States
- Cards: hover:shadow-md transition
- Buttons: Standard Material Design button states
- Table rows: hover:bg-gray-50 for scannability
- No animations beyond subtle transitions (200ms duration)

### Responsive Behavior
- Desktop (lg): Full sidebar, 4-column KPI grid, 2-column analytics
- Tablet (md): Collapsed sidebar icon-only, 2-column KPIs
- Mobile (base): Hidden sidebar (hamburger menu), single-column stack, horizontal scroll tables