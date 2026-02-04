# Layui-Vue Design Contract (Stitch HTML → Vue SFC Mapping)

When converting Stitch-generated HTML to Vue 3 + Layui-Vue, map structure and styles to the following. Align with stitch-ui-design-spec-layui for generation-time constraints.

## 1. Design Tokens

### Color Tokens (Layui-Vue theme)
- **Primary**: `#16baaa` (Cyan-Green), **Secondary**: `#16b777`, **Nav-bg**: `#393D49`
- **Functional**: Success `#16b777`, Warning `#FFB800`, Danger `#FF5722`, Info `#31BDEC`
- **Neutrals**: Text `#333`/`#666`/`#999`, Border `#e2e2e2`/`#eeeeee`, Bg `#f2f2f2`/`#ffffff`

### Typography & Spacing
- **Font sizes (px)**: 12, 14, 16, 18, 20, 24, 30. **Titles**: font-weight 500; **Body**: 400.
- **Spacing (px)**: 5, 10, 15, 20, 30 (10/15px grid).

### Radius & Border
- **Radius**: Small 2px, Medium 4px. Do not use large radius (8px+) unless requested.
- **Border**: 1px solid `#e2e2e2`. **Shadows**: Very subtle or flat.

## 2. Component Mapping (Stitch HTML → Layui-Vue)

### Component tags and usage (Layui-Vue uses lay- prefix)
- **Button**: `<lay-button type="primary" size="md">` — type: primary, normal, warm, danger; size: lg, md, sm, xs; props: disabled, loading, icon; event: @click.
- **Input**: `<lay-input v-model="val" placeholder="..." />` — props: disabled, readonly, prefixIcon, suffixIcon; events: @input, @change, @blur, @focus.
- **Table**: use columns, dataSource, pagination, sortable, checkbox; events: @change, @select.
- **DatePicker**: `<lay-date-picker v-model="date" type="date" />` — type: date, datetime, year, month, daterange; event: @change.
- **Card style**: Bg white, Header height 42px, border-bottom #f6f6f6, Body padding 10px 15px, Radius 2px (use lay-card or equivalent).
- **PageHeader**: `<lay-page-header content="Detail" @back="onBack" />`
- **Result**: `<lay-result status="success" title="Success" describe="..." />`
- **Skeleton**: `<lay-skeleton :rows="4" />`
- **Timeline**: `<lay-timeline><lay-timeline-item title="Step 1">...</lay-timeline-item></lay-timeline>`
- **Space**: `<lay-space direction="vertical" size="md">...</lay-space>`

### Design dimensions (align when converting)
- Buttons: height 38px (normal), 30px (small), 44px (large); Radius 2px.
- Inputs: height 38px, Border #e2e2e2, Focus border #16baaa.
- Table: Header bg #f2f2f2, Border #e2e2e2, Row hover #f8f8f8.

## 3. Component API quick reference
- See [api/component-api.md](../api/component-api.md) for Button / Input / Table / DatePicker / Form props and events.

## 4. Invariants

- **Radius**: Strictly 2px or 4px. No large rounded corners (8px+).
- **Style**: Minimalist, flat, clean, "Classic Design".
- **No raw HTML for UI**: Use `<lay-button>` not `<button class="layui-btn">`; use Layui-Vue table/input components per api.
