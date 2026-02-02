---
name: stitch-ui-design-spec-generator
description: Logic skill that translates vague user requirements into structured Design Specifications (Theme, Color, Typography).
---

# Design Spec Generator

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" or when orchestrating a Stitch design task.

This skill acts as a **Creative Director**. It takes a high-level user request and outputs a structured **Design Specification**.

## Input
*   **User Request**: e.g., "A cyberpunk login page" or "A clean medical dashboard".

## Output Format (JSON)
The skill must produce a JSON block like this:

```json
{
  "theme": "DARK" | "LIGHT",
  "primaryColor": "Hex Code",
  "font": "Font Name",
  "roundness": "High" | "Medium" | "Low",
  "density": "COMPACT" | "COMFORTABLE" | "SPACIOUS",
  "designMode": "WIREFRAME" | "HIGH_FIDELITY",
  "styleKeywords": ["Keyword1", "Keyword2"],
  "deviceType": "MOBILE" | "TABLET" | "DESKTOP" | "SMART_WATCH"
}
```

## Logic Rules
1.  **Analyze Tone**:
    *   "Corporate/Medical/Finance" -> Clean, Blue/Grey, Low Roundness, Inter font.
    *   "Creative/Gaming" -> Dark Mode, Neon colors, High Contrast.
    *   "Lifestyle/Food" -> Warm colors, High Roundness, Serif fonts.
2.  **Determine Device**:
    *   "Dashboard/Admin" -> DESKTOP.
    *   "App/Instagram-like" -> MOBILE.
    *   "Watch Face" -> SMART_WATCH.
    *   Default to MOBILE if unspecified.
3.  **Determine Mode**:
    *   "Sketch/Blueprint/Draft" -> WIREFRAME.
    *   Default to HIGH_FIDELITY.

## Usage
Call this skill *internally* (by thinking) before creating a project or generating a prompt.
