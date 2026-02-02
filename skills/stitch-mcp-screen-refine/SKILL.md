---
name: stitch-mcp-screen-refine
description: Logic skill that translates user feedback into a refinement prompt for existing screens. Use when user wants to change/edit a generated design.
---

# Stitch Screen Refine

**CRITICAL PREREQUISITE:**
**You must ONLY use this skill when the user EXPLICITLY mentions "Stitch".**

This skill handles the **"Edit Loop"**. It takes an existing screen context and a user's change request, and outputs a new Prompt to regenerate/refine the screen.

## Input
*   **Original Prompt**: The prompt used to generate the current screen.
*   **User Feedback**: e.g., "Make the button bigger", "Change background to red", "Remove the footer".

## Output Format (String)
A new, complete Stitch Prompt that incorporates the changes.

## Logic Rules

1.  **Preserve Core Context**: Keep the original Device, App Category, and Layout unless explicitly changed.
2.  **Apply Modifiers**:
    *   *Color Change*: Replace color keywords. (e.g., "Neon blue" -> "Neon red").
    *   *Layout Change*: Modify the "Layout" section.
    *   *Component Change*: Add/Remove items in the "Components" section.
3.  **Refinement Keywords**: Add "Refined version", "Updated design" to the start to hint the model.

## Usage Example

**Original**: "Mobile login screen. Dark mode. Blue button."
**Feedback**: "Change button to green."
**Output**: "Refined Mobile login screen. Dark mode. **Green** button. [Rest of prompt...]"
