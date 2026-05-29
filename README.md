# RouteDrop

A free, no-account random route generator for running, walking, and cycling. Enter a starting location and a distance — RouteDrop generates a clean loop route on a real street map, ready to export.

**Live:** [routedrop.malvez.org](https://routedrop.malvez.org)

---

## Features

- **Random loop or out-and-back routes** generated using an isodistance triangle algorithm — clean shapes, no tangled crossings
- **Real road routing** via the free OSRM API, snapped to actual streets
- **Distance accuracy** — binary search calibration with 3-bearing fallback keeps generated routes within ~15% of your target distance
- **Steps unit** — set your distance in steps instead of miles/km, with activity-specific stride lengths (run: 3.5ft, walk: 2.5ft)
- **Address autocomplete** powered by OpenStreetMap Nominatim
- **Interactive map** with numbered route markers (S, 1, 2, 3...), built on Leaflet + CARTO Voyager tiles
- **System theme** — automatically follows your device's light or dark mode
- **Save favorite routes** stored locally in your browser
- **Rich link previews** via Open Graph meta tags

## Supported activities

| Activity | Est. Pace | Stride Length |
|----------|-----------|---------------|
| Running  | 10 min/mi | 3.5 ft        |
| Walking  | 20 min/mi | 2.5 ft        |
| Cycling  | 4 min/mi  | N/A           |

## Export options

- **Google Maps** — multi-waypoint directions link
- **GPX file** — import to Strava, Komoot, AllTrails, etc.
- **Garmin TCX** — import via Garmin Connect

## How it works

RouteDrop uses a variation of the **isodistance algorithm** inspired by [Routeshuffle](https://routeshuffle.com):

1. Pick a random compass direction from the start point
2. Place waypoint 2 at `target distance ÷ 3` in that direction
3. Turn ~60° and place waypoint 3, forming a triangle
4. Route start → wp2 → wp3 → start via OSRM
5. Measure actual routed distance — binary search the leg length until within 15% of target
6. If no direction converges within tolerance, try up to 2 more random bearings
7. Draw the result on the map with numbered markers

## Tech stack

- Vanilla HTML/CSS/JS — zero build step, single file
- [Leaflet](https://leafletjs.com/) — map rendering
- [CARTO Voyager](https://carto.com/basemaps/) — map tiles
- [OSRM](https://project-osrm.org/) — free open-source road routing
- [Nominatim](https://nominatim.org/) — free geocoding and address search
- [Outfit](https://fonts.google.com/specimen/Outfit) + [DM Mono](https://fonts.google.com/specimen/DM+Mono) — typography

No API keys required. No backend. No account needed.

## Exporting to Garmin

1. Click **Garmin TCX** to download the `.tcx` file
2. Go to [connect.garmin.com](https://connect.garmin.com) and click the Import button
3. Upload the `.tcx` file — it imports as an Activity
4. In the Garmin Connect app: **Training & Planning → Courses → Send to Device**
5. On your watch (Forerunner 265): **Hold Up → Navigation → Courses → Do Course**

## Known limitations

- Distance accuracy varies in areas with dense street grids, dead ends, water, or highways — occasional outliers can occur
- Walk and Run use the same OSRM routing profile — difference is pace estimate and stride length only
- OSRM is a public free API with no SLA — if it's down, route generation will fail
- Saved routes are stored in `localStorage` and will be lost if browser data is cleared

## Version

v2.11.0 — see [Releases](https://github.com/malvez23/routedrop/releases) for changelog.

## License

MIT
