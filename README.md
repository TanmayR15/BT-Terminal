<p align="center">
  <img src="logo.jpg" width="120" alt="BT Terminal logo" />
</p>

<h1 align="center">BT Terminal</h1>

<p align="center">
  A retro pixel-console progress tracker for JEE-style exam prep — Maths, Physics &amp; Chemistry, module by module, exercise by exercise.
</p>

<p align="center">
  <img alt="type" src="https://img.shields.io/badge/type-single--file%20HTML-38B6FF" />
  <img alt="stack" src="https://img.shields.io/badge/stack-vanilla%20JS-4CDE6E" />
  <img alt="storage" src="https://img.shields.io/badge/storage-localStorage-FF5A36" />
  <img alt="build" src="https://img.shields.io/badge/build-none%20required-8F9296" />
</p>

---

## ⚡ What is this?

**BT Terminal** is a single-page study dashboard styled like a retro terminal/arcade console (pixel fonts, scanline grid, chunky drop-shadow buttons). Everything runs client-side in the browser and everything you track is saved to `localStorage` by default — no backend, no account, no sign-up required. An optional passphrase account, backed by a small Cloudflare Worker, lets you sync progress across devices if you want it.

It's built around one idea: **open the app, see exactly where you stand, log a solved exercise in two clicks, close the app.**

## 🧩 Features

- **📚 Subject → Module → Chapter drill-down** for Maths, Physics, and Chemistry, with progress bars and completion stats at every level
- **✅ Exercise tracking** — log solved counts for EX-1 / EX-2 per chapter against known totals
- **🎯 PYQ (Previous Year Questions) tracking** alongside regular exercises
- **📝 Per-chapter notes** — jot down quick notes against any chapter
- **📌 "Today's Focus"** — pin a chapter to the dashboard with quick `+1` buttons and an undo stack
- **🔥 Heatmap view** — a GitHub-style activity heatmap per subject to visualize consistency
- **📅 Calendar & countdowns** — track key dates and see live countdowns to exams/deadlines
- **🕐 Live IST clock** on the dashboard
- **🔁 Revision mode & freeze days** for spaced review and planned breaks
- **⏱️ Pomodoro timer & stats** tracking for focused study sessions, with presets and a mute toggle
- **☁️ Optional passphrase cloud sync** — create a passphrase-based account to sync progress across devices; entirely opt-in, everything still works offline with just `localStorage`
- **💾 Export/backup & import** — export a full backup file, import it back in, and get nudged to export if it's been a while
- **🎨 Distinct color themes** per subject (green/orange/blue) for fast visual scanning

## 🚀 Getting started

No installation, no dependencies, no build tools — it's a hosted single page.

1. Open **[BT Terminal](https://tanmayr15.github.io/BT-Terminal/)**.
2. Start logging progress right away — this works immediately with no account, saved to your browser's `localStorage`.
3. To sync across devices, click **ACCOUNT** in the top-right corner and choose **CREATE NEW ACCOUNT**. You'll get a generated passphrase (or you can set your own) — save it somewhere safe, since it's the only way to log back in and it can't be recovered if lost.
4. On another device, open the same link, click **ACCOUNT → LOG IN**, and enter that passphrase to pull your progress down.

Creating an account is entirely optional; skip it if you only ever use the app on one browser.

## 🗂️ Project structure

```
bt-terminal/
├── BT_Terminal.html   # the entire app: markup, styles, and logic in one file
└── logo.jpg           # app icon / favicon
```

## 💽 Data & privacy

By default, all progress (exercises, PYQs, notes, countdowns, pins, heatmap history, Pomodoro stats) is stored **only in your browser's `localStorage`**, and nothing is sent to a server. Clearing browser data or switching browsers/devices will lose your progress unless you use the export feature — so back up regularly using the in-app **EXPORT NOW** prompt (and use **IMPORT** to restore a backup).

If you want your progress to follow you across devices, you can optionally create a passphrase-based account from the **ACCOUNT** button. This is opt-in only: turning it on sends your backup payload to a small sync API whenever your data changes, keyed to your passphrase, so entering the same passphrase on another device pulls it back down. Skip this if you'd rather keep everything strictly local — the app is fully functional without it.

### ☁️ How the Cloudflare sync works

The sync backend is a [Cloudflare Worker](https://workers.cloudflare.com/), a small serverless function hosted at its own `*.workers.dev` URL, that the page in your browser talks to directly over HTTPS. There's no separate server to run — it's just three endpoints on that Worker:

- `POST /api/register` — generates (or accepts a custom) passphrase and creates a new account
- `POST /api/sync/push` — called automatically ~1.5s after any change, sends your current backup payload (progress, PYQs, notes, calendar, pins, stats) up under your passphrase
- `POST /api/sync/pull` — called when you log in with a passphrase on a device, fetches the latest payload back down

The passphrase itself is your only credential — it's stored in your browser's `localStorage` once you've logged in (so you're not re-entering it every visit) and is what the Worker uses to key your data. Because there's no separate username, treat the passphrase like a password: anyone with it can read or overwrite that account's data.

## 🛠️ Tech stack

- Vanilla JavaScript (no framework, no bundler)
- `VT323` and `Press Start 2P` (Google Fonts) for the terminal/pixel aesthetic
- CSS custom properties for the subject-specific color themes
- Browser `localStorage` for persistence, with an optional Cloudflare Worker backend for passphrase-based cross-device sync

## 🤝 Contributing

Issues and pull requests are welcome — since it's a single HTML file, most changes are a straightforward diff. Please keep the no-build-step philosophy intact.

## 📄 License

© 2026 Tanmay Rastogi. All rights reserved.

This code is made available for personal, local viewing and use only.
You may NOT:
  - Host this application publicly (as-is or modified)
  - Redistribute, sublicense, or share copies of this code
  - Sell or commercially exploit this code or any derivative of it
Any other use requires prior written permission from the author.
