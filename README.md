# myMoods

A small, friendly mood diary for your phone. Log how you feel with one tap, see it alongside your biorhythms, and track it against local sunshine and daylight to spot seasonal patterns (such as Seasonal Affective Disorder).

It's a single-page Progressive Web App with no backend, no account and no build step. Everything is stored in the browser's `localStorage` on your device.

## Features

- **Today**: biorhythm curves (physical 23 days, emotional 28, intellectual 33) worked out from your birth date, drawn on a sky that changes from grey to blue with today's sunshine. Drag the chart to move through days and tap a day to see its values. Your logged moods appear as small faces on the chart.
- **One-tap check-ins**: five mood faces. You can also add energy, calm, sleep quality, tags and a note.
- **Today's light**: sunshine hours, day length and how it changed since yesterday, sunrise and sunset, temperature, rain and UV.
- **History**: a monthly calendar coloured by mood, with a sunshine bar for each day. You can edit check-ins or add ones for past days.
- **Insights** (after 7 logged days):
  - mood over time against day length
  - mood vs sunshine and mood vs daylight, with correlations
  - a check of whether your biorhythms actually predict your mood
  - which tags go with better or worse moods
- **Share your mood**: send your latest check-in as a friendly message, such as "Hi Greg! Quick mood update: I'm doing pretty well 🙂". Add a partner's name and WhatsApp number in Settings and the button opens their WhatsApp chat directly. Without a number it opens your phone's share sheet. Notes are never included.
- **Backup**: export and import everything as a JSON file.
- **Offline and installable** when served over HTTPS.

## Running it

The app is just static files in `web/`. Any web server works, for example:

```sh
php -S 0.0.0.0:8080 -t web
```

Then open `http://<your-ip>:8080/`.

### HTTPS matters

Browsers only allow service workers (install to home screen and offline use) and GPS location on **secure origins**: HTTPS or `localhost`. Over plain HTTP on a LAN address the app still works, but:

- it can't be installed and won't work offline
- you set your location by searching for your town instead of using GPS

For testing on a LAN, you can mark the address as secure in Chrome at `chrome://flags/#unsafely-treat-insecure-origin-as-secure`.

## Data and privacy

- Check-ins, settings and cached weather are stored in `localStorage` under keys starting with `mm.`.
- Only two things are sent to [Open-Meteo](https://open-meteo.com/) (free, no API key): your town's coordinates, to look up the weather, and the town name when you search for it. Anything else leaves the device only when you choose to share a mood message yourself.
- Browser storage can be cleared (for example, iOS may clear it for sites that aren't installed), so **export a backup now and then**. The app reminds you after 30 days.

## Files

| File | Purpose |
| --- | --- |
| `web/index.html` | The whole app: HTML, CSS and vanilla JS |
| `web/sw.js` | Service worker: offline app shell, network-first weather, cached fonts |
| `web/manifest.webmanifest` | PWA manifest |
| `web/icon*.svg`, `web/*.png` | App icons |

## Updating

After changing any files, increase `VERSION` in `web/sw.js` (for example `mymoods-v2`) so installed copies pick up the new version.

## A note on biorhythms

Biorhythms are pseudoscience and are included for fun. The Insights screen checks them against your own logged moods, so you can see for yourself whether they mean anything for you.
