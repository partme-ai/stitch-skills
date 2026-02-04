---
name: stitch-ued-guide
description: A knowledge base of UED Interaction Guidelines and Prompt Engineering best practices for Stitch.
---

# Stitch UED Guidelines

This skill serves as a reference for User Experience Design (UED) guidelines when working with Stitch. It includes interaction principles, visual vocabulary, and prompt engineering strategies.

## Design Modes (Model Selection)

Stitch operates in two distinct modes, which you should choose based on the user's need for speed vs. fidelity:

*   **Standard Mode (Gemini 2.5 Flash)**
    *   **Best for**: Rapid iteration, wireframing, exploring multiple layout ideas quickly.
    *   **Features**: Fast generation, Text-to-UI, Theme editing.
    *   **Use Case**: "Show me 3 different layout options for a login screen."

*   **Experimental Mode (Gemini 2.5 Pro)**
    *   **Best for**: High-fidelity design, complex logic, visual references.
    *   **Features**: Image-to-UI (Sketch/Screenshot upload), richer details, smarter component logic.
    *   **Use Case**: "Turn this napkin sketch into a production-ready dashboard."

## Prompt Engineering Strategy

A perfect Stitch prompt follows this structure:
`[Context & Style]` + `[Layout Structure]` + `[Component Details]` + `[Content & Data]`

### 1. Context & Style
*   **Context**: "Mobile fitness app for gym goers."
*   **Style**: "Dark mode with neon green accents (Cyberpunk). Rounded corners."
*   **Reference**: "Similar to Spotify's dark theme but for fitness."

### 2. Layout Structure
*   **Mobile**: "Bottom navigation bar, scrollable feed."
*   **Desktop**: "Left sidebar navigation, top header, main content area with data grid."
*   **Grid**: "3-column card grid with responsive behavior."

### 3. Component Details
*   **Don't say**: "A list."
*   **Do say**: "A vertical list of 'Workout Cards', each containing a map thumbnail, duration (e.g., '30 min'), and a 'Start' button."

### 4. Content & Data
*   **Realism**: Ask for realistic data. "User 'Alice', 'Morning Yoga', '300 kcal'."
*   **State**: "Active state for the 'Home' tab."

## Visual Vocabulary

Use these terms to control the look and feel:

### Layout Patterns
*   **Hero Section**: Top area with main headline/image.
*   **Split Screen**: Left/Right division (common in Desktop Auth).
*   **Masonry**: Waterfall layout (Pinterest style).
*   **Sidebar Navigation**: Vertical nav on the left (SaaS standard).

### Style Modifiers
*   **Flat**: No shadows, high saturation.
*   **Material**: Shadows, layers, paper metaphor.
*   **Neomorphism**: Soft shadows, extruded shapes.
*   **Glassmorphism**: Blurred transparency, frosted glass.
*   **Brutalism**: Raw, bold, high contrast, large typography.

## Device Guidelines

*   **Mobile**: ~375px width. Focus on thumb-friendly bottom navigation. Vertical scrolling is expected.
*   **Desktop/Web**: ~1440px width. utilize horizontal space. Multi-column layouts.
*   **Tablet**: Hybrid. often resembles desktop but with touch targets.

## Controls & Variants

*   **Variants**: Stitch generates multiple options. You can ask to "Generate variants for the hero section" to A/B test designs.
*   **Controls**: Use the **Interactive Chat** to refine designs ("Make the button blue", "Move the logo to the center").

## Related resources

- **Stitch Effective Prompting Guide**: https://stitch.withgoogle.com/docs/learn/prompting/ — official best practices; consult for up-to-date recommendations.
- **Vague → enhanced prompt**: Use **stitch-ui-prompt-architect** (Path A: enhance vague UI ideas with specificity, UI/UX keywords, DESIGN.md context). Use with **stitch-design-md** for DESIGN.md and **stitch-ui-design-spec-generator** for full flow.
- **Stitch skills in this repo** (prefer these over official): design-md → **stitch-design-md**; enhance-prompt → **stitch-ui-prompt-architect** (two paths + framework contracts); react-components → **stitch-react-components**; stitch-loop → **stitch-loop**; remotion → **stitch-remotion**; shadcn-ui → **stitch-shadcn-ui**. Plus **stitch-mcp-*** (one skill per MCP tool: project-create, project-get, project-list, screen-generate, screen-get, screen-list, screen-refine), **stitch-ui-design-spec-*** (Bootstrap, Element Plus, Layui, uView, uView Pro, Vant), **stitch-ui-designer** (orchestrator), and six Stitch→framework conversion skills (Vue + Element/Bootstrap/Layui/Vant, uni-app + uView/uView Pro). These skills reference each other and the same MCP; use stitch-mcp-{resource}-{action} names (e.g. get_screen → stitch-mcp-screen-get).
