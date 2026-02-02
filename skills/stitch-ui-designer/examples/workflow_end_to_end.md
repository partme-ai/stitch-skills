# End-to-End Workflow Example

## Scenario: Creating a Pet Adoption App

**User**: "I want to design a pet adoption app called 'PawPals'. Start with a warm, friendly home screen."

### Step 1: Initialize Project
*Orchestrator invokes `stitch-mcp-project-create`*

**Agent Action**:
```json
{
  "name": "stitch-mcp-project-create",
  "arguments": {
    "title": "PawPals"
  }
}
```
**Result**: Project created. ID: `proj_123`.

### Step 2: Design Analysis
*Orchestrator invokes `stitch-ui-design-spec-generator`*

**Agent Action**:
```json
{
  "name": "stitch-ui-design-spec-generator",
  "arguments": {
    "request": "Pet adoption app, warm friendly style"
  }
}
```
**Result**:
```json
{
  "theme": "LIGHT",
  "primaryColor": "#FF9F43", // Warm Orange
  "roundness": "HIGH",
  "font": "Nunito",
  "styleKeywords": ["Friendly", "Playful", "Clean"],
  "deviceType": "MOBILE"
}
```

### Step 3: Prompt Construction
*Orchestrator invokes `stitch-ui-prompt-architect`*

**Agent Action**:
```json
{
  "name": "stitch-ui-prompt-architect",
  "arguments": {
    "userRequest": "Home screen",
    "designSpec": { ... } // JSON from Step 2
  }
}
```
**Result**: "Mobile High-Fidelity home screen for PawPals. Friendly aesthetic. Light mode. Background: Soft cream. Components: 'Find your friend' rounded search bar. 'Categories' horizontal scroll (Dogs, Cats, Birds). 'Featured' vertical list of pet cards with large rounded photos, names, and 'Adopt' pill buttons. Bottom Nav: Home, Favorites, Messages, Profile."

### Step 4: Generation
*Orchestrator invokes `stitch-mcp-screen-generate`*

**Agent Action**:
```json
{
  "name": "stitch-mcp-screen-generate",
  "arguments": {
    "projectId": "proj_123",
    "prompt": "Mobile High-Fidelity home screen for PawPals...",
    "deviceType": "MOBILE",
    "modelId": "GEMINI_3_PRO"
  }
}
```

### Step 5: Presentation
**Agent Response**: "I've created the project 'PawPals' and generated the home screen for you. It features a warm orange theme with rounded, friendly UI elements. [Image Link]"
