---
name: stitch-ui-prompt-architect
description: Logic skill that constructs detailed, structure-aware Stitch Prompts based on Design Specs and User Request.
---

# UI Prompt Architect

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" or when orchestrating a Stitch design task.

This skill acts as a **Senior UX Designer**. It merges the User Request and the Design Spec (from `design-spec-generator`) into a final **Stitch-Ready Prompt**.

## Input
*   **User Request**: The functional requirement (e.g., "Login page with social auth").
*   **Design Spec**: The JSON output from `design-spec-generator`.

## Output Format (String)
A single, descriptive paragraph following this template:

`[Device] [Design Mode] [Screen Type] for [App Category]. [Style Keywords] aesthetic. [Theme] mode. [Density] layout. Background: [Color/Style]. Layout: [Structure Description]. Components: [Detailed Component List]. Content: [Content Strategy].`

## Construction Logic

### 1. Context & Style
Combine `deviceType`, `designMode`, `theme`, and `styleKeywords`.
*   *Example*: "Mobile High-Fidelity login screen. Cyberpunk aesthetic. Dark mode with neon blue accents."
*   *Wireframe Example*: "Mobile Wireframe sketch. Blueprint style. Monochrome."

### 2. Layout Structure
Define the macro layout based on `deviceType`.
*   **Mobile**: Header -> Body (Stack) -> Footer (Nav/Action).
*   **Desktop**: Sidebar/TopNav -> Main Grid -> Widgets.

### 3. Component Details
Translate functional requirements into UI components.
*   "Login" -> Inputs (User/Pass), Button (Primary), Link (Forgot Pass).
*   "Dashboard" -> Cards (KPIs), Charts (Bar/Line), Tables (Data).

### 4. Content
Add specific text examples to make the design realistic.
*   Instead of "Text", use "Welcome back, Agent".

## Example Output
> "Mobile login screen for a Fintech App. Clean minimalist aesthetic. Light mode.
> Layout: Center-aligned vertical stack.
> Header: Brand logo 'PayFast' and 'Welcome' title.
> Form: Input field for 'Email' with mail icon. Input field for 'Password' with eye toggle.
> Actions: Full-width primary blue button 'Sign In'. 'Forgot Password?' link.
> Footer: 'Create Account' link."
