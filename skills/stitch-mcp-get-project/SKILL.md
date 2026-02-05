---
name: stitch-mcp-get-project
description: Retrieves the detailed metadata of a specific Stitch project.
---

# Get Stitch Project Details

**CRITICAL PREREQUISITE:**
**You must ONLY use this skill when the user EXPLICITLY mentions "Stitch".**

This skill retrieves the detailed metadata of a specific Stitch project.

## Use Case
Invoke this skill when you need to know the context of a project (e.g., its default theme, device type) before generating new screens, or to verify project existence.

## Input Parameters

The skill expects you to extract the following information from the user request:
*   `name` (required): The resource name of the project. Format: `projects/{project_id}`.

## Output Schema

Returns a `Project` object including:
*   `name`, `title`, `createTime`, `updateTime`
*   `designTheme`: Detailed theme settings.
*   `screenInstances`: List of screen instances currently in the project.

## Usage Example

User Input: "What is the theme of project 'projects/123'?"

Agent Action:
1.  Identify the user wants details of a specific project.
2.  Extract project name "projects/123".
3.  Call `get_project` tool with arguments `{"name": "projects/123"}`.
