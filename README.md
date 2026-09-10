# AdVenture Media — Creative Portfolio

Single-page creative portfolio. Static, zero build step, zero dependencies.

## Deploy

**Vercel:** import the repo. Framework preset = **Other**. No build command, no output dir.
Vercel serves `index.html` at the root automatically.

**Anything else:** it is one HTML file. Drop it on any static host.

## Editing content

Everything lives in two arrays near the top of the `<script>` block in `index.html`.

### Cinema Stage (the pinned hero, one film at a time)
```js
const CHAPTERS = [
  { id:'YOUTUBE_ID', client:'Client Name', metric:'31x Blended ROAS',
    disc:'Performance Video', note:'One or two sentences of craft context.' },
];
```
The section height auto-adjusts: each chapter gets 100vh of scroll.

### Reel Wall (the mosaic below)
```js
const REELS = [
  { id:'YOUTUBE_ID', client:'Client Name', metric:'Metric', span:4, rows:2 },
];
```
- `span` = columns out of 6. `rows` = row span (use for hero tiles).
- `tall:true` forces 4:5, `sq:true` forces 1:1.

`id` is the YouTube video ID only. From `https://youtu.be/sON-woKfynA` the id is `sON-woKfynA`.

## Notes

- Videos are `youtube-nocookie.com` embeds, muted autoplay, controlled via the postMessage API.
- The Reel Wall runs a live-iframe budget (4 on desktop, 2 on touch). Tiles outside that
  budget unmount, so the grid stays smooth at any number of reels.
- postMessage control needs an http/https origin. Over `file://` videos still play muted,
  but hover-to-unmute will not fire. Use `python -m http.server` locally.
- Honors `prefers-reduced-motion`: autoplay and scroll animation are disabled.

## Local preview
```
python -m http.server 4321
```
