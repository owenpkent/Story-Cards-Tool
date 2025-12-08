# Story Cards & Storyboard Tool

A drag-and-drop story beat organizer and visual storyboarding tool. No server needed — just open `story-cards.html` in any browser.

---

## Quick Start

1. Open `story-cards.html` in your browser
2. Drag cards to rearrange, click to edit
3. Switch between **Story Beats**, **Swimlanes**, and **Storyboard** views
4. Click **Export** → Download your work
5. Commit to Git for version control

---

## Features

### Story Beats View
- **Acts View** — Columns for each act (drag to reorder acts)
- **Swimlane View** — Rows by subplot, columns by act

### Storyboard View
- **Visual timeline** — Arrange shots in sequence
- **Image references** — Drag & drop images or paste URLs
- **Shot numbers** — Auto-numbered with manual override
- **Descriptions** — Add shot descriptions, camera notes

### Editing
- **Click card** — Open edit modal
- **Right-click card** — Context menu (edit, duplicate, move, delete)
- **Right-click empty area** — Add card here
- **Drag cards** — Move between acts/subplots
- **Drag acts** — Reorder act columns

### Templates
17 built-in story structures including:
- Three Act, Save the Cat, Story Circle, Hero's Journey
- Romance, Horror, Mystery genre-specific beats
- See `templates/README.md` for full list

### Settings
- **Light/Dark mode** toggle
- **Custom colors** for status, subplots, and accent

---

## Multi-Project Organization

This tool is designed to be deployed per-project. Recommended structure:

```
my-video-project/
├── story-cards.html          # The tool (copy this)
├── project.json              # Project config (auto-created)
├── story-beats/              # Beat card exports
│   ├── story-beats-v1.md
│   └── story-beats-v2.md
├── storyboard/               # Storyboard exports
│   └── storyboard-v1.json
└── images/                   # Reference images for storyboard
    ├── shot-001.jpg
    └── shot-002.png
```

### Deploying to a New Project

1. Copy `story-cards.html` to your project folder
2. Create an `images/` folder for reference images
3. Open the HTML file — it auto-creates config on first export

### Image References

The storyboard stores **file paths** or **URLs** to images, not the images themselves:
- Drag images from your file explorer → stores relative path
- Paste image URL → stores the URL
- Images stay in your project's `images/` folder

This keeps your storyboard file small and Git-friendly.

---

## File Locations

| Location | Purpose |
|----------|---------|
| `story-cards.html` | The tool |
| `project.json` | Project settings |
| `story-beats/` | Versioned story beat exports |
| `storyboard/` | Storyboard exports (JSON) |
| `images/` | Reference images for storyboard |
| `templates/` | Story structure reference docs |

---

## Keyboard Shortcuts

| Action | How |
|--------|-----|
| Zoom in/out | Slider or +/- buttons |
| Close modal | Click outside or Escape |
| Switch view | Click view buttons in toolbar |

---

## Tips

- **No auto-save** — Export when done rearranging
- Browser warns before leaving with unsaved changes
- Use the **Ideas** column as a parking lot for beat cards
- Right-click for quick actions
- Keep images in the `images/` folder for portable projects
- Git commit your exports for version history

---

## Cloud Hosting (Future)

See [CLOUD_HOSTING_PROPOSAL.md](CLOUD_HOSTING_PROPOSAL.md) for plans to add:
- User accounts (Google sign-in)
- Cloud save/sync
- Multi-device access
- Image uploads
