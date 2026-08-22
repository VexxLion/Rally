# Rally

**focus now, get it done**

Rally is a single-page calendar and note-taking app built around one idea: capture fast, stay focused, and don't let anything quietly fall through the cracks. It opens straight into a Focus view of *today* instead of a full calendar grid — no digging, no clutter.

## Features

- **Focus-first view** — lands on today's agenda by default; the full month calendar is one toggle away.
- **Notes & Reminders** — two dedicated entry points, each with its own quick-capture form. Reminders carry a time, notes don't.
- **Carried-over tracking** — undone reminders from past days automatically surface at the top of today's view, so nothing gets lost. One tap moves them to today.
- **Todo List page** — a clean, organized view combining:
  - **Chore Chart** — no date or time required, just today's must-dos. Swipe left (or tap "later") to reschedule an unfinished chore as a future dated reminder instead.
  - **Today's Reminders** — everything due today, with quick-add built in.
  - **Notes** — a searchable, chronological list of everything you've jotted down.
- **Share / export** — compiles today's chores, reminders, and notes into clean plain text and hands it to your phone's native share sheet (or a copy/SMS fallback on desktop) so you can text your list to yourself or anyone else in seconds.
- **Color-coded, distraction-free design** — a warm paper palette with Fraunces + IBM Plex typography; notes, reminders, and chores each get their own accent color so you can scan a day at a glance.

## Tech stack

Pure HTML, CSS, and vanilla JavaScript — no build step, no frameworks, no dependencies. Everything lives in a single `.html` file.

## Running it

Just open `ledger.html` in a browser. That's it.

## A note on data persistence

This version was built inside a Claude.ai artifact and uses Claude's `window.storage` API to persist entries between sessions. That API only exists inside Claude's artifact environment — if you deploy this file elsewhere (GitHub Pages, your own server, etc.), you'll need to swap the `loadEntries()` / `saveEntries()` functions for something else (e.g. `localStorage` for a quick single-device fix, or a small backend/DB if you want data to sync across devices).

## Roadmap ideas

- Real syncing between devices/people (currently "sharing" is text-export only, not live sync)
- Recurring chores/reminders
- Dark mode
