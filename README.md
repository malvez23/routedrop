# RouteDrop

A free, no-account random route generator for running, walking, and cycling. Enter a starting location and a distance — RouteDrop generates a clean loop route on a real street map, ready to export.

**Live:** [malvez23.github.io/routedrop](https://malvez23.github.io/routedrop)

---

## Features

- **Random loop or out-and-back routes** generated using an isodistance triangle algorithm — clean shapes, no tangled crossings
- **Real road routing** via the free OSRM API, snapped to actual streets
- **Distance accuracy** — binary search calibration keeps generated routes within ~15% of your target distance
- **Address autocomplete** powered by OpenStreetMap Nominatim
- **Interactive map** with directional arrows, built on Leaflet + OpenStreetMap tiles
- **System theme** — automatically follows your device's light or dark mode
- **Save favorite routes** stored locally in your browser
- **Export options:**
  - Google Maps (multi-waypoint directions link)
  - GPX file (Strava, Komoot, AllTrails, etc.)
  - Garmin TCX (import via Garmin Connect)
  - Share link

## Supported activities

| Activity | Estimated pace |
|----------|---------------|
| Running  | 10 min/mile   |
| Walking  | 20 min/mile   |
| Cycling  | 4 min/mile    |

## How it works

RouteDrop uses a variation of the **isodistance algorithm** — the same approach used by [Routeshuffle](https://routeshuffle.com):

1. Pick a random compass direction from the start point
2. Place waypoint 2 at `target distance ÷ 3` in that direction
3. Turn ~60° and place waypoint 3, forming a triangle
4. Route start → wp2 → wp3 → start via OSRM
5. Measure actual routed distance — if more than 15% off target, binary search the leg length and re-route
6. Draw the result on the map with directional arrows

This guarantees a clean loop with no crossings and a result close to your requested distance.

## Tech stack

- Vanilla HTML/CSS/JS — zero build step, single file
- [Leaflet](https://leafletjs.com/) — map rendering
- [OpenStreetMap](https://www.openstreetmap.org/) — map tiles
- [OSRM](https://project-osrm.org/) — free open-source road routing
- [Nominatim](https://nominatim.org/) — free geocoding and address search
- [Outfit](https://fonts.google.com/specimen/Outfit) + [DM Mono](https://fonts.google.com/specimen/DM+Mono) — typography

No API keys required. No backend. No account needed.

## Usage

Open [malvez23.github.io/routedrop](https://malvez23.github.io/routedrop) in any browser — works on desktop and mobile Safari.

To run locally, just open `index.html` in a browser. All external dependencies are loaded via CDN.

## Exporting to Garmin

1. Click **Garmin TCX** to download the `.tcx` file
2. Go to [connect.garmin.com](https://connect.garmin.com) and click the Import button
3. Upload the `.tcx` file — it imports as an Activity
4. In the Garmin Connect app: **Training & Planning → Courses → Send to Device**
5. On your watch (Forerunner 265): **Hold Up → Navigation → Courses → Do Course**

## Known limitations

- Distance accuracy varies in areas with dense street grids, dead ends, water, or highways — occasional outliers of ±30% can occur
- Apple Maps export not supported — Apple Maps doesn't accept loop routes via URL
- OSRM is a public free API with no SLA — if it's down, route generation will fail
- Saved routes are stored in `localStorage` and will be lost if browser data is cleared

## License

MIT
