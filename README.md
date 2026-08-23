# Rally

**v2.0.0** · focus now, get it done

Rally is a single-page calendar and note-taking app built around one idea: capture fast, stay focused, and don't let anything quietly fall through the cracks. It opens straight into a Focus view of *today* instead of a full calendar grid — no digging, no clutter.

## Features

- **Focus-first view** — lands on today's agenda by default; the full month calendar is one toggle away.
- **Notes & Reminders** — two dedicated entry points, each with its own quick-capture form. Reminders carry a time, notes don't. Notes are editable after saving.
- **Auto-rollover & late marking** — unfinished chores and reminders automatically carry forward to the next day instead of disappearing. A reminder still due later today, or overdue from a past day, is flagged in red so it doesn't get lost. Reminders that aren't for today get a small "↗ calendar" button to jump straight to that day.
- **Recurring chores & reminders** — set any chore or reminder to repeat daily, on weekdays, weekly, or monthly from its "↻ repeat" button. New instances generate automatically as they come due.
- **Todo List page** — a clean, organized, collapsible view combining:
  - **Chore Chart** — no date or time required, just today's must-dos. Swipe left (or tap "later") to reschedule an unfinished chore as a future dated reminder instead.
  - **Today's Reminders** — everything due today plus anything overdue, with quick-add built in.
  - **Notes** — a searchable, chronological list of everything you've jotted down.
  - Each section can be collapsed with one tap; the state is remembered.
- **Tags & categories** — tag any entry (e.g. `mechanic`, `farm`, `household`) from a quick-pick popover, then filter the Todo List page down to just one category. The filter row always shows your top 3 most-used tags first, then the rest alphabetically. Tags are entirely optional and can be added or changed after the fact — tapping an open tag button again closes it, same as Cancel.
- **Archive** — deleting an entry or checking something off doesn't erase it right away. It moves to the Archive (one button, top right, with a count badge) where you can restore it or delete it for good. Anything left there is purged automatically after 30 days. A running **lifetime completed** count is also shown there, and survives the 30-day purge.
- **Share / export & Import** — compiles today's chores, reminders, and notes into clean plain text and hands it to your phone's native share sheet (or a copy/SMS fallback on desktop) so you can text your list to yourself or anyone else in seconds. The matching **Import** button parses that same text back in, so you can pull in a list someone shared with you.
- **Dark mode** — toggle in the header; respects your system preference on first visit and remembers your choice after that.
- **Color-coded, distraction-free design** — a warm paper palette (or dark equivalent) with Fraunces + IBM Plex typography; notes, reminders, and chores each get their own accent color so you can scan a day at a glance.

## Tech stack

Pure HTML, CSS, and vanilla JavaScript — no build step, no frameworks, no dependencies. Everything lives in a single `.html` file, and all data is stored in the browser's `localStorage`, so it's fully standalone — no account, no server, no external API calls. Your data stays on whichever device/browser you're using it in.

## Running it

Just open `ledger.html` in a browser (or host it anywhere — GitHub Pages works fine). That's it.

## Changelog

### v2.0.0
- Recurring chores/reminders (daily, weekdays, weekly, monthly)
- Dark mode with system-preference detection
- Collapsible Todo List sections with persisted state
- Archive: lifetime completed counter
- Import: paste a shared list back in
- Tag popovers now toggle closed on a second click
- Tag filter chips ranked by usage (top 3, then alphabetical)
- Today's Reminders now auto-rolls over overdue items, with late/overdue flagging and a jump-to-calendar button
- Notes are now editable after saving

### v1.x (prior, unversioned iterations)
- Standalone `localStorage` persistence (replacing the original Claude-artifact-only storage)
- Tags/categories with quick-pick assignment
- Archive with 30-day auto-purge and restore
- Share/export to plain text with native share sheet + SMS fallback
- Todo List page: Chore Chart, Today's Reminders, Notes
- Chore Chart carry-over and "reschedule as reminder" swipe/button
- Focus-first default view, app renamed to Rally
- Original release: calendar + notes + reminders

## Roadmap ideas

- Real syncing between devices/people (currently "sharing" is text-export only, not live sync — localStorage is per-browser)
