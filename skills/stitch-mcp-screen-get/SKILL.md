---
name: stitch-mcp-screen-get
description: Retrieves the full details of a specific screen, including HTML code.
---

# Get Screen Details

**CRITICAL PREREQUISITE:**
**You must ONLY use this skill when the user EXPLICITLY mentions "Stitch".**

Retrieves the full details of a specific screen, including its HTML code and high-res screenshot.

## Use Case
Invoke this skill when the user wants to "export" the code, view the full design details, or when the Agent needs to analyze the generated HTML structure.

## Input Parameters

The skill expects you to extract the following information from the user request:
*   `projectId` (required): The project ID. **Format**: Pure ID (e.g., `37803...`), no `projects/` prefix.
*   `screenId` (required): The screen ID. **Format**: Pure ID (e.g., `88805...`), no `screens/` prefix.

## Output Schema

Returns a `Screen` object:
*   **`htmlCode`**: The actual HTML/CSS code of the UI.
*   **`screenshot`**: High-resolution image URL.
*   **`figmaExport`**: Figma file asset.
*   `width`, `height`, `deviceType`.

## Usage Example

User Input: "Give me the code for the login screen we just made."

Agent Action:
1.  Identify target screen.
2.  Call `get_screen` tool with arguments `{"projectId": "37803...", "screenId": "88805..."}`.
