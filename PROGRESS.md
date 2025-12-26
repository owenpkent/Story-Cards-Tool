# Story Cards Tool — Progress & Next Steps

**Last Updated:** December 25, 2025

---

## Project Overview

A browser-based story beat organizer and visual storyboarding tool. Supports drag-and-drop editing, multiple views (Acts, Swimlanes, Storyboard), and exports to Markdown/JSON.

**Goal:** Deploy to Netlify and create an MCP server that can ingest markdown and generate coherent timelines/visuals.

---

## Completed ✅

### Core Application
- [x] Single-file HTML app (`story-cards.html`) — works offline
- [x] **Story Beats View** — Kanban-style cards organized by acts
- [x] **Swimlane View** — Rows by subplot, columns by act
- [x] **Storyboard View** — Visual timeline with shot cards and image support
- [x] Drag-and-drop for cards, acts, and shots
- [x] Inline editing for all fields
- [x] Right-click context menus
- [x] Light/dark mode toggle
- [x] 17 built-in story templates (Three Act, Save the Cat, Hero's Journey, etc.)

### Import/Export
- [x] Export to Markdown (`.md`) and JSON (`.json`)
- [x] Load from local files
- [x] Image drag-and-drop (stores as base64 locally)
- [x] localStorage session persistence

### Cloud Features (Phase 1 MVP)
- [x] Firebase Authentication (Email/Password)
- [x] Firestore cloud save/load
- [x] User-specific project storage (`users/{userId}/projects/default`)
- [x] Auth state persistence across refreshes

### Documentation
- [x] README with quick start and features
- [x] CLOUD_STATUS.md — cloud implementation status
- [x] CLOUD_HOSTING_PROPOSAL.md — original cloud plans
- [x] MCP_SERVER_DESIGN.md — detailed MCP architecture spec
- [x] CONSTELLATION_INTEGRATION_GUIDE.md — meta-project integration
- [x] AGENTIC_WORKFLOW_OPTIONS.md — AI workflow comparison

---

## In Progress 🔄

### Netlify Deployment
- [ ] **Prepare for deployment** — Currently a single HTML file, ready for static hosting
- [ ] Configure Firebase authorized domains for Netlify URL
- [ ] Set up Firestore security rules for production
- [ ] Test cloud auth on deployed URL

### MCP Server ✅ COMPLETE
- [x] Created `story-cards-mcp/` project with TypeScript
- [x] Implemented resources: `storyboard://current`, `storyboard://shots`, `storyboard://beats`, `storyboard://acts`
- [x] Implemented tools: `add_shot`, `edit_shot`, `delete_shot`, `reorder_shots`, `add_beat`, `edit_beat`, `delete_beat`, `move_beat`, `add_act`, `import_markdown`, `export_storyboard`
- [x] Built and tested

**To configure in Windsurf:** Settings → MCP Servers → Add:
```json
{
  "story-cards": {
    "command": "node",
    "args": ["C:/Users/Owen/dev/Story-Cards-Tool/story-cards-mcp/dist/index.js"],
    "env": {
      "STORYBOARD_PATH": "C:/Users/Owen/dev/Story-Cards-Tool/storyboard.json"
    }
  }
}
```

---

## Next Steps — Detailed Tasks

### Phase 1: Netlify Deployment (Priority: HIGH)

Deploy the existing app to get a live URL.

| Task | Subtasks | Est. Time |
|------|----------|-----------|
| **1.1 Deploy to Netlify** | - Create Netlify site from GitHub repo<br>- Set subdomain (e.g., `story-cards.netlify.app`)<br>- Verify static HTML loads correctly | 10 min |
| **1.2 Configure Firebase** | - Add Netlify domain to Firebase Auth authorized domains<br>- Update Firestore security rules for production<br>- Test sign-in on live URL | 15 min |
| **1.3 API Key Security** | - Restrict API key in Google Cloud Console (HTTP referrers)<br>- Limit to Firebase APIs only | 10 min |

---

### Phase 2: MCP Server Implementation (Priority: HIGH)

Create an MCP server so AI assistants can directly read/write storyboards.

| Task | Subtasks | Est. Time |
|------|----------|-----------|
| **2.1 Create MCP Server Project** | - Set up `story-cards-mcp/` folder<br>- Initialize Node.js project with TypeScript<br>- Install `@modelcontextprotocol/sdk` | 30 min |
| **2.2 Implement Resources** | - `storyboard://current` — full storyboard<br>- `storyboard://shots` — shot list<br>- `storyboard://beats` — story beats<br>- `storyboard://acts` — act structure | 1 hr |
| **2.3 Implement Core Tools** | - `add_shot`, `edit_shot`, `delete_shot`<br>- `add_beat`, `edit_beat`, `move_beat`<br>- `add_act`, `reorder_shots` | 2 hr |
| **2.4 File Storage Layer** | - Read/write `storyboard.json`<br>- Path configuration via env vars | 30 min |
| **2.5 IDE Configuration** | - Add MCP config for Windsurf/Cascade<br>- Test basic tool calls | 15 min |

---

### Phase 3: Markdown-to-Timeline Feature (Priority: MEDIUM)

The core ask: **Feed markdown → Generate visual timeline.**

| Task | Subtasks | Est. Time |
|------|----------|-----------|
| **3.1 Markdown Parser** | - Parse structured markdown (headings = acts, bullets = beats)<br>- Extract metadata (status, subplot tags)<br>- Handle various markdown formats | 2 hr |
| **3.2 Import UI** | - Add "Import Markdown" button to toolbar<br>- File upload or paste modal<br>- Preview parsed structure before import | 1 hr |
| **3.3 MCP Tool: `import_markdown`** | - Accept raw markdown text<br>- Parse and populate storyboard<br>- Return summary of created items | 1 hr |
| **3.4 Timeline Visualization** | - Add horizontal timeline view (beyond current storyboard)<br>- Zoomable timeline with beat markers<br>- Color coding by act/subplot | 3 hr |

**Markdown Format Example (supported):**
```markdown
# Act I: Setup
## The Ordinary World
The hero in their normal life.
- Status: draft
- Subplot: A-plot

## Call to Adventure
Something disrupts the status quo.
```

---

### Phase 4: GitHub Integration (Priority: LOW)

Enable syncing storyboards with GitHub repos.

| Task | Subtasks | Est. Time |
|------|----------|-----------|
| **4.1 GitHub OAuth** | - Add GitHub sign-in option<br>- Request repo access scope | 1 hr |
| **4.2 Repo Sync** | - Push/pull `storyboard.json` to repo<br>- Commit with meaningful messages | 2 hr |
| **4.3 Watch for Changes** | - Detect changes in repo<br>- Optional: Auto-reload on file change | 1 hr |

---

### Phase 5: Browser Sync (Optional)

Real-time sync between MCP edits and browser UI.

| Task | Subtasks | Est. Time |
|------|----------|-----------|
| **5.1 WebSocket Server** | - Add WS server to MCP (port 8765)<br>- Broadcast on storyboard changes | 30 min |
| **5.2 Browser Listener** | - Add WS client to `story-cards.html`<br>- Auto-reload data on `storyboard_updated` event | 30 min |

---

## Architecture Decision: MCP Approach

Two options for MCP integration:

### Option A: Local MCP Server (Recommended)
- Runs on your machine
- Reads/writes local `storyboard.json` files
- Works with Windsurf, VS Code + Continue, Claude Desktop
- **No cloud dependency** — fully offline capable

### Option B: Cloud API + MCP Proxy
- Hosted API on Netlify/Vercel
- MCP server proxies to cloud API
- Enables remote access from any device
- Requires Firebase integration for data

**Recommendation:** Start with **Option A** for immediate AI integration, add cloud API later if needed.

---

## Quick Commands

**Deploy to Netlify (via CLI):**
```powershell
# If Netlify CLI installed
netlify deploy --prod --dir .
```

**Start MCP Server (after implementation):**
```powershell
cd story-cards-mcp; npm run start
```

**Test MCP locally:**
```powershell
npx @anthropic-ai/mcp-inspector story-cards-mcp
```

---

## Blockers & Questions

1. **Image storage:** Currently base64 (too large for Firestore). Phase 3 planned Firebase Storage integration.
2. **Multi-project support:** Currently single "default" project per user. Phase 2 of cloud features.
3. **MCP hosting:** For GitHub integration, MCP needs access to repo files — local server or GitHub App?

---

## Summary

| Area | Status |
|------|--------|
| Core App | ✅ Complete |
| Cloud Auth/Save | ✅ Complete |
| Netlify Deployment | 🔲 Ready to deploy |
| MCP Server | ✅ Complete |
| Markdown Import | ✅ Built into MCP (`import_markdown` tool) |
| **Accessibility (WCAG)** | ✅ Phases 1-5 complete — see [ACCESSIBILITY.md](ACCESSIBILITY.md) |
| Timeline Visualization | 🔲 Not started |
| GitHub Integration | 🔲 Planning |

### Accessibility Implementation (Dec 25, 2025)
- ✅ Semantic landmarks (`<header>`, `<nav>`, `<main>`, `<section>`)
- ✅ Skip link for keyboard users
- ✅ ARIA labels on all buttons and controls
- ✅ View tabs with `role="tab"` and `aria-selected`
- ✅ Cards/shots: `tabindex`, `role="article"`, keyboard handlers
- ✅ Keyboard reordering: `Ctrl+Arrow` for cards and shots
- ✅ Toggle switch: `role="switch"`, `aria-checked`, keyboard support
- ✅ Modal focus management and announcements
- ✅ Live region for screen reader announcements
- ✅ Visible focus indicators (`:focus-visible`)

**Remaining:** Status text badges (not color-only), context menu keyboard support.

**Immediate Next Action:** Deploy to Netlify.
