# Rally

**v2.4.0** · focus now, get it done

Rally is a calm, mobile-first calendar, reminder, chore and note app built around one idea: capture fast, stay focused, and don't let anything quietly fall through the cracks. It is a single static site (no server, no build step) designed to live on your Android home screen.

## Features

**Look and feel (new in 2.4.0)**
- **Calm and neat** — off-white paper (or a true dark theme), one deep-teal accent, soft rounded cards, system fonts, three text sizes. Every color comes from a small set of design tokens, so light/dark is a pure token swap.
- **Bottom tab bar** — Calendar, Todo and Archive are one thumb-tap away. The same layout is used on desktop, in a centered ~640px column.
- **One Add button** — the sticky header always shows **Add**. It opens a sheet: Chore, Reminder or Note, then the relevant form (date, time, repeat and tags are all set right there).
- **Quiet rows, actions on demand** — a row shows just a check circle, the text and small caption info. Tap it to reveal labeled actions: Check off, Move to today, Reschedule, Repeat, Tags, Edit (notes), Delete. On touch screens, swipe left for Check off / Later / Delete.
- **Calm status** — overdue items get a red left edge and an "Overdue" caption; carry-over labels ("from Sat, Oct 3") are plain captions; progress is a thin bar ("3 of 10 done") instead of counters.
- **Settings sheet** — notifications, sound, sync, manage tags, import, share, dark mode and focus mode all live behind the gear icon, so the main screens are just your lists.
- **Motion with manners** — checking something off strikes it through and slides it away; sheets slide up; sections fold. All of it switches off if your device asks for reduced motion.

**Planning**
- **Focus-first Calendar tab** — lands on today's agenda. The month grid sits behind a **Show calendar** button (Rally remembers if you leave it open); picking another day leaves Focus mode so you can see it.
- **Auto-rollover and late marking** — unfinished chores and reminders carry forward instead of disappearing; a reminder past its time or date is flagged in red.
- **Recurring chores and reminders** — daily, weekdays, weekly or monthly; new instances appear as they come due.
- **Todo tab** — Chore Chart (no date or time needed), Today's Reminders (including anything overdue) and Notes (searchable), each collapsible with the state remembered, plus tag filter chips (your top 3 most-used tags first, then alphabetical).
- **Multiple tags per entry** — tag anything with as many tags as you like. **Manage tags** (Settings) renames a tag everywhere or deletes it, always asking first.
- **Reminder notifications (opt-in)** — turn on in Settings. Rally asks the browser for permission once, then notifies when a timed reminder comes due (no duplicates, optional chime). Reminders with no time never notify. Notifications only fire while Rally is open, and the Settings sheet says so.
- **Delete with Undo** — deleting shows an 8-second Undo; everything also stays restorable from the Archive for 30 days.
- **Archive tab** — restore or permanently delete (with a confirmation); items purge 30 days after completion or deletion. A **lifetime completed** counter survives the purge, is kept per device so it adds up across synced devices, and catches up with completed items already on record.

**Sharing and sync**
- **Share / Import** — share today's list as plain text (native share sheet, or copy / SMS fallback). Import shows a live preview ("Found 3 chores, 1 reminder, 2 notes") and adds nothing until you tap Import.
- **Sync between devices** — pair devices (you and your wife, say) through a free jsonbin.io account. Changes push and pull automatically (about every 30 seconds and right after each edit), merged last-edit-wins per item.
- **Instant push (optional)** — add a free Ably key and updates arrive over a live WebSocket instead of waiting for the next poll.

**Accessibility**
- Every control has an accessible name; check circles, calendar days and switches work from the keyboard; Escape closes sheets; keyboard focus shows a clear accent outline; touch targets are at least 44px.

## Install it on your phone (Android home screen)

Rally is a Progressive Web App, so on Android it can be installed like a real app. It needs to be served over **https**, which GitHub Pages does for free.

1. Put these files together in the same folder of your repo (keep the folder structure):
   ```
   Rally.html
   manifest.json
   sw.js
   icons/icon.svg
   icons/icon-192.png
   icons/icon-512.png
   icons/icon-maskable-512.png
   icons/apple-touch-icon.png
   ```
2. Turn on GitHub Pages for the repo (Settings → Pages) and open `https://<you>.github.io/<repo>/Rally.html` in **Chrome on Android**.
3. Chrome menu (⋮) → **Install app** (or **Add to Home screen**). Rally gets its own icon and opens full screen with no browser bar.

Good to know:
- **Offline:** after the first visit Rally opens instantly from a cache and works offline (viewing and adding). Sync catches up when you are back online.
- **Updates:** the cache refreshes in the background, so a new version shows up the *next* time you open the app.
- **Renaming the page:** if you rename `Rally.html` (for example to `index.html`), also change `start_url` and `id` in `manifest.json` and the file list at the top of `sw.js`.
- Opening `Rally.html` straight from your phone's storage still works as a normal page, but installing, offline mode and notifications need the https address.

## Tech stack

Pure HTML, CSS and vanilla JavaScript: no frameworks, no dependencies, no build step. Icons are inline SVG (Lucide-style paths). Local data lives in the browser's `localStorage`, so the app is fully standalone by default. The service worker only caches the app shell; it never touches your data or the sync traffic. Sync is opt-in and talks straight from the browser to jsonbin.io (storage) and, if you add it, Ably (instant push). Notifications use the browser's built-in Notification API.

## A note on syncing

Real syncing needs *some* server in the loop, which no single static file can avoid. Rally uses two free services, each opt-in and independent of the other:

**Storage sync (jsonbin.io)**
1. Create a free account at [jsonbin.io](https://jsonbin.io) and copy your **Master Key** from the API Keys section.
2. On one device open **Settings → Sync**, paste the Master Key and tap **Create a new synced list**. You get a **Sync Code**.
3. On the other device open **Settings → Sync**, paste the same Master Key and the Sync Code, and tap **Join existing list**.

Both devices then sync automatically. That is enough for most use.

**Instant push (Ably), optional**
1. Create a free account at [ably.com](https://ably.com) and copy an API key with publish/subscribe capability.
2. In **Settings → Sync** (after storage sync is set up) paste it into "Ably API Key" and tap **Save & enable instant sync**, on each device.
3. The badge switches from "Polling only" to "Instant" once connected.

Known limitation: permanently deleting an item from the Archive ("Delete forever") does not propagate as a deletion to a device that hasn't synced yet, so it can reappear there on its next sync. Regular deletes sync correctly.

## Changelog

### v2.4.0
- Visual redesign: design-token system (one teal accent, light and dark by swapping tokens), system fonts with a 3-size type scale, inline SVG icons instead of text glyphs, cards with soft shadows
- Bottom tab bar (Calendar / Todo / Archive) on every screen size; Archive is now a tab; content in a centered ~640px column on wide screens
- Single **Add** button in a sticky header opening a Chore / Reminder / Note sheet; the old per-screen add forms and rows are gone
- Rows simplified to check + text + captions; tap for labeled actions; touch swipe-left strip (Check off / Later / Delete)
- Quieter status: red left edge + "Overdue" caption, plain carry-over captions, progress bars instead of counters, friendly empty states with icons everywhere
- Check-off animation (respects reduced-motion), smooth section folding, sheet and tab transitions, accent focus outlines
- Calendar grid refinement: accent ring for today, soft fill for the selected day, smaller dots
- Settings sheet (gear icon) consolidating notifications, sound, sync status, manage tags, import, share, dark mode and focus mode
- PWA: web app manifest, icons (192, 512, maskable, Apple touch), service worker caching the app shell for instant and offline launch, theme-color and mobile meta tags
- No changes to the data model, sync logic or Ably integration

### v2.3.0
- Opt-in notifications for timed reminders (permission requested once, no duplicates, optional chime); alerts fire only while Rally is open in a tab, and the UI says so
- Fixed "Lifetime completed" showing 0 next to completed items: counter now reconciles with completed history on load, is stored per device, and merges across synced devices
- Add forms now include repeat and tags (Calendar reminder form also gets a date field); comma-separated tags with suggestions
- Focus mode shows a "Show calendar" button instead of hiding the calendar; state remembered
- Delete now shows an Undo toast; "Delete forever" asks for confirmation
- Date labels read "Sat, Oct 3" (year added when not current); carry-over help text explains the label; Archive shows purge dates
- Import shows a live preview with per-type counts and requires an explicit Import tap
- "New category…" renamed to "New tag…"
- Popovers and the note Edit button restyled; reschedule shows a readable date
- Touch vs. mouse help text for rescheduling chores
- Accessibility pass and mobile (≤720px) pass

### v2.2.0
- Real-time push via Ably (WebSocket), layered on top of the jsonbin.io sync as an optional "instant sync"; polling remains the fallback
- Multiple tags per entry via a multi-select tag popover, replacing the old one-tag limit
- Tag filtering, ranking and management (rename/delete) updated for multi-tag entries

### v2.1.0
- Real syncing between devices via jsonbin.io (create or join a synced list, background push/pull, last-write-wins merge)
- Manage tags: rename a tag everywhere or delete it, with a confirmation prompt
- "→ later" reschedule button on Today's Reminders, next to "→ today" on overdue items
- Output file renamed from `ledger.html` to `Rally.html`

### v2.0.0
- Recurring chores and reminders (daily, weekdays, weekly, monthly)
- Dark mode with system-preference detection
- Collapsible Todo sections with persisted state
- Archive: lifetime completed counter
- Import: paste a shared list back in
- Tag popovers toggle closed on a second click; tag filter chips ranked by usage
- Today's Reminders auto-rolls over overdue items, with late flagging and a jump-to-calendar button
- Notes editable after saving

### v1.x (earlier, unversioned iterations)
- Standalone `localStorage` persistence, tags, Archive with 30-day auto-purge and restore
- Share/export to plain text with native share sheet and SMS fallback
- Todo List page: Chore Chart, Today's Reminders, Notes; chore carry-over and reschedule
- Focus-first default view; app renamed to Rally; original calendar + notes + reminders release

## Roadmap ideas

- Tombstone-based deletion sync (closes the one known sync gap, noted above)
- Reminder notifications while Rally is closed (needs a service worker plus a push service, which means more setup than a static site)
