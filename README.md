# SwimStopwatch

A phone-only stopwatch for swim training: a swimmer roster, named groups,
per-swimmer swim and split timing, session history and CSV export. It needs no
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
- **Swimmer rows** - each row has two equal buttons. **Start / Stop** begins
  and ends a *swim*: one whole measurement, for example a 2000 m. **Split**
  marks a *split* inside the running swim, for example every 100 m, while the
  swim keeps timing. Stop also closes the last split, so 20 splits take 19
  taps of Split and one of Stop. While running, the big number is the whole
  swim so far and the small line shows the split number and the previous
  split's time.
- **Bottom bar** (hidden by default, switched on in the menu) - **Start
  all** starts everyone at the same instant.
  **Start selected** starts only the swimmers whose tick box (left of each
  row) is ticked, then clears the ticks so the next wave can be ticked.
  **Stop all** ends everyone's swim.

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

Holds the **Group start and stop** switch, which shows or hides the bottom
bar and the tick boxes on the Stopwatch tab (off by default), and the
**session**: its name, **New** to start a named session and
**End** to close it. The active session's name is shown in the header. If no
session is active, one is created automatically when the first swim is
stopped, so a timed swim is never lost.

### History tab

Every session, with each swimmer's swims. A swim shows its total time and,
if splits were marked, one bar per split: the bar's length is relative to the
slowest split of that swim and the fastest split is green, with average and
best below. × on a swim deletes it. × on a split removes that mark and adds
its time to the next split, which undoes a mistaken Split tap without
changing the total. Sessions can be exported as CSV or deleted, and a full
backup can be exported or imported.

### CSV export

One row per tap - start, every split, stop:

```
session,swimmer,swim,event,split,split_seconds,total_seconds,clock
Morning,Nikša,1,start,,,0.00,07:57:58.10
Morning,Nikša,1,split,1,67.30,67.30,07:59:05.40
Morning,Nikša,1,stop,2,72.56,139.86,08:00:17.96
```

`split_seconds` is the time of that split, `total_seconds` the time since
the swim started, and `clock` the phone's time of day.

## Where the data lives

Only on that phone, in that browser (`localStorage`). Nothing is uploaded.

- Clearing the browser's site data erases everything - use **History →
  Export backup** now and then, and **Import backup** to restore or to move
  to another phone.
- On iPhone, the home-screen app and Safari keep separate data. Pick one and
  stay with it.
- Two phones do not share data.
