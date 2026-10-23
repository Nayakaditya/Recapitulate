# Recapitulate – Spaced Revision Register

A clean, single-file revision register for exam prep (1-3-7-15-30 day spaced repetition). No login, no server: your entries are saved in your own browser.

## Put it online (GitHub Pages)
1. Create a free GitHub account, then **New repository** → name it `recapitulate` → **Public** → Create.
2. Click **uploading an existing file**, drag in ALL of these files: `index5.html` **renamed to `index.html`** (GitHub Pages opens `index.html` automatically; if you keep the name `index5.html` the site address must end in `/index5.html`), `sw.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png` (replace old ones if they exist), then **Commit changes**.
   If your phone still shows the old version afterwards, close the app fully and reopen it (the cache in `sw.js` can hold the previous version for one visit).
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch `main`, folder `/ (root)` → Save.
4. After 1-2 minutes the site is live at `https://YOUR-USERNAME.github.io/recapitulate/`.

## Google sign-in and cloud backup (optional, free)
Without this, entries live only in the browser you use. With it, your register is saved to your own Google account and comes back after you reinstall the browser or change device. Everything works as before without it.

1. Go to https://console.firebase.google.com → **Add project** (any name; Analytics can be off).
2. **Build → Authentication → Get started → Sign-in method → Google → Enable** → choose a support email → Save.
3. **Build → Firestore Database → Create database** → production mode → pick a region near you.
4. Firestore **Rules** tab: replace the rules with the following and **Publish**. This lets each person read and write only their own data.
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{db}/documents {
       match /users/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```
5. **Authentication → Settings → Authorized domains → Add domain**: `YOUR-USERNAME.github.io`.
6. **Project settings ⚙️ → General → Your apps → Web app (</>)** → register it, then copy the four values `apiKey`, `authDomain`, `projectId`, `appId` into `FIREBASE_CONFIG` near the top of the cloud section in `index5.html` (search for `FIREBASE_CONFIG`). These web config values are not secrets, so it is fine that they sit in a public repository. Never put a client secret, service-account key or password into this file.
7. Upload the file, open the site, then **Settings ⚙️ → Google cloud backup → Sign in with Google**.

How it syncs: after any change it saves to the cloud a few seconds later, and it checks the cloud again each time you return to the app. First sign-in on a device that already has entries merges them with the cloud copy (ticks are combined, same-topic registers are not duplicated). On a new device with no entries it simply downloads your register. Limits: if you change data on two devices at the same moment the later save wins; deleting a register on one device can bring it back after merging with another; the whole register must stay under about 900 KB; on an iPhone installed to the Home Screen the Google pop-up may be blocked, so sign in once from Safari. **Delete all data** also clears the cloud copy while you are signed in.

## Your data
Without cloud backup, entries live in the browser you use. Clearing browser data, using a private window or switching device will not carry them over, so use **Export backup** now and then (Settings ⚙️ → Backup & Restore), and **Import backup** on any device to restore. Importing only adds missing entries.

## Features
- Today, Register and + New tabs; due/overdue counters; search and filters
- Today tab: filter chips (All / Due today / Overdue); the green box counts revisions you finished in the last 24 hours, with "of N" including what is still due; a "Completed in the last 24 hours" list at the bottom shows each tick in the order you did it, with the time, and each item drops off after 24 hours
- Register filter → Revision: Added today, Due today (everything you need to revise now, including overdue), Revised yesterday, Due tomorrow
- + New tab: an "Added today" list so you can see what you already logged, and a yellow warning while typing if the subject and sub-topics look similar to an existing register (also shown when editing one). It only warns; exact duplicates are still blocked
- Subject dropdown (edit the list in Settings), a ⋮ menu on each card (Edit / Delete), delete with a warning pop-up and a 6-second Undo
- Duplicate protection: the same subject + sub-topics can't be created twice
- Gestures (Settings → Gestures & shortcuts, each can be switched off): swipe left/right between tabs; press and hold a folder or register title for its menu; swipe a pop-up down to close it; flick or tap a note to close it; pull-to-refresh is blocked so a stray pull can't reload the page; one-time tips teach each gesture. On a computer: right-click folders and registers, arrow keys / Enter / F2 / Delete / Backspace on folders
- Many folders stay tidy: pinned folders get their own section, folders switch to a compact 3-column layout after 12 (Settings → Folder size: Auto / Large / Compact), and searching also finds folders by name
- Folder menu: right-click a folder (or press and hold on a phone) for Open, Add register here, Rename (rename to an existing name to merge), Change colour, Pin to top, Stats, Properties, Export folder, Reset progress and Delete folder. Rename, reset and delete all have Undo
- Register tab = folders: each subject is a folder tile (coloured, with a register count, due badge and progress bar). Double-click a folder on a computer, or tap it on a phone, to open the registers inside. Use ← or your phone's Back button to return. The search box searches every folder; a filter icon next to it filters by status (All / Active / Completed)
- Fading ink: folders and cards slowly lose their colour the longer revisions are overdue, and regain it as you catch up (switch off in Settings → Preferences)
- Time-capsule notes: when writing a note you can seal it until a later checkpoint and predict how well you'll recall it. A 💌 appears when it is ready, and when you rate that checkpoint the app compares your prediction with the result
- Sticky notes: ⋮ menu → Add note. Pick one of 8 paper styles (post-it, lined, grid, kraft, pinned...). A small note icon appears on the card; tap it to pop the note up, and tap anywhere to close it. Notes are included in backups
- Each subject gets its own colour on top of its cards (change it in Settings → Subjects)
- A checkpoint (+3d, +7d, ...) is locked until its day arrives, so you can't tick revisions early
- Red "Completed" cards after all 5 checkpoints are ticked or 30 days have passed
- Session button creates a ready prompt for the Feynman check, traps, micro-quiz and Hindi mnemonic
- Settings (⚙️): theme (auto/light/dark), accent colour, animations on/off, show/hide completed, sort order, manage subjects, backup, delete all data
- Memory boosters (toggles in Settings): active recall first with a 2-minute timer, Feynman check, why/how questions, Hindi mnemonics, memory palace, and self-rating after each revision (weak topics return the next day). Traps & common errors and the interleaved quiz are always included in Session prompts
- Works on phones, tablets and desktops. On phones the tabs sit in a floating bottom bar with a raised round + (New) button in the middle, Today on the left and Register on the right and you can swipe left/right to change tabs; on larger screens the tabs are at the top

## Share with a friend
Send them the link. Everyone's register is stored in their own browser and is never shared.

## Notifications
- **Bell (top-left):** shows what needs revising right now (due today, overdue, weak spots). Tap an item to jump to its card.
- **Daily reminder (Settings → Notifications):** turn it on, allow notifications when your browser asks, and pick a time. A notification appears at that time if anything is due.
- **Honest limit:** a website can't wake a closed phone browser by itself. Reminders show while the app is open or running in the background (an installed app on Android works best). For alerts that work even when the app is closed, use **Add to calendar (.ics)** in the same section; it adds each upcoming revision to your phone calendar with an alarm.
- **Install on your phone:** Android Chrome: menu → *Install app* / *Add to Home screen*. iPhone: Safari → Share → *Add to Home Screen* (needed before iPhone allows web notifications).
- Also: the tab title and app icon show the due count, and a short summary appears the first time you open the app each day.

## Performance hub
Profile (streak button) → Tools → Performance opens a study analytics hub: a 0-100 study score (due revisions done, on-time rate, recall quality, 14-day consistency), subjects ranked by how much attention they need, a 13-week activity heatmap with weekday and time-of-day patterns, a 14-day workload forecast, and calc accuracy by operation. Timing data (on-time rate, best hour) starts building from the first revision you tick after this update.

## SSC speed maths and Calc mastery
The Calc challenge now has 12 SSC-style operations on top of + − × ÷: squares, cubes, square roots, cube roots, percentages and fractions, tables (11-40), shortcut multiplication (x11, x25, x99, x101...), series sums, HCF, LCM, remainders and averages. Presets (Basics / SSC speed / Everything) pick them quickly, and the five number-size levels scale each drill. Harder operations earn more XP per correct answer.

Calc mastery (Profile → Tools → Calc mastery, or from the Calc challenge screen) counts correct answers per operation. Ranks unlock at 1,000, 1,500, 2,500, 4,000, 6,000, 8,000 and 10,000 correct answers. Each rank gives bonus XP, a surprise gift, a level-up style celebration and a permanent +5% XP on that operation. Small milestones at 100, 250 and 500 give a quick XP boost. Mastery is lifetime: it does not reset with the 60-day cycle. The thresholds are the `MT`, `MXB`, `MS` and `MSB` lists in the script if you want to tune them.

## Weakness heatmap
Profile → Tools → Weakness heatmap (unlocks at level 13) shows every subject against the five checkpoints and picks up subtle weakness, not only topics you rated weak. A cell is scored from: weak ratings, OK-only ratings, recall dropping between checkpoints, topics stuck below strong, predictions that were too confident (time-capsule notes), late revisions, overdue checkpoints, revisions done without a rating and weak spots still open. Chips switch between All signals, Recall only and Timing only. Tap a subject to open its topics, tap any cell for the exact reasons and a tip, or use "Topics to fix first" for a ranked list.

## Calc challenge v3
- **More practice:** Classic rounds of 5, 10, 15, 20, 30 or 50 questions; Sprint (answer as many as you can in 1, 2 or 3 minutes); Survival (3 lives, the timer shortens as you go, +25% XP per answer). The daily calc XP cap is now 300.
- **Daily challenge:** the same 10 mixed questions every day (at your chosen difficulty), with a +20 XP bonus once a day at 70% or better.
- **25 question types:** the earlier 16 plus BODMAS, identity (a² − b²), unit digit, ratio, profit/loss, simple interest, speed (km/h, m/s, trains), number patterns and counting multiples. Operations are grouped (Basic, Powers & roots, Mental tricks, SSC arithmetic, Number system) with Select all per group and a Surprise preset.
- **Learn from mistakes:** a wrong answer shows the right one plus a short shortcut tip for that type. The results screen has a per-operation breakdown, a mistakes review and a Retry mistakes button.
