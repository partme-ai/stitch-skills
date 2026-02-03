# uView Pro Design Contract (Vue 3 / uni-app)

## 1. Design Tokens (Hard Constraints)

### Colors (Standard Theme)
- **Primary**: `#3c9cff` (Blue)
- **Success**: `#5ac725` (Green)
- **Warning**: `#f9ae3d` (Orange)
- **Danger**: `#f56c6c` (Red)
- **Info**: `#909399` (Gray)
- **Main Text**: `#303133`
- **Content Text**: `#606266`
- **Tips Text**: `#909399`
- **Light Text**: `#c0c4cc`
- **Border**: `#dadbde`
- **Background**: `#f3f4f6`

### Typography
- **Unit**: `rpx` (Responsive Pixel) is standard for mobile.
- **Sizes**:
  - Main Title: `32rpx` or `36rpx` (Bold)
  - Content: `28rpx` (Base)
  - Tips/Secondary: `24rpx`
  - Small: `20rpx`

### Radius & Spacing
- **Radius**: `8rpx` (Small), `16rpx` (Card), `9999px` (Circle/Pill).
- **Spacing**: Use `gap` in flex layouts or utility classes if available.

## 2. Component Contracts

**IMPORTANT**: uView Pro components typically use the `up-` prefix (e.g., `<up-button>`).

### Layout
- **Flex Grid**: `<up-row>` and `<up-col span="6">`.
- **Gap**: `<up-gap height="20" bgColor="#f3f4f6"></up-gap>` for vertical spacing.
- **Divider**: `<up-divider text="End"></up-divider>`.

### Buttons
- **Tag**: `<up-button>`
- **Props**: `type="primary"`, `shape="circle"`, `size="normal"`, `plain`.

### Forms
- **Wrapper**: `<up-form :model="form" ref="uForm">`
- **Item**: `<up-form-item label="Name" prop="name" borderBottom>`
- **Input**: `<up-input v-model="form.name" border="none" placeholder="Please input"></up-input>`
- **Upload**: `<up-upload :fileList="fileList1" @afterRead="afterRead" ...></up-upload>`

### Navigation
- **Navbar**: `<up-navbar title="Home" @leftClick="leftClick" :autoBack="true">`
- **Tabs**: `<up-tabs :list="list1" @click="click"></up-tabs>`
- **IndexList**: `<up-index-list :indexList="indexList">...</up-index-list>` (Contact list style)

### List & Data
- **SwipeAction**: `<up-swipe-action><up-swipe-action-item ...>...</up-swipe-action-item></up-swipe-action>`
- **List**: `<up-list @scrolltolower="scrolltolower">...</up-list>` (Load more)
- **Grid Menu**: `<up-grid :col="3">...</up-grid>`
- **Waterfall**: `<up-waterfall v-model="flowList">...</up-waterfall>` (Masonry layout)

### Feedback
- **Toast**: `<up-toast ref="uToast"></up-toast>`
- **JS Usage**: `uni.$u.toast('Hello')` (Note: uView Pro hangs tools on `uni.$u`)
- **Code**: `<up-code :seconds="60" @end="end"></up-code>` (SMS verification countdown)

## 3. Icons
- **Tag**: `<up-icon name="photo" color="#2979ff" size="28"></up-icon>`
- **Library**: Built-in uView Pro icons.

## 4. JS Utilities (`uni.$u`)
- **Trim**: `uni.$u.trim(str)`
- **Test**: `uni.$u.test.mobile(str)` (Validation)
- **Route**: `uni.$u.route('/pages/index/index')`
- **Request**: `uni.$u.http.post(...)`

## 5. Script Setup (Vue 3)
- Use `<script setup lang="ts">`.
- Import hooks and utils from `uview-pro` if needed, or rely on global `uni.$u`.
