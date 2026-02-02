---
name: stitch-ued-guide
description: A knowledge base of UED Interaction Guidelines and Prompt Engineering best practices for Stitch.
---

# Stitch UED Guidelines

This skill serves as a reference for User Experience Design (UED) guidelines when working with Stitch. It includes interaction principles, visual vocabulary, and prompt engineering strategies.

## Visual Vocabulary

Use these terms when describing UI elements in prompts:

### Layout Patterns
*   **Hero Section**: Top area with main headline/image.
*   **Split Screen**: Left/Right division (common in Desktop Auth).
*   **Card Grid**: Grid of content cards.
*   **Masonry**: Waterfall layout.
*   **Sidebar Navigation**: Vertical nav on the left.

### Style Modifiers
*   **Flat**: No shadows, high saturation.
*   **Material**: Shadows, layers, paper metaphor.
*   **Neomorphism**: Soft shadows, extruded shapes.
*   **Glassmorphism**: Blurred transparency.
*   **Brutalism**: Raw, bold, high contrast.
*   **Cyberpunk**: Neon, dark mode, futuristic.

## Prompt Engineering Strategy

A perfect Stitch prompt follows this structure:
`[Context & Style]` + `[Layout Structure]` + `[Component Details]` + `[Content & Data]`

### Example
"Mobile screen for a meditation app. Minimalist and Zen aesthetic. Soft pastel colors. (Context & Style)
Layout consists of a clean header, a mood selector, and a session list. (Layout)
The mood selector contains circular icons with emojis. The session list uses card components. (Components)
Use peaceful nature photography for thumbnails. Text should be calming. (Content)"

## Device Guidelines

*   **Mobile**: Width ~375px. Focus on thumb-friendly bottom navigation and vertical scrolling.
*   **Desktop**: Width ~1440px. Use multi-column layouts and sidebar navigation.
