# uView Pro Design Contract (Stitch HTML → uni-app Page Mapping)

When converting Stitch-generated HTML to uni-app + Vue 3 + uView Pro, map structure and styles to the following. Align with stitch-ui-design-spec-uviewpro (same repo) for generation-time constraints. **Use rpx** for typography and spacing. Components use the **u-** prefix (same as uView 2; uView Pro is the Vue 3 package `uview-pro`, easycom: `^u-(.*)` → `uview-pro/components/u-$1`).

## 1. Design Tokens

### Colors (Standard Theme)
- **Primary**: `#3c9cff` (Blue)
- **Success**: `#5ac725`, **Warning**: `#f9ae3d`, **Danger**: `#f56c6c`, **Info**: `#909399`
- **Main Text**: `#303133`, **Content**: `#606266`, **Tips**: `#909399`, **Light**: `#c0c4cc`
- **Border**: `#dadbde`, **Background**: `#f3f4f6`

### Typography (rpx)
- Main Title: 32rpx or 36rpx (Bold)
- Content: 28rpx (Base)
- Tips/Secondary: 24rpx
- Small: 20rpx

### Radius & Spacing
- Radius: 8rpx (Small), 16rpx (Card), 9999px (Circle/Pill).
- Spacing: Use gap in flex or utility classes; rpx where appropriate.

## 2. Component Mapping (Stitch HTML → uView Pro)

### Layout
- **Flex Grid**: `<u-row>`, `<u-col span="6">`.
- **Gap**: `<u-gap height="20" bgColor="#f3f4f6"></u-gap>`.
- **Divider**: `<u-divider text="End"></u-divider>`.

### Buttons
- **Tag**: `<u-button>` — type: primary, success, info, warning, error; size: large, normal, small, mini; shape: circle, round; props: plain, disabled, loading, icon; event: @click.

### Forms
- **Wrapper**: `<u-form :model="form" ref="uForm">`; methods: validate(), validateField(), resetFields(), clearValidate().
- **Item**: `<u-form-item label="Name" prop="name" borderBottom>`
- **Input**: `<u-input v-model="form.name" border="none" placeholder="Please input">` — props: type, size, disabled, readonly, clearable, prefix-icon, suffix-icon; events: @input, @change, @focus, @blur.
- **Upload**: `<u-upload :fileList="fileList1" @afterRead="afterRead" ...></u-upload>`

### Navigation
- **Navbar**: `<u-navbar title="Home" @leftClick="leftClick" :autoBack="true">`
- **Tabs**: `<u-tabs :list="list1" @click="click"></u-tabs>`
- **IndexList**: `<u-index-list :indexList="indexList">...</u-index-list>`

### List & Data
- **SwipeAction**: `<u-swipe-action><u-swipe-action-item ...>...</u-swipe-action-item></u-swipe-action>`
- **List**: `<u-list @scrolltolower="scrolltolower">...</u-list>` (Load more)
- **Grid**: `<u-grid :col="3">...</u-grid>`
- **Waterfall**: `<u-waterfall v-model="flowList">...</u-waterfall>`

### Feedback
- **Toast**: In template `<u-toast ref="uToast"></u-toast>`; JS: `uni.$u.toast('Hello')`.
- **Code**: `<u-code :seconds="60" @end="end"></u-code>` (SMS countdown)

### Icons
- **Tag**: `<u-icon name="photo" color="#2979ff" size="28"></u-icon>`

## 3. Component API quick reference
- See [api/component-api.md](../api/component-api.md) for Button / Input / Form / Toast / Navbar / Tabs / List / SwipeAction / Upload props and events.

## 4. Script Setup (Vue 3)
- Use `<script setup lang="ts">`.
- Import hooks/utils from uview-pro if needed; rely on global `uni.$u` for trim, test, route, http.

## 5. Invariants
- Use u-* component names only; do not use raw HTML for buttons, forms, layout when a u-* component exists.
- Register pages in `pages.json`; use rpx for responsive layout.
- Keep section spacing consistent within a screen.
