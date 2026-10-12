# SwimStopwatch

A phone-only lap stopwatch for swim training: a swimmer roster, named groups,
per-swimmer tap-to-time laps, session history and CSV export. It needs no
board, no server and no connection at the pool - everything runs in the
phone's browser and is stored on the phone.

It is the stopwatch and grouping part of
[SwimPace](https://github.com/MesicBenjamin/SwimPace), without the LED strip.

**Live app:** https://mesicbenjamin.github.io/SwimStopwatch/

## Files

```
SwimStopwatch/
├── index.html             the whole app (HTML, CSS and JS in one file)
├── sw.js                  offline cache, used only when hosted
├── manifest.webmanifest   "Add to Home Screen" name, colours and icon
└── icon.svg
```

`index.html` works on its own. The other three files only add offline use
and a home-screen icon when the folder is hosted.

## Getting it onto a phone

Open https://mesicbenjamin.github.io/SwimStopwatch/ on the phone while
online, then:

- iPhone: Safari → Share → **Add to Home Screen**
- Android: Chrome → menu → **Add to Home screen** / **Install app**

Open it once from the new icon while still online. After that it starts from
the icon and works with no connection.

**As a local file (Android only).** Copy `index.html` to the phone and open
it in Chrome from a file manager. iPhones do not run scripts or keep data for
local HTML files, so on an iPhone use the address above.

## Hosting and updating

The app is served by GitHub Pages straight from the `main` branch of this
repository (Settings → Pages → Deploy from a branch → `main`, `/ (root)`).
Pushing a commit redeploys it in about a minute. A phone picks up the new
version the next time the app is opened while online; if the old version
still shows, close and reopen it.

Any other static https host works the same way - upload the four files.

To try it on a computer: `python3 -m http.server` in this folder, then open
`http://localhost:8000`.

## Using it

A phone that has never used the app starts with a small roster (Matej, Ema,
Lucas, Benjamin, Branimir, Josipa) and a group **All** containing them. This
happens once; swimmers deleted later do not come back.

### Stopwatch tab

- **Group bar** (top) - one button per group. Tapping a group replaces the
  list with that group's swimmers; the loaded group stays highlighted.
- **Swimmer rows** - tap a row to start that swimmer's timer, tap again to
  stop and log the lap. **Split** logs a lap and keeps timing. Each row shows
  the lap count and the last lap time.
- **Bottom bar** - **Start all** starts everyone at the same instant.
  **Start selected** starts only the swimmers whose tick box (left of each
  row) is ticked, then clears the ticks so the next wave can be ticked.
  **Stop all** stops everyone and logs their laps.

### Swimmers tab

- **Swimmers** - search, tick the swimmers that should appear on the
  Stopwatch tab, tap a name to rename it, × to delete. The
  list shows four at a time and scrolls. Add a new swimmer with the form
  below the list.
- **Groups** - tick a set of swimmers, type a group name and **Save**. The
  search matches group names and member names. Each group has a **Show on
  Stopwatch tab** tick box (untick to keep the group but hide its button) and
  × to delete. The list shows four at a time and scrolls.

### Menu (☰, next to the title)

Holds the **session**: its name, **New** to start a named session and
**End** to close it. The active session's name is shown in the header. If no
session is active, one is created automatically on the first lap, so a timed
swim is never lost.

### History tab

Every session with per-swimmer laps, average and best. Each lap is a bar:
its length is relative to that swimmer's slowest lap, and their fastest lap
is green. Export a session as CSV, delete single laps or whole sessions, and
export or import a full backup.

## Where the data lives

Only on that phone, in that browser (`localStorage`). Nothing is uploaded.

- Clearing the browser's site data erases everything - use **History →
  Export backup** now and then, and **Import backup** to restore or to move
  to another phone.
- On iPhone, the home-screen app and Safari keep separate data. Pick one and
  stay with it.
- Two phones do not share data.
