# Usage Example

## Scenario: Creating a "Music App Designer" Skill

**User Request**:
> "I want to add a skill to help design music player apps with Stitch."

**Agent Action**:
1.  **Analyze**: Domain = "Music App". Skill Name = `stitch-ui-music-designer`.
2.  **Scaffold**: Create `skills/stitch-ui-music-designer`.
3.  **Implement `SKILL.md`**:

```markdown
---
name: stitch-ui-music-designer
description: Specialized prompt architect for Music Player and Streaming screens.
---

# Music Screen Designer

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" or when orchestrating a Stitch design task.

This skill helps you construct high-quality prompts for Music App flows (Player, Playlist, Library).

## Prompt Template

```text
[Device] music player screen for [App Name]. [Style] aesthetic.
Background: [Blurred Album Art / Gradient].
Layout: Vertical stack.
Header: "Now Playing" title, Down arrow (collapse).
Hero: Large Album Art (Square/Rounded) with shadow.
Track Info: Song Title (Bold), Artist Name (Subtle).
Controls:
- Scrubbing Bar (Progress).
- Play/Pause (Large, Centered).
- Previous/Next buttons.
- Shuffle/Repeat toggles.
Footer: Lyrics / Up Next queue.
```
```

4.  **Implement `examples/usage.md`**:

```markdown
# Usage Example

## 1. Spotify-like Player
**User**: "Dark mode player like Spotify."
**Output**: "Mobile music player screen... Dark mode... Black background... Green accent controls..."
```

5.  **Validation**:
    *   Does it have the Stitch Constraint? Yes.
    *   Does it separate design from execution? Yes (it returns a prompt template).
