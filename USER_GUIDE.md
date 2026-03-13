# Feature Context Hub — User Guide

**Feature Context Hub** is a personal workspace for product designers to track every in-flight feature in one place. It replaces scattered Confluence notes, Slack threads, and browser bookmarks with a single file that keeps context, research, calls, and tasks together — organized per feature, always accessible offline.

---

## Quick Start (Browser Only)

Open the app in your browser — no installation required:

**https://elainezhang86.github.io/feature-hub/**

Your data saves automatically to your browser's localStorage. It stays in your browser — no account, no server, no sign-in.

> **Note:** If you clear your browser data or switch to a different browser or machine, your data will not carry over. For persistent backup across machines, follow the Git Sync setup below.

---

## Git Sync Setup (Recommended)

This setup gives you automatic backups to git — every change you make is committed and pushed every 30 seconds. Your data follows you across machines via `git clone`.

### What you need

- [Node.js](https://nodejs.org) (v18 or later)
- [Git](https://git-scm.com)
- A GitHub account

### Step 1 — Fork the repo

Go to **https://github.com/ElaineZhang86/feature-hub** and click **Fork**. This creates your own copy of the app under your GitHub account.

### Step 2 — Clone your fork

```bash
git clone https://github.com/YOUR_USERNAME/feature-hub.git
cd feature-hub
```

### Step 3 — Start the server

```bash
node server.js
```

You should see:
```
Feature Tracker running at http://localhost:3456
Auto-sync will commit to git every 30 s after a change.
```

### Step 4 — Open the app

Open **http://localhost:3456** in your browser. Keep the terminal open while you work.

### Step 5 — Work normally

Every time you make a change, a 30-second timer starts. When it fires, the server commits your full state to git and pushes to your fork on GitHub.

### Restoring on a new machine

```bash
git clone https://github.com/YOUR_USERNAME/feature-hub.git
cd feature-hub
node server.js
```

Open `http://localhost:3456` — your data loads automatically from the snapshot embedded in `index.html`.

### Daily workflow

1. `node server.js` — run once at the start of your session
2. Open `http://localhost:3456`
3. Work normally — data syncs every 30 seconds
4. Confirm the sync indicator in the sidebar turned green at least once before closing

---

## Navigation

The left sidebar lists every feature with its current status badge. Click any feature to open it. At the top is **Schedule Overview**, a dashboard showing all features at once.

### Sidebar footer

| Icon | Action |
|------|--------|
| ↻ | Force sync to git now (only available with git sync setup) |
| Sun/Moon | Toggle light / dark theme |

---

## Schedule Overview

The landing page. Shows every feature as a card with:

- **Status badge** (Discovery / Design / Dev / QA / Done)
- **Customer** and **due date**
- **Current Focus** — what you are actively working on right now
- **Progress bar** — percentage of To Do tasks marked Done (postponed tasks excluded)

Click any card to jump to that feature's detail page.

---

## Adding a New Feature

Click the **+** button next to "Features" in the sidebar. Fill in:

- Title, icon, status, customer, due date
- Summary, current focus
- Team members

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

- Click **+ Add** and choose Customer Call or Internal Call
- Each call has three tabs: **General Info**, **Call Prep**, **Post Meeting**
- Use **Copy prep prompt to Claude.ai** to generate AI-assisted call prep
- Paste the transcript in Post Meeting and generate an AI summary

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
- Edit or delete pre-loaded specs

---

### Design Files

Links to Figma files, prototypes, or other design assets.

- Add links with **+ Add**
- Direct links open in a new tab

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
