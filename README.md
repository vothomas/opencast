# OpenCast

A free, open-source fishing intelligence app — a Fishbrain-style tool built entirely on public data sources and simple, transparent math instead of paid APIs or a backend.

## What it does

- **Bite Score forecast** — an hourly 0–100 score for the next 7 days, computed from real weather (barometric pressure trend, wind, cloud cover), sunrise/sunset timing, and lunar phase.
- **Moon phase** — computed locally with an astronomical formula, no API needed.
- **Tide times** — optional lookup for US coastal NOAA stations.
- **Spot map** — drop pins for your fishing spots, keep them private or share them to a community map that every user of the app can see.
- **Catch log** — record species, bait, size, rating, and notes per trip, automatically tagged with the Bite Score at the time.
- **Bait Advisor** — a rule-based recommendation engine (not machine learning) that suggests lures, colors, and technique by species, water clarity, season, and current activity level.

## Why it's built this way

Real-time weather, tides, and moon data all come from free, no-API-key, CORS-friendly public services:
- [Open-Meteo](https://open-meteo.com/) — weather forecast + geocoding
- [NOAA CO-OPS](https://tidesandcurrents.noaa.gov/) — US tide predictions
- [OpenStreetMap](https://www.openstreetmap.org/) — map tiles, via [Leaflet](https://leafletjs.com/)

No backend, no database, no signup. It's a single HTML file — open it in any browser and it works.

## What's intentionally *not* included (yet)

Two of the harder Fishbrain-style features aren't in this build, on purpose rather than by accident:

- **Scraping fishing forums / Google Earth imagery.** Doing this legitimately needs a backend crawler, respects each site's terms of service, and often needs permission or a licensed data feed. The community-shared spot map is the honest substitute here — real users contributing real spots, opt-in, inside the app itself.
- **"AI" fish-behavior tracking.** Fishbrain's version of this is trained on millions of real angler reports. Without that dataset, a from-scratch model would just be guessing with extra steps. The Bait Advisor instead uses a transparent rule-based system grounded in well-known species behavior — you can read exactly why it recommends what it recommends. It's a solid v1, and a real roadmap item once the app has enough logged catches to learn from.

## Get this on your phone

There are three ways to use it, from zero-setup to a real installed app icon.

**1. Right now, no setup — inside Claude**
Open this conversation in the Claude app on your phone and use the app directly in the chat. This is the least "app-like" option (it lives inside Claude's interface), but your spots and catch log are saved to your Claude account via Claude's built-in storage, so they'll be there next time you open this chat on any device.

**2. Real installed app icon (recommended)** — takes about 2 minutes:
1. Unzip `opencast-app.zip`.
2. Go to [app.netlify.com/drop](https://app.netlify.com/drop) on a computer and drag the unzipped folder onto the page. No account needed. You'll get a live `https://something.netlify.app` URL.
   *(GitHub Pages works too, and gives you a real repo: create a new repo, upload the unzipped files, enable Pages in repo Settings → Pages → deploy from the main branch.)*
3. Open that URL on your phone.
4. **iPhone (Safari):** tap the Share icon → "Add to Home Screen."
   **Android (Chrome):** tap the ⋮ menu → "Add to Home Screen" / "Install app."
5. You now have a OpenCast icon on your home screen that opens full-screen, no browser bar.

**3. Just open the file directly**
Unzip and open `index.html` in your phone's browser (via AirDrop, email attachment, a cloud drive link, etc.). This works for the forecast, moon phase, spot logging, and catch log. Two things won't work perfectly this way: the "locate me" button needs a secure (https) connection, which a local file doesn't have — search for your location by name instead — and community spot-sharing isn't possible without a real server, so shared spots just save locally on that device. Both work normally once you host it via option 2.

### A note on data storage
This app auto-detects where it's running:
- **Inside Claude.ai** — spots and catches save through Claude's persistent storage, tied to your account.
- **Hosted or opened as a file** — it falls back to your browser's local storage automatically. Your data stays on that one device/browser; there's no account or sync. Community-shared spots specifically need a real backend to be visible to other people, so when running standalone, "shared" spots just behave like private ones (the app tells you this in the checkbox label).



- Auto-detect the nearest NOAA tide station from GPS instead of typing a station ID
- Train a real recommendation model once there's a meaningful volume of community catch-log data
- Add a bathymetry/depth-contour map layer where free data exists
- PWA packaging (installable, offline-capable) for a true mobile-app feel
- Optional lightweight backend if you want spot/catch data to sync across devices instead of living in browser storage

## Running it

The zip bundle (`opencast-app.zip`) contains everything: `index.html`, `manifest.json`, `sw.js`, and app icons. Unzip it and either open `index.html` directly, or host the whole folder on any static file service (GitHub Pages, Netlify, a plain web server) — see "Get this on your phone" below for the installable version. No build step, no dependencies to install.

## License

MIT — do anything you want with it, including selling it. See below.

```
MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
