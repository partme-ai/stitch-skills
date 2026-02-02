# Usage Example

## 1. Create a New Project

**User Input:**
> "I want to design a new travel blog app."

**Agent Action:**
```json
{
  "name": "stitch-mcp-project-create",
  "arguments": {
    "title": "Travel Blog App"
  }
}
```

**Output (Success):**
```json
{
  "name": "projects/123456789",
  "title": "Travel Blog App",
  "createTime": "2023-10-27T10:00:00Z",
  "projectType": "TEXT_TO_UI"
}
```

## 2. Handling Response
The Agent should save the returned `name` (Project ID) to its context memory as the `current_project_id` for subsequent calls.
