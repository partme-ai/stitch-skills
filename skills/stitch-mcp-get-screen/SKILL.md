---
name: stitch-mcp-get-screen
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

## When the user provides a Stitch design URL

If the user pastes a **Stitch design page link**, parse it to obtain `projectId` and `screenId` so you can call `get_screen` directly without listing projects/screens.

**URL format:**
`https://stitch.withgoogle.com/projects/{projectId}?node-id={screenId}`

**Parsing rules:**
*   **projectId**: The numeric (or string) segment after `/projects/` and before `?`. Example: from `https://stitch.withgoogle.com/projects/3492931393329678076?node-id=375b1aadc9cb45209bee8ad4f69af450` → `projectId = "3492931393329678076"`.
*   **screenId**: The value of the query parameter `node-id`. Same example → `screenId = "375b1aadc9cb45209bee8ad4f69af450"`.

**Agent flow:**
1.  Recognize the URL as a Stitch design link (domain `stitch.withgoogle.com`, path starts with `/projects/`, has `node-id` query).
2.  Extract `projectId` and `screenId` as above.
3.  Call `get_screen` with `{"projectId": "<parsed projectId>", "screenId": "<parsed screenId>"}`.
4.  Use the returned `htmlCode.downloadUrl`, `screenshot.downloadUrl`, and metadata for design-to-code (e.g. stitch-design-md or a framework conversion skill).

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
