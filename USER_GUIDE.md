# Feature Context Hub — User Guide

**Feature Context Hub** is a personal workspace for product designers to track every in-flight feature in one place. It replaces scattered Confluence notes, Slack threads, and browser bookmarks with a single file that keeps context, research, calls, and tasks together — organized per feature, always accessible offline.

---

## User Guide

---

**Getting Started**
- [Why Use Feature Context Hub?](#why-use-feature-context-hub)
- [How to Set Up](#how-to-set-up)

---

**Using the App**
- [Navigation](#navigation)
- [Your Identity](#your-identity)
- [Settings](#settings)
- [Schedule Overview](#schedule-overview)
- [Adding a New Feature](#adding-a-new-feature)
- [Exporting and Importing Features](#exporting-and-importing-features)
- [Feature Detail Page](#feature-detail-page)

---

**Tabs**
- [Context](#context)
- [Domain Knowledge](#domain-knowledge)
- [Feature Brief](#feature-brief)
- [Calls](#calls)
- [Q&A](#qa)
- [Design Spec](#design-spec)
- [Design Files](#design-files)
- [Notes](#notes)
- [To Do](#to-do)

---

**Reference**
- [Deleted Features](#deleted-features)
- [Status Workflow](#status-workflow)
- [Tips](#tips)

---

## Why Use Feature Context Hub?

As a product designer juggling multiple features at once, context is constantly slipping — what was decided and why, what a customer said last week, what's blocked and waiting. Feature Context Hub keeps everything in one place, per feature, so you can pick up any feature in seconds instead of spending 20 minutes reconstructing context from Confluence, Slack, and your notes app.

- **One place per feature** — context, calls, research, tasks, and design files all under one roof
- **No account, no sync service** — runs in your browser or locally, data stays yours
- **Designed for designers** — not a Jira replacement, but a personal layer on top of your existing tools

---

## How to Set Up

There are two ways to use Feature Hub — browser only, or with git sync for backup across machines.

---

### Option A — Browser only (no setup)

Open the app directly:

**https://elainezhang86.github.io/feature-hub/**

Or double-click `index.html` locally.

Data saves automatically to your browser's localStorage. Pick one way to open and stick with it — GitHub Pages and the local file have separate localStorage.

**To keep your data safe:**
1. Always use the same browser — switching browsers means starting fresh
2. Do not clear your browser history or site data — this will wipe your data
3. Do not use private/incognito mode — localStorage does not persist when the window closes

> Data only lives in your browser. If you clear browser data or switch machines, data will not carry over unless you set up git sync below.

---

### Option B — With git sync (recommended for backup)

This setup auto-saves your data to git every 30 seconds, so it follows you across machines.

**What you need:** [Node.js](https://nodejs.org) v18 or later, [Git](https://git-scm.com)

**1. Clone the repo**

```bash
git clone https://github.com/ElaineZhang86/feature-hub.git
cd feature-hub
```

**2. Start the server**

```bash
node server.js
```

You should see:
```
Feature Hub running at http://localhost:3457
Auto-sync will commit to git every 30 s after a change.
```

**3. Open the app**

Open **http://localhost:3457** in your browser. Keep the terminal open while you work.

> **Important:** When using git sync, always open at **http://localhost:3457** — not by double-clicking the file. Double-clicking opens `file://` which has separate storage and your data won't show up.

**Daily workflow with git sync:**
1. `node server.js` — run once at the start of your session
2. Open **http://localhost:3457**
3. Work normally — data syncs every 30 seconds automatically
4. Before closing, confirm the sync indicator turned green at least once

**Restoring on a new machine:**
```bash
git clone https://github.com/ElaineZhang86/feature-hub.git
cd feature-hub
node server.js
```
Open `http://localhost:3457` — your data loads automatically from the snapshot in `index.html`.

**Getting updates:**

> When new features or fixes are published, pull them into your existing clone — no need to re-clone.
>
> ```bash
> git pull
> node server.js
> ```
>
> Your data is not affected. The pull only updates the app code. The app will also show a banner at the top when an update is available.

---

## Common Questions

**Does the app need internet to work?**
No. The app runs entirely on your local machine. When you run `node server.js`, it starts a small local server and your browser connects to it through `localhost`. No internet connection is required.

---

**What is the terminal doing? Can I use other terminals while it's open?**
The terminal is just running the local server. As long as `node server.js` is running somewhere, the app works. You can freely use other terminals or work in other directories — that one just needs to stay open so the server keeps running.

---

**Where is my data stored?**
Your feature data is stored locally in the repo folder. The server periodically commits a snapshot to git automatically, so everything stays backed up. If you ever move to a new machine, clone the repo and run `node server.js` — your data loads automatically.

---

**Do I need to create a git branch?**
If you are just using the tool — adding tasks, notes, calls, domain knowledge — you can stay on `main`. No branch needed.

If you want to experiment with changing Feature Hub itself (modifying the UI, adding functionality), create your own branch so you can test things without affecting the working version.

---

**Will my changes affect the original repo?**
No. Since you cloned it, any changes you make only affect your local copy. The original repo would only change if someone pushed changes back to GitHub, which requires permissions.

---
## Navigation

The left sidebar lists every feature with its current status badge. Click any feature to open it. At the top is **Schedule Overview**, a dashboard showing all features at once.

### Sidebar header

Your name and role appear below the app title. Click them to edit. On first launch you will be prompted to enter them.

### Sidebar footer

| Icon | Action |
|------|--------|
| ↻ | Force sync to git now (only visible when using git sync) |
| ⚙ | Open Settings |

The theme toggle (sun/moon) is in the sidebar header, next to the app title.

---

## Your Identity

On first launch, a welcome modal asks for your name and role. These appear in the sidebar header so you always know whose workspace this is.

- **Edit at any time** — click your name in the sidebar, or go to **Settings → Account**
- Name is required; role is optional
- Identity is stored locally in your browser — it is not synced to git

---

## Settings

Click the **⚙ icon** in the sidebar footer to open Settings.

| Section | What you can do |
|---------|----------------|
| Account | Update your name and role |
| Help | Open the User Guide |
| Appearance | Toggle light / dark theme |

---

## Schedule Overview

The landing page. Shows every feature at a glance. Switch between three views using the toggle in the top-right:

| View | Description |
|------|-------------|
| Cards | Grid of cards, each showing status, customer, current focus, and progress |
| List | Table layout with columns: Feature, Status, Customer, Due Date, Progress |
| Timeline | Kanban board grouped by status |

Each card or row shows:

- **Status badge** (Discovery / Design / Dev / QA / Done)
- **Customer** and **due date**
- **Current Focus** — what you are actively working on right now
- **Progress bar** — percentage of To Do tasks marked Done (postponed tasks excluded)

Click any card to jump to that feature's detail page.

**Drag to reorder** — drag any card or list row to rearrange the feature order. The order is saved automatically and persists across sessions.

---

## Adding a New Feature

Click the **+** button next to "Features" in the sidebar. Fill in:

- Title, icon, status, customer, due date
- Summary, current focus
- Team members

To add a feature from a file exported by someone else, click the **upload icon** next to the + button and select a `.json` export file.

---

## Exporting and Importing Features

Features can be exported as self-contained JSON files and imported into any other Feature Hub instance — useful for sharing context with teammates or backing up individual features.

### Export

Open a feature and click the **download icon** (↓) in the top-right of the feature header. A file named `feature-<title>.json` is saved to your downloads folder.

### Import

Click the **upload icon** (↑) next to the "Features" label in the sidebar. Select a `.json` export file. The feature is added to your workspace with a new ID — your existing features are not affected.

> Exported files contain the full feature definition and all associated state: tasks, calls, Q&A, notes, domain knowledge, and design files.

---

## Feature Detail Page

Each feature has a header with an editable **status dropdown** and **due date picker**, then a **Current Focus ribbon** you can update at any time.

Below that are tabs, each covering a different dimension of the feature.

---

## Tabs

### Context

A reference card showing the core feature brief:
- **Summary** — one-paragraph problem statement
- **Key Decisions** — confirmed design/product decisions
- **Constraints** — known limitations and out-of-scope items
- **Links** — Jira tickets, PRDs, Gong calls, design files
- **Team** — PM, Eng, stakeholders with their roles

---

### Domain Knowledge

A personal notebook for context you have built up over time — edge cases, mental models, integration quirks, anything not in the PRD.

- Click **+ Add** to create a new entry
- Entries are collapsible, editable, and deletable
- Title autosaves when you click away

---

### Feature Brief

Structured background context — architecture decisions, data models, domain deep-dives.

- Click **+ Add** to create a new entry
- Same collapsible/editable/deletable pattern as Domain Knowledge

---

### Calls

Log all calls related to a feature — customer discovery, internal syncs, design reviews.

#### Creating a call

Click **+ Add** and choose **Customer Call** or **Internal Call**. The call opens immediately in edit mode — no modal or popup. Fill in the fields directly:

- **Call Name** — primary identifier
- **Type** — Customer or Internal
- **Category** — Customer Discovery, Design Review, Internal Sync, etc.
- **Status** — Scheduled / Completed / Action Items Pending
- **Date**, **Customer**, **Attendees**, **Notes Link**
- **External Resources** — attach slides, recordings, or docs with a label and URL

Click the **edit icon** (pencil) on any existing call card to switch it to edit mode. When editing, click **Save** to confirm your changes or **Discard** to revert them. Discarding a brand new call removes it entirely.

#### Call status chips

| Status | Color |
|--------|-------|
| Scheduled | Blue |
| Completed | Green |
| Action Items Pending | Yellow |

#### Inside each call — three tabs

**General Info** — call details, attendees, resources

**Call Prep** — structured pre-call preparation:
- Research Questions, Interviewee Background, Warm-up Questions, Topic Questions, Look For / Listen For
- Use **Copy prep prompt to Claude.ai** to generate AI-assisted prep

**Post Meeting** — paste the transcript; generate an AI summary with Claude

---

### Q&A

A question bank with tracked answers.

- Add questions with **+ Add**
- Answers support markdown
- Mark questions as **Resolved** when answered; filter by open/resolved

---

### Design Spec

Links and embeds for your design spec.

- Add spec links with **+ Add**
- Edit or delete existing specs

---

### Design Files

Links to Figma files, prototypes, or other design assets.

- Add links with **+ Add**
- Links open in a new tab

---

### Notes

A free-form scratchpad. Autosaves as you type.

---

### To Do

A unified task list for all work states.

| Status | Meaning |
|--------|---------|
| To Do | Not started |
| Done | Completed |
| Postponed | Deferred — stores a reason |

- Add tasks with **+ Add**
- Postpone a task to record why it is blocked
- Progress bar on Schedule Overview counts Done / (To Do + Done) — postponed tasks excluded

---

## Deleted Features

Deleted features appear in the **Deleted** section at the bottom of the sidebar.

- **Restore** — brings the feature back
- **Delete forever** — permanent removal (confirmation required)

---

## Status Workflow

| Status | Meaning |
|--------|---------|
| Discovery | Researching the problem |
| Design | Actively designing |
| Dev | Handed off to engineering |
| QA | In testing |
| Done | Shipped or closed |

---


## Tips

- **Delete the sample feature** and add your own once you are comfortable with the layout
- **Use Current Focus as a daily intent** — one sentence: what specifically needs to happen today on this feature
- **Log calls even before they happen** — create the call as Scheduled, fill in prep, paste the transcript after
- **Domain Knowledge is for things you learned, not things you were told** — if you had to figure it out, write it down so you never have to again
- **Postpone, don't delete** — if a task is blocked, postpone it with a reason so the context is preserved
- **Export before you hand off** — share a feature's full context with a teammate as a single file
