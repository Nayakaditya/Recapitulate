# Recapitulate – Spaced Revision Register

A clean, single-file revision register for exam prep (1-3-7-15-30 day spaced repetition). No login, no server: your entries are saved in your own browser.

## Put it online (GitHub Pages)
1. Create a free GitHub account, then **New repository** → name it `recapitulate` → **Public** → Create.
2. Click **uploading an existing file**, drag in ALL of these files: `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png` (replace old ones if they exist), then **Commit changes**.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch `main`, folder `/ (root)` → Save.
4. After 1-2 minutes the site is live at `https://YOUR-USERNAME.github.io/recapitulate/`.

If you set up Firebase/Google sign-in earlier, you can delete that Firebase project; this version does not use it.

## Your data
Entries live in the browser you use. Clearing browser data, using a private window or switching device will not carry them over, so use **Export backup** now and then (on computers the 💾 button at the bottom-right, on phones Settings ⚙️ → Backup & Restore), and **Import backup** on any device to restore. Importing only adds missing entries.

## Features
- Today, Register and + New tabs; due/overdue counters; search and filters
- Subject dropdown (edit the list in Settings), a ⋮ menu on each card (Edit / Delete), delete with a warning pop-up and a 6-second Undo
- Duplicate protection: the same subject + sub-topics can't be created twice
- Register tab = folders: each subject is a folder tile (coloured, with a register count, due badge and progress bar). Double-click a folder on a computer, or tap it on a phone, to open the registers inside. Use ← or your phone's Back button to return. The search box searches every folder; a filter icon next to it filters by status (All / Active / Completed)
- Sticky notes: ⋮ menu → Add note. Pick one of 8 paper styles (post-it, lined, grid, kraft, pinned...). A small note icon appears on the card; tap it to pop the note up, and tap anywhere to close it. Notes are included in backups
- Each subject gets its own colour on top of its cards (change it in Settings → Subjects)
- A checkpoint (+3d, +7d, ...) is locked until its day arrives, so you can't tick revisions early
- Red "Completed" cards after all 5 checkpoints are ticked or 30 days have passed
- Session button creates a ready prompt for the Feynman check, traps, micro-quiz and Hindi mnemonic
- Settings (⚙️): theme (auto/light/dark), accent colour, animations on/off, show/hide completed, sort order, manage subjects, backup, delete all data
- Memory boosters (toggles in Settings): active recall first with a 2-minute timer, Feynman check, why/how questions, Hindi mnemonics, memory palace, and self-rating after each revision (weak topics return the next day). Traps & common errors and the interleaved quiz are always included in Session prompts
- Works on phones, tablets and desktops. On phones the tabs sit in a bottom bar (Today | New | Register) and you can swipe left/right to change tabs; on larger screens the tabs are at the top

## Share with a friend
Send them the link. Everyone's register is stored in their own browser and is never shared.

## Notifications
- **Bell (top-left):** shows what needs revising right now (due today, overdue, weak spots). Tap an item to jump to its card.
- **Daily reminder (Settings → Notifications):** turn it on, allow notifications when your browser asks, and pick a time. A notification appears at that time if anything is due.
- **Honest limit:** a website can't wake a closed phone browser by itself. Reminders show while the app is open or running in the background (an installed app on Android works best). For alerts that work even when the app is closed, use **Add to calendar (.ics)** in the same section; it adds each upcoming revision to your phone calendar with an alarm.
- **Install on your phone:** Android Chrome: menu → *Install app* / *Add to Home screen*. iPhone: Safari → Share → *Add to Home Screen* (needed before iPhone allows web notifications).
- Also: the tab title and app icon show the due count, and a short summary appears the first time you open the app each day.
