# kaleidoscope-video-maker

Single-file in-browser tool: any image → animated kaleidoscope → WebM video export. Pure client-side, deployed to GitHub Pages at `https://abobabo91.github.io/kaleidoscope-video-maker/`.

## Critical rules

- NEVER introduce a build step, bundler, or dependency. The project is **intentionally single-file** — everything (UI + canvas math + WebM encoder via `MediaRecorder`) lives in `index.html`. Don't split it.
- NEVER add a backend or upload step. The "no upload, no backend" property is the value proposition — images stay client-side.
- Browser compatibility floor: any modern Chromium/Firefox with `MediaRecorder` support. If you add APIs, verify they're available there.

## Stack & run

- Pure HTML + canvas + vanilla JS + `MediaRecorder` for WebM encoding
- Run locally: open `index.html` directly in a browser (no server needed)
- Deploy: push to `main` → GitHub Pages serves from repo root

## Where things live

- `index.html` — everything (UI, kaleidoscope rendering, video export logic)
- `screenshots/` — README images

## Gotchas

- Video export uses `MediaRecorder` with WebM. If a user wants MP4, that's a browser-codec limitation, not a code one — document, don't try to ship ffmpeg.wasm just for that.
- Resolution + bitrate combos in the export UI: 720p/1080p/2K/4K × 15–60 fps × 1–20 Mbps. Verify any new combo before adding (some browsers cap above certain bitrates).
- Pan/zoom of the source image is a separate gesture from the symmetry-axis controls — keep them independent in the UI logic.
