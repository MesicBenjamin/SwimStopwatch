# SwimStopwatch

A phone-only lap stopwatch for swim training: a swimmer roster, named groups,
per-swimmer tap-to-time laps, session history and CSV export. It needs no
board, no server and no connection at the pool - everything runs in the
phone's browser and is stored on the phone.

It is the stopwatch and grouping part of [SwimPace](../SwimPace/), without
the LED strip.

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

**Hosted (iPhone and Android).** Put this folder on any static https host
(GitHub Pages, Netlify, Cloudflare Pages). Open the address once on the phone
while online, then:

- iPhone: Safari → Share → **Add to Home Screen**
- Android: Chrome → menu → **Add to Home screen** / **Install app**

After that it starts from the home-screen icon and works with no connection.

**As a local file (Android only).** Copy `index.html` to the phone and open
it in Chrome from a file manager. iPhones do not run scripts or keep data for
local HTML files, so on an iPhone use the hosted route.

To try it on a computer: `python3 -m http.server` in this folder, then open
`http://localhost:8000`.

## Using it

- **Swimmers** - add swimmers (name and colour). Ticked swimmers appear on
  the Stopwatch tab. Tick a set, name it and save it as a **group** to load
  the whole set later with one tap.
- **Stopwatch** - tap a swimmer to start their timer, tap again to stop and
  log the lap. **Split** logs a lap and keeps timing. **Start all** gives
  everyone the same start time. A session is created automatically on the
  first tap if none was started, so a timed swim is never lost.
- **History** - every session with per-swimmer laps, average and best.
  Export a session as CSV, delete single laps or whole sessions.

## Where the data lives

Only on that phone, in that browser (`localStorage`). Nothing is uploaded.

- Clearing the browser's site data erases everything - use **History →
  Export backup** now and then, and **Import backup** to restore or to move
  to another phone.
- On iPhone, the home-screen app and Safari keep separate data. Pick one and
  stay with it.
- Two phones do not share data.
