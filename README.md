# VisSched

A free, account-free **visual schedule and class timer** for K–12 classrooms, special education, therapy sessions, and home routines.

A teacher builds an ordered list of timed activity blocks ("Warm-up 5m / Mini-lesson 10m / Work time 20m / Recap 10m"), then projects the running schedule on a screen at the front of the room. Students see what's happening *now*, what's *next*, and how long is *left* — all in one view, without the teacher having to narrate it.

The whole product ships as a **single self-contained `.html` file** (`vissched.html`, ~250 KB) that runs entirely in the browser. There is no backend, no signup, no database, no analytics, no tracking.

## Try it

**→ [vissched.com](https://vissched.com)**

**iOS app:** coming soon — TestFlight then App Store. Link will be added here at launch.

Or open [`vissched.html`](vissched.html) directly in any modern browser if you'd rather host it yourself.

Schedules persist in `localStorage` and can also be encoded directly into the URL (`?s=…`), so you can bookmark, share, or hand off a schedule just by copying a link.

## Features at a glance

- **12 view modes** for the running timer — schedule list, growing sunflower, rocket launch, melting candle, train to station, and more — so the same timer can read as serious for older students or playful for the K–2 carpet.
- **5 color themes** (Light, Dark, High-contrast, Warm, Cool) and **6 text sizes** sized to be legible from the back row.
- **Optional transition chimes** at 2:00, 1:00, 0:30, and 0:10 remaining.
- **Per-schedule visual settings** — each schedule remembers its own view mode, theme, and text size.
- **Share by URL** — schedules are base64-JSON encoded into `?s=`. No accounts, no server.
- **Offline-capable** — once loaded, the tab can run all day without network.

## Architecture, in one paragraph

VisSched is a vanilla-JS app with a single mutable `state` object and a re-render-on-mutate pattern. Schedules are arrays of `{ id, title, durationMinutes, icon?, description? }` blocks, with optional per-schedule visual `settings`. The timer drives `state.secondsElapsedInBlock` via `setInterval` (schedule-list mode) or `requestAnimationFrame` (visual modes). View modes are dispatched to `renderX(...)` functions that return inline SVG. Themes and text sizes set CSS custom properties on `:root`. State persists to `localStorage`; sharing encodes a v2 object as base64-JSON in `?s=` and decodes it on load.

## Contributing

Issues and pull requests welcome at [github.com/mattnupen/VisSched/issues](https://github.com/mattnupen/VisSched/issues). A few ground rules:

- **No backend, no accounts, no tracking.** Privacy is part of the product.
- **No build step on the shipping path.** `vissched.html` stays a single self-contained file.
- **Don't break the URL share format.** It's the contract that keeps shared links working across versions.

## License

MIT — see [`LICENSE`](LICENSE).
