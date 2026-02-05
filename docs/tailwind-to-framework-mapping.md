# Tailwind → Framework Mapping (Stitch HTML Conversion)

## Purpose

Stitch exports **Tailwind-based HTML**. When converting to a target framework, AI must map **Tailwind utilities** to that framework’s units and components instead of copying class names. This document is the **Tailwind-side reference**: it indexes **Tailwind’s official categories, utilities, and docs** so the AI can query “what is this class / where does it belong?” and then use each framework’s **independent** mapping doc for the actual conversion.

- **This doc**: Tailwind official structure, categories, utility patterns, scale, and doc links (no framework-specific mapping).
- **Per-framework mapping**: Each skill keeps its own `references/tailwind-to-<framework>.md`; see [Where each framework defines its mapping](#where-each-framework-defines-its-mapping).

---

## How to use this doc (AI query flow)

1. **See a Tailwind class in Stitch HTML** (e.g. `p-4`, `text-sm`, `rounded-xl`, `bg-primary`).
2. **Find the category** in the sections below (Layout, Spacing, Typography, Colors, etc.) and the **utility pattern** (e.g. padding → `p-*`, `px-*`, `py-*`).
3. **Open the official Tailwind link** for that category if you need exact values or behavior.
4. **Use the target framework’s mapping doc** (e.g. `tailwind-to-uviewpro.md`) to get the concrete conversion (rpx, component prop, theme token).

---

## Tailwind scale and theme (source of truth)

- **Spacing scale**: Default `1` = 0.25rem = 4px. So `p-4` = 16px, `m-2` = 8px, `gap-4` = 16px.  
  Official: [Customizing spacing](https://tailwindcss.com/docs/customizing-spacing), [Padding](https://tailwindcss.com/docs/padding), [Margin](https://tailwindcss.com/docs/margin).
- **Theme variables**: Tailwind v4 uses `@theme` and CSS variables (e.g. `--color-primary`, `--radius-xl`). Stitch may define `primary`, `background-light`, `shadow-soft` in `tailwind.config` or theme.  
  Official: [Theme variables](https://tailwindcss.com/docs/theme-variables), [Colors](https://tailwindcss.com/docs/colors).

---

## Tailwind official categories and utilities

Below, each category lists **official doc link(s)** and **main utility patterns** you will see in Stitch HTML. Use these to classify a class, then look up the conversion in the target framework’s `tailwind-to-<framework>.md`.

### Getting started

| Topic | Official doc | Notes |
|-------|--------------|--------|
| Installation (Vite) | [Using Vite](https://tailwindcss.com/docs/installation/using-vite) | Stitch output is pre-built HTML/CSS; no install needed for conversion. |
| Utility classes | [Styling with utility classes](https://tailwindcss.com/docs/styling-with-utility-classes) | How Tailwind class names work. |
| Responsive design | [Responsive design](https://tailwindcss.com/docs/responsive-design) | Prefixes: `sm:`, `md:`, `lg:`, `xl:`, `2xl:`. |
| Dark mode | [Dark mode](https://tailwindcss.com/docs/dark-mode) | Prefix `dark:` (e.g. `dark:bg-gray-800`, `dark:text-white`). |
| Theme / config | [Theme variables](https://tailwindcss.com/docs/theme-variables), [Configuration](https://tailwindcss.com/docs/configuration) | Custom colors (e.g. `primary`), radius, shadows. |

---

### Layout

| Category | Official doc | Main utility patterns (examples) |
|----------|--------------|-----------------------------------|
| Display | [display](https://tailwindcss.com/docs/display) | `block`, `inline-block`, `inline`, `flex`, `grid`, `hidden`, `contents`. |
| Position | [position](https://tailwindcss.com/docs/position) | `static`, `fixed`, `absolute`, `relative`, `sticky`. |
| Top / Right / Bottom / Left | [top right bottom left](https://tailwindcss.com/docs/top-right-bottom-left) | `top-0`, `right-0`, `bottom-0`, `left-0`, `inset-0`, `top-14`, etc. |
| Visibility | [visibility](https://tailwindcss.com/docs/visibility) | `visible`, `invisible`, `collapse`. |
| Z-index | [z-index](https://tailwindcss.com/docs/z-index) | `z-0`, `z-10`, `z-50`, `z-auto`. |
| Overflow | [overflow](https://tailwindcss.com/docs/overflow) | `overflow-auto`, `overflow-hidden`, `overflow-visible`, `overflow-scroll`, `overflow-x-*`, `overflow-y-*`. |
| Object fit / position | [object-fit](https://tailwindcss.com/docs/object-fit), [object-position](https://tailwindcss.com/docs/object-position) | `object-contain`, `object-cover`, `object-fill`, `object-none`; `object-top`, `object-center`. |
| Aspect ratio | [aspect-ratio](https://tailwindcss.com/docs/aspect-ratio) | `aspect-auto`, `aspect-square`, `aspect-video`, `aspect-4/3`, etc. |
| Box sizing | [box-sizing](https://tailwindcss.com/docs/box-sizing) | `box-border`, `box-content`. |
| Flex basis / direction / wrap | [flex](https://tailwindcss.com/docs/flex) | `basis-*`, `flex-auto`, `flex-initial`, `flex-none`, `flex-1`. |
| Flex direction | [flex-direction](https://tailwindcss.com/docs/flex-direction) | `flex-row`, `flex-row-reverse`, `flex-col`, `flex-col-reverse`. |
| Flex wrap | [flex-wrap](https://tailwindcss.com/docs/flex-wrap) | `flex-wrap`, `flex-wrap-reverse`, `flex-nowrap`. |
| Flex grow / shrink | [flex-grow](https://tailwindcss.com/docs/flex-grow), [flex-shrink](https://tailwindcss.com/docs/flex-shrink) | `grow`, `grow-0`; `shrink`, `shrink-0`. |
| Order | [order](https://tailwindcss.com/docs/order) | `order-1`, `order-2`, `order-first`, `order-last`, `order-none`. |
| Grid template columns/rows | [grid-template-columns](https://tailwindcss.com/docs/grid-template-columns), [grid-template-rows](https://tailwindcss.com/docs/grid-template-rows) | `grid-cols-1` … `grid-cols-12`, `grid-cols-none`; `grid-rows-*`. |
| Grid column/row span | [grid-column](https://tailwindcss.com/docs/grid-column), [grid-row](https://tailwindcss.com/docs/grid-row) | `col-auto`, `col-span-*`, `col-start-*`, `col-end-*`; `row-*` variants. |
| Gap | [gap](https://tailwindcss.com/docs/gap) | `gap-0` … `gap-*`, `gap-x-*`, `gap-y-*`. |
| Justify / align content | [justify-content](https://tailwindcss.com/docs/justify-content), [align-content](https://tailwindcss.com/docs/align-content) | `justify-start`, `justify-end`, `justify-center`, `justify-between`, `justify-around`, `justify-evenly`; `content-*`. |
| Justify / align items | [justify-items](https://tailwindcss.com/docs/justify-items), [align-items](https://tailwindcss.com/docs/align-items) | `justify-items-*`; `items-start`, `items-end`, `items-center`, `items-baseline`, `items-stretch`. |
| Place content / items / self | [place-content](https://tailwindcss.com/docs/place-content), [place-items](https://tailwindcss.com/docs/place-items), [place-self](https://tailwindcss.com/docs/place-self) | `place-content-*`, `place-items-*`, `place-self-*`. |

---

### Spacing

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Padding | [padding](https://tailwindcss.com/docs/padding) | `p-0` … `p-*`, `px-*`, `py-*`, `pt-*`, `pr-*`, `pb-*`, `pl-*`, `ps-*`, `pe-*`. |
| Margin | [margin](https://tailwindcss.com/docs/margin) | `m-*`, `mx-*`, `my-*`, `mt-*`, `mr-*`, `mb-*`, `ml-*`, `ms-*`, `me-*`, `-m-*` (negative). |
| Space between | [space](https://tailwindcss.com/docs/space) (if present in v4) or gap | `space-x-*`, `space-y-*` (margin between children). |

Scale (default): `0`, `0.5`, `1`, `2`, `3`, `4`, `5`, `6`, `8`, `10`, `12`, `16`, `20`, `24`, … (units = 0.25rem each, e.g. `4` = 1rem = 16px).

---

### Sizing

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Width | [width](https://tailwindcss.com/docs/width) | `w-0`, `w-px`, `w-*` (e.g. `w-10`, `w-24`), `w-full`, `w-screen`, `w-min`, `w-max`, `w-fit`, `w-auto`, `w-1/2`, `w-1/3`, etc. |
| Min-width | [min-width](https://tailwindcss.com/docs/min-width) | `min-w-0`, `min-w-full`, `min-w-min`, `min-w-max`, `min-w-fit`. |
| Max-width | [max-width](https://tailwindcss.com/docs/max-width) | `max-w-*`, `max-w-xs` … `max-w-7xl`, `max-w-full`, `max-w-screen-*`. |
| Height | [height](https://tailwindcss.com/docs/height) | `h-0`, `h-px`, `h-*`, `h-full`, `h-screen`, `h-min`, `h-max`, `h-fit`, `h-auto`. |
| Min-height | [min-height](https://tailwindcss.com/docs/min-height) | `min-h-0`, `min-h-full`, `min-h-screen`, `min-h-min`, `min-h-max`, `min-h-fit`. |
| Max-height | [max-height](https://tailwindcss.com/docs/max-height) | `max-h-*`, `max-h-full`, `max-h-screen`. |
| Size (width+height) | [size](https://tailwindcss.com/docs/size) (if present) | `size-*` for equal width and height. |

---

### Typography

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Font family | [font-family](https://tailwindcss.com/docs/font-family) | `font-sans`, `font-serif`, `font-mono`. |
| Font size | [font-size](https://tailwindcss.com/docs/font-size) | `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl` … `text-9xl`. |
| Font smoothing | [font-smoothing](https://tailwindcss.com/docs/font-smoothing) | `antialiased`, `subpixel-antialiased`. |
| Font style | [font-style](https://tailwindcss.com/docs/font-style) | `italic`, `not-italic`. |
| Font weight | [font-weight](https://tailwindcss.com/docs/font-weight) | `font-thin`, `font-extralight`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `font-extrabold`, `font-black`. |
| Letter spacing | [letter-spacing](https://tailwindcss.com/docs/letter-spacing) | `tracking-tighter`, `tracking-tight`, `tracking-normal`, `tracking-wide`, `tracking-wider`, `tracking-widest`. |
| Line height | [line-height](https://tailwindcss.com/docs/line-height) | `leading-none`, `leading-tight`, `leading-snug`, `leading-normal`, `leading-relaxed`, `leading-loose`, `leading-*`. |
| Text align | [text-align](https://tailwindcss.com/docs/text-align) | `text-left`, `text-center`, `text-right`, `text-justify`, `text-start`, `text-end`. |
| Text color | [color](https://tailwindcss.com/docs/color) (text) | `text-*` (e.g. `text-gray-500`, `text-primary`, `text-white`, `text-black`). |
| Text decoration | [text-decoration](https://tailwindcss.com/docs/text-decoration-line) | `underline`, `overline`, `line-through`, `no-underline`. |
| Text transform | [text-transform](https://tailwindcss.com/docs/text-transform) | `uppercase`, `lowercase`, `capitalize`, `normal-case`. |
| Text overflow | [text-overflow](https://tailwindcss.com/docs/text-overflow) | `truncate`, `text-ellipsis`, `text-clip`. |
| Line clamp | [line-clamp](https://tailwindcss.com/docs/line-clamp) | `line-clamp-1` … `line-clamp-none`. |
| List style | [list-style-type](https://tailwindcss.com/docs/list-style-type) | `list-none`, `list-disc`, `list-decimal`. |
| Vertical align | [vertical-align](https://tailwindcss.com/docs/vertical-align) | `align-baseline`, `align-top`, `align-middle`, `align-bottom`, `align-sub`, `align-super`. |
| White space | [white-space](https://tailwindcss.com/docs/white-space) | `whitespace-normal`, `whitespace-nowrap`, `whitespace-pre`, `whitespace-pre-line`, `whitespace-pre-wrap`, `whitespace-break-spaces`. |
| Word break | [word-break](https://tailwindcss.com/docs/word-break), [overflow-wrap](https://tailwindcss.com/docs/overflow-wrap) | `break-normal`, `break-words`, `break-all`, `break-keep`; `overflow-wrap-*`. |

---

### Backgrounds

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Background color | [background-color](https://tailwindcss.com/docs/background-color) | `bg-transparent`, `bg-current`, `bg-*` (e.g. `bg-white`, `bg-gray-50`, `bg-primary`, `bg-card-light`). |
| Background image | [background-image](https://tailwindcss.com/docs/background-image) | `bg-none`, `bg-gradient-*`, `bg-*` image utilities. |
| Background size | [background-size](https://tailwindcss.com/docs/background-size) | `bg-auto`, `bg-cover`, `bg-contain`. |
| Background position | [background-position](https://tailwindcss.com/docs/background-position) | `bg-center`, `bg-top`, `bg-bottom`, `bg-left`, `bg-right`, etc. |
| Background repeat | [background-repeat](https://tailwindcss.com/docs/background-repeat) | `bg-repeat`, `bg-no-repeat`, `bg-repeat-x`, `bg-repeat-y`. |

---

### Borders

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Border radius | [border-radius](https://tailwindcss.com/docs/border-radius) | `rounded`, `rounded-sm`, `rounded-md`, `rounded-lg`, `rounded-xl`, `rounded-2xl`, `rounded-3xl`, `rounded-full`, `rounded-none`, `rounded-*` (sides: `rounded-t-*`, `rounded-b-*`, etc.). |
| Border width | [border-width](https://tailwindcss.com/docs/border-width) | `border`, `border-0`, `border-2`, `border-4`, `border-t`, `border-b`, `border-l`, `border-r`, `border-x`, `border-y`. |
| Border color | [border-color](https://tailwindcss.com/docs/border-color) | `border-*` (e.g. `border-gray-200`, `border-primary`, `dark:border-gray-700`). |
| Border style | [border-style](https://tailwindcss.com/docs/border-style) | `border-solid`, `border-dashed`, `border-dotted`, `border-double`, `border-none`. |
| Outline | [outline](https://tailwindcss.com/docs/outline-width), [outline-color](https://tailwindcss.com/docs/outline-color), [outline-offset](https://tailwindcss.com/docs/outline-offset) | `outline`, `outline-0`, `outline-*`, `outline-offset-*`. |

---

### Effects

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Box shadow | [box-shadow](https://tailwindcss.com/docs/box-shadow) | `shadow-sm`, `shadow`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`, `shadow-inner`, `shadow-none`. Custom (e.g. Stitch `shadow-soft`, `shadow-floating`) come from theme. |
| Text shadow | [text-shadow](https://tailwindcss.com/docs/text-shadow) | `shadow-*` for text. |
| Opacity | [opacity](https://tailwindcss.com/docs/opacity) | `opacity-0` … `opacity-100`, `opacity-*`. |
| Mix blend mode | [mix-blend-mode](https://tailwindcss.com/docs/mix-blend-mode) | `mix-blend-*`. |
| Background blend mode | [background-blend-mode](https://tailwindcss.com/docs/background-blend-mode) | `bg-blend-*`. |

---

### Filters (optional for conversion)

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Filter | [filter](https://tailwindcss.com/docs/filter) | `blur-*`, `brightness-*`, `contrast-*`, `grayscale`, `hue-rotate-*`, `invert`, `saturate-*`, `sepia`; `filter`, `filter-none`. |
| Backdrop filter | [backdrop-filter](https://tailwindcss.com/docs/backdrop-filter) | `backdrop-blur-*`, `backdrop-brightness-*`, etc. |

---

### Transitions and animation

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Transition | [transition](https://tailwindcss.com/docs/transition-property), [transition-duration](https://tailwindcss.com/docs/transition-duration), [transition-timing-function](https://tailwindcss.com/docs/transition-timing-function), [transition-delay](https://tailwindcss.com/docs/transition-delay) | `transition`, `transition-none`, `transition-all`, `duration-*`, `ease-*`, `delay-*`. |
| Animation | [animation](https://tailwindcss.com/docs/animation) | `animate-*` (e.g. `animate-spin`, `animate-ping`, `animate-pulse`, `animate-bounce`). |
| Transform | [transform](https://tailwindcss.com/docs/transform), [rotate](https://tailwindcss.com/docs/rotate), [scale](https://tailwindcss.com/docs/scale), [translate](https://tailwindcss.com/docs/translate) | `transform`, `transform-cpu`, `transform-gpu`, `transform-none`; `rotate-*`, `scale-*`, `translate-*`. |

---

### Interactivity

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Cursor | [cursor](https://tailwindcss.com/docs/cursor) | `cursor-auto`, `cursor-pointer`, `cursor-wait`, `cursor-not-allowed`, etc. |
| Pointer events | [pointer-events](https://tailwindcss.com/docs/pointer-events) | `pointer-events-none`, `pointer-events-auto`. |
| Resize | [resize](https://tailwindcss.com/docs/resize) | `resize`, `resize-none`, `resize-y`, `resize-x`. |
| Scroll behavior / snap | [scroll-behavior](https://tailwindcss.com/docs/scroll-behavior), [scroll-margin](https://tailwindcss.com/docs/scroll-margin), [scroll-padding](https://tailwindcss.com/docs/scroll-padding), [scroll-snap](https://tailwindcss.com/docs/scroll-snap-align) | `scroll-auto`, `scroll-smooth`; `scroll-m-*`, `scroll-p-*`; `snap-*`. |
| Touch action | [touch-action](https://tailwindcss.com/docs/touch-action) | `touch-auto`, `touch-none`, `touch-pan-*`, `touch-pinch-zoom`. |
| User select | [user-select](https://tailwindcss.com/docs/user-select) | `select-none`, `select-text`, `select-all`, `select-auto`. |
| Accent color | [accent-color](https://tailwindcss.com/docs/accent-color) | `accent-*`. |
| Appearance | [appearance](https://tailwindcss.com/docs/appearance) | `appearance-none`, `appearance-auto`. |
| Caret color | [caret-color](https://tailwindcss.com/docs/caret-color) | `caret-*`. |

---

### States (hover, focus, etc.)

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Hover / focus / other states | [Hover, focus, and other states](https://tailwindcss.com/docs/hover-focus-and-other-states) | Prefix: `hover:`, `focus:`, `focus-visible:`, `active:`, `disabled:`, `visited:`, `checked:`, `group-hover:`, `peer-*`, `dark:`, `sm:`, `md:`, etc. Examples: `hover:bg-gray-100`, `focus:ring-1`, `focus:ring-primary`, `focus:outline-none`, `dark:bg-gray-800`. |

---

### Tables (if present in Stitch)

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Border collapse | [border-collapse](https://tailwindcss.com/docs/border-collapse) | `border-collapse`, `border-separate`. |
| Table layout | [table-layout](https://tailwindcss.com/docs/table-layout) | `table-auto`, `table-fixed`. |

---

### SVG (if present)

| Category | Official doc | Main utility patterns |
|----------|--------------|------------------------|
| Fill / stroke | [fill](https://tailwindcss.com/docs/fill), [stroke](https://tailwindcss.com/docs/stroke), [stroke-width](https://tailwindcss.com/docs/stroke-width) | `fill-*`, `stroke-*`, `stroke-*` width. |

---

### Forms plugin (optional)

If Stitch or the project uses `@tailwindcss/forms`:

| Topic | Notes |
|-------|--------|
| Form styles | [Forms plugin](https://github.com/tailwindlabs/tailwind-forms) — form-* classes. When converting, replace with framework form components (u-input, el-input, etc.), not raw Tailwind form classes. |

---

### Stitch-specific tokens (common in Stitch HTML)

Stitch often extends Tailwind config with custom theme keys. Treat these as **colors / effects** and map via the target framework’s theme or design tokens:

| Token / pattern | Likely category | Map in framework doc |
|-----------------|-----------------|----------------------|
| `primary`, `bg-primary`, `text-primary` | Colors | Theme primary / activeColor |
| `background-light`, `background-dark` | Background color | Page/card background |
| `card-light`, `card-dark` | Background color | Card background |
| `border-light`, `border-dark` | Border color | Border color |
| `shadow-soft`, `shadow-floating` | Box shadow | Shadow in framework units |
| `rounded-xl`, `rounded-2xl` (theme override) | Border radius | Radius in rpx/rem |
| `dark:` variants | Dark mode | Framework dark theme or media query |

---

## Where each framework defines its mapping

**Framework mappings are independent.** Each skill’s doc is the single source for “Tailwind class X → framework Y”.

| Framework skill | Tailwind → framework mapping doc |
|-----------------|----------------------------------|
| stitch-uviewpro-components | [references/tailwind-to-uviewpro.md](../skills/stitch-uviewpro-components/references/tailwind-to-uviewpro.md) |
| stitch-uview-components | [references/tailwind-to-uview.md](../skills/stitch-uview-components/references/tailwind-to-uview.md) |
| stitch-vue-vant-components | [references/tailwind-to-vant.md](../skills/stitch-vue-vant-components/references/tailwind-to-vant.md) |
| stitch-vue-bootstrap-components | [references/tailwind-to-bootstrap.md](../skills/stitch-vue-bootstrap-components/references/tailwind-to-bootstrap.md) |
| stitch-vue-element-components | [references/tailwind-to-element-plus.md](../skills/stitch-vue-element-components/references/tailwind-to-element-plus.md) |
| stitch-vue-layui-components | [references/tailwind-to-layui.md](../skills/stitch-vue-layui-components/references/tailwind-to-layui.md) |
| stitch-react-components | [references/tailwind-to-react.md](../skills/stitch-react-components/references/tailwind-to-react.md) |
| stitch-shadcn-ui | [references/tailwind-to-shadcn.md](../skills/stitch-shadcn-ui/references/tailwind-to-shadcn.md) |

---

## Usage in skills

- **This doc**: Use when you need to **identify** a Tailwind class or category (and optionally open official docs). Do not put framework-specific conversion tables here.
- **Per-framework**: In each skill’s **SKILL.md**, tell the model to use `references/tailwind-to-<framework>.md` (and `references/stitch-html-patterns.md` where it exists) when converting Stitch HTML. The model consults **this** doc for Tailwind structure and **that** doc for the actual mapping to the target framework.
