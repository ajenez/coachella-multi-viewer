# Coachella 2026 Multi-Viewer

Watch all 7 Coachella stage streams at once — with live schedules, a full-screen main player, Picture-in-Picture windows, and a visual timeline. No install, no dependencies. Just open `index.html`.

## Features

- **7 simultaneous streams** — Coachella Stage, Outdoor Theatre, Sahara, Mojave, Gobi, Sonora, Quasar
- **Live schedule** — Current artist, set progress bar, and upcoming acts on every card
- **Main view** — Full-screen focused player with draggable PiP windows for 2 other stages
- **Stage switcher** — Thumbnail row at the bottom for instant crossfade switching
- **Full schedule overlay** — Visual timeline grid across all stages, for all 6 festival days
- **Stream URLs pre-loaded** — Weekend 1 IDs are hardcoded; no setup needed
- **Embed error handling** — Detects YouTube embedding blocks and shows a direct YouTube link
- **Keyboard shortcuts** — See below
- **Rebroadcast indicator** — Flags when a stage is replaying earlier content
- **PDT clock** — All times shown in festival time (Pacific Daylight Time)

## Usage

### Easiest — open directly
Download `index.html` and open it in your browser. Everything works from a single file.

> **Note:** YouTube blocks embeds on `file://` origins. If streams don't load, serve the file over HTTP instead:
> ```bash
> cd /path/to/coachella-multi-viewer
> python3 -m http.server 8080
> ```
> Then open `http://localhost:8080` in your browser.

### Via GitHub Pages / any static host
Upload `index.html` to any static host (GitHub Pages, Netlify, etc.) and it will work without the `file://` limitation.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `1` – `7` | Switch to stage 1–7 |
| `M` | Mute / unmute main player |
| `S` | Open / close schedule |
| `Esc` | Back out (close schedule → close modal → return to grid) |

## Updating Stream IDs

Coachella publishes new YouTube stream IDs for each weekend. To update for Weekend 2 (Apr 17–19), find the `DEFAULTS` object near the top of the `<script>` block in `index.html` and replace the video IDs:

```js
// Weekend 1 stream IDs — update these for Weekend 2 (Apr 17–19)
const DEFAULTS = {
  coachella: 'YOUR_ID_HERE',
  outdoor:   'YOUR_ID_HERE',
  sahara:    'YOUR_ID_HERE',
  mojave:    'YOUR_ID_HERE',
  gobi:      'YOUR_ID_HERE',
  sonora:    'YOUR_ID_HERE',
  quasar:    'YOUR_ID_HERE',
};
```

Find the live stream IDs at [youtube.com/@coachella](https://youtube.com/@coachella) — look for the 7 concurrent live videos during the festival. You can paste a full YouTube URL or just the video ID (the 11-character string after `v=`).

> Users who have previously saved custom stream URLs in their browser will need to re-enter them via the **Set Stream URLs** button, as saved values take precedence over defaults.

## Festival Dates

| Weekend | Dates |
|---------|-------|
| Weekend 1 | Apr 10–12, 2026 |
| Weekend 2 | Apr 17–19, 2026 |

On non-festival days the app shows an off-day screen with the next stream date.

## Schedule Data

The full Weekend 1 schedule is included. Weekend 2 schedule data is currently empty — if you have the confirmed times, update the `SCHEDULE` object in `index.html` under the `2026-04-17`, `2026-04-18`, and `2026-04-19` keys. Times use a 24h+ format where post-midnight hours continue past 24 (e.g. `1:00 AM = [25, 0]`).
