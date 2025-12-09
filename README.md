# Story Cards & Storyboard Tool

A drag-and-drop story beat organizer and visual storyboarding tool. No server needed — just open `story-cards.html` in any browser.

---

## Quick Start

1. Open `story-cards.html` in your browser
2. Switch between **Story Beats**, **Swimlanes**, and **Storyboard** views
3. Edit your content (drag to rearrange, click to edit)
4. Click **Export** → Download your work as `.md` or `.json`
5. To continue later: Click **Load** → Select your saved file

---

## Using the Storyboard

### Creating Shots
1. Click the **Storyboard** button in the toolbar
2. **Drag images** from File Explorer directly onto the storyboard — each image becomes a shot
3. Or click the **+ Add Shot** card to add a shot manually

### Editing Shots (Inline)
Click directly on any field to edit it:
- **Shot number** — e.g., "1", "1A", "2B"
- **Description** — What happens in the shot
- **Camera** — e.g., "Wide", "CU", "Dolly in"
- **Duration** — e.g., "5s"

Press **Enter** to save, **Escape** to cancel.

### Saving & Loading Your Storyboard
1. Click **Export** → Downloads `storyboard.json`
2. Save this file somewhere safe (e.g., your project folder)
3. To continue later: Click **Load** → Select your `storyboard.json` file
4. Your shots, images, and all metadata are restored

> **Important**: The JSON file stores image data, so your images will appear when you reload. Keep the JSON file — it's your save file!

---

## Features

### Story Beats View
- **Acts View** — Columns for each act (drag to reorder acts)
- **Swimlane View** — Rows by subplot, columns by act

### Storyboard View
- **Visual timeline** — Arrange shots in sequence
- **Drag & drop images** — Drop images directly from File Explorer onto the storyboard
- **Inline editing** — Click any field to edit shot number, description, camera notes, duration
- **Reorder shots** — Drag shots to rearrange the sequence
- **Multiple images at once** — Drop several images to create multiple shots

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
