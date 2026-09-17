# Rally

**v2.2.0** · focus now, get it done

Rally is a single-page calendar and note-taking app built around one idea: capture fast, stay focused, and don't let anything quietly fall through the cracks. It opens straight into a Focus view of *today* instead of a full calendar grid — no digging, no clutter.

## Features

- **Focus-first view** — lands on today's agenda by default; the full month calendar is one toggle away.
- **Notes & Reminders** — two dedicated entry points, each with its own quick-capture form. Reminders carry a time, notes don't. Notes are editable after saving.
- **Auto-rollover & late marking** — unfinished chores and reminders automatically carry forward to the next day instead of disappearing. A reminder still due later today, or overdue from a past day, is flagged in red so it doesn't get lost. Overdue reminders show both a "→ today" and a "→ later" button side by side; reminders that aren't for today also get a small "↗ calendar" button to jump straight to that day.
- **Recurring chores & reminders** — set any chore or reminder to repeat daily, on weekdays, weekly, or monthly from its "↻ repeat" button. New instances generate automatically as they come due.
- **Todo List page** — a clean, organized, collapsible view combining:
  - **Chore Chart** — no date or time required, just today's must-dos. Swipe left (or tap "later") to reschedule an unfinished chore as a future dated reminder instead.
  - **Today's Reminders** — everything due today plus anything overdue, with quick-add and a "→ later" reschedule option built in.
  - **Notes** — a searchable, chronological list of everything you've jotted down.
  - Each section can be collapsed with one tap; the state is remembered.
- **Multiple tags per entry** — tag any note, reminder, or chore with as many categories as you want (e.g. `mechanic`, `farm`, `household` on the same item) from a multi-select popover: tap chips to toggle them on/off, type to add a brand-new one, tap **Done** when finished. Each assigned tag shows as its own small pill right on the entry.
- **Tag filtering & management** — the Todo List page's filter row shows your top 3 most-used tags first, then the rest alphabetically; pick one to narrow the whole page to just that category. A dedicated **Manage tags** screen (via "Edit tags" next to the filter row) lets you rename a tag everywhere it's used, or delete it entirely — deleting always asks for confirmation first, since it can't be undone.
- **Sync between devices** — pairs two or more devices (e.g. you and your wife) using a free [jsonbin.io](https://jsonbin.io) account as the relay. One device creates a synced list and gets a Sync Code; any other device pastes in a Master Key + that Sync Code to join. From then on, changes push and pull automatically in the background (roughly every 30 seconds, plus right after you make an edit), merged by last-updated-wins per item.
- **Instant push (optional)** — add a free [Ably](https://ably.com) API key in the Sync panel and updates travel over a live WebSocket connection instead of waiting for the next 30-second poll: as soon as one device saves a change, the other gets notified and re-syncs immediately. Without it, plain polling sync (above) still works fine — this is a pure add-on. See "A note on syncing" below for setup and the one real limitation.
- **Archive** — deleting an entry or checking something off doesn't erase it right away. It moves to the Archive (one button, top right, with a count badge) where you can restore it or delete it for good. Anything left there is purged automatically after 30 days. A running **lifetime completed** count is also shown there, and survives the 30-day purge.
- **Share / export & Import** — compiles today's chores, reminders, and notes into clean plain text and hands it to your phone's native share sheet (or a copy/SMS fallback on desktop) so you can text your list to yourself or anyone else in seconds. The matching **Import** button parses that same text back in, so you can pull in a list someone shared with you. (This is separate from — and lighter-weight than — the Sync feature above: Share/Import is a one-time manual snapshot; Sync keeps devices continuously up to date.)
- **Dark mode** — toggle in the header; respects your system preference on first visit and remembers your choice after that.
- **Color-coded, distraction-free design** — a warm paper palette (or dark equivalent) with Fraunces + IBM Plex typography; notes, reminders, and chores each get their own accent color so you can scan a day at a glance.

## Tech stack

Pure HTML, CSS, and vanilla JavaScript — no build step, no frameworks, no dependencies. Everything lives in a single `.html` file. Local data is stored in the browser's `localStorage`, so the app is fully standalone by default — no account or server required to use it. Sync is opt-in and, when enabled, talks directly to jsonbin.io's REST API from the browser; instant push (also opt-in, layered on top) talks directly to Ably's realtime API over WebSocket. No proxy or backend of ours sits in between either way.

## Running it

Just open `Rally.html` in a browser (or host it anywhere — GitHub Pages works fine). That's it. Sync is optional — see below if you want two devices to share one list.

## A note on syncing

Real syncing needs *some* server in the loop — there's no way around that for a single static HTML file. Rally uses two free services for this, each opt-in and independent of the other:

**Storage sync (jsonbin.io)** — the durable relay both devices read from and write to.
1. Create a free account at [jsonbin.io](https://jsonbin.io) and copy your **Master Key** from the API Keys section of the dashboard.
2. On one device, open Rally's **Sync** button, paste the Master Key, and click **Create a new synced list**. You'll get a **Sync Code**.
3. On the other device, open **Sync**, paste the *same* Master Key and the Sync Code, and click **Join existing list**.

At this point both devices sync automatically every ~30 seconds and right after each edit. That's enough for most use.

**Instant push (Ably) — optional.** If you want updates to appear immediately instead of waiting for the next poll:
1. Create a free account at [ably.com](https://ably.com) and copy an API key with publish/subscribe/presence/history capability.
2. In Rally's Sync panel (once storage sync above is set up), paste it into the "Ably API Key" field and click **Save & enable instant sync**. Do this on each device you want instant updates on.
3. The badge next to that field switches from "Polling only" to "Instant" once connected.

Known limitation: permanently deleting an item from the Archive ("Delete forever") does not propagate as a deletion to a device that hasn't synced yet — it can reappear on that device's next sync. Regular deletes (which move things to the Archive rather than erasing them) sync correctly. There's no way around this without a more complex tombstone system, which felt like overkill for a personal/family list.

## Changelog

### v2.2.0
- Real-time push via Ably (WebSocket), layered on top of the existing jsonbin.io sync as an optional "instant sync" — polling remains the fallback
- Multiple tags per entry (notes, reminders, chores) via a multi-select tag popover, replacing the old one-tag-per-entry limit
- Tag filtering, ranking, and management (rename/delete) all updated to work across multi-tag entries

### v2.1.0
- Real syncing between devices/people via jsonbin.io (Sync button: create or join a synced list, background push/pull, last-write-wins merge)
- Manage tags: rename a tag everywhere it's used, or delete it — deletion always prompts for confirmation
- Added a "→ later" reschedule button to Today's Reminders, placed next to "→ today" on overdue items
- Output file renamed from `ledger.html` to `Rally.html`

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

- Tombstone-based deletion sync (closes the one known gap in sync, noted above)
