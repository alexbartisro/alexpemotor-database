# Alex Pe Motor — Route Database

Public data repository for [Alex Pe Motor](https://youtube.com/@alexpemotor) — motorcycle routes, GPS tracks and placemarks covering Romania and beyond.

This repo is the data backend for the interactive map at **apm.bartis.ro** (or whichever subdomain is current). The website itself lives in a separate private repo; this one contains only the route files and the manifest that drives the map.

---

## What's in here

```
alexpemotor-database/
├── tracks.json          ← manifest: baseUrl + all tracks + all placemarks
├── routes/              ← one file per route
│   ├── *.gpx            ←   GPS device recordings (includes elevation)
│   ├── *.kml            ←   Google My Maps exports (2D only)
│   └── *.kmz            ←   zipped KML (also supported)
└── placemarks/          ← (future) standalone point-of-interest files
```

### tracks.json structure

```json
{
  "baseUrl": "https://raw.githubusercontent.com/alexbartisro/alexpemotor-database/main",
  "tracks": [
    {
      "id": 1,
      "title": "Vascau → Varfurile",
      "date": "2025-06-15",
      "type": "onroad",
      "file": "routes/vascau-varfurile.kml",
      "youtube": "https://youtu.be/VIDEO_ID",
      "description": "Optional short description."
    }
  ],
  "placemarks": [
    {
      "id": 1,
      "title": "Cheile Turzii viewpoint",
      "lat": 46.5591,
      "lng": 23.6852,
      "type": "viewpoint",
      "description": "Best pull-off on the south side."
    }
  ]
}
```

**Track fields:** `id` (unique int), `title`, `date` (YYYY-MM-DD), `type` (`"onroad"` or `"offroad"`), `file` (relative path), `youtube` (optional), `description` (optional)

Route colours are defined in the website code and applied automatically based on `type` — no colour value is needed in the data. Onroad routes render in blue, offroad in amber.

**Placemark types:** `viewpoint` 👁, `fuel` ⛽, `food` 🍴, `camp` ⛺, `danger` ⚠️, `photo` 📷 — anything else renders as 📍

---

## Contributing

Found a great road and want to add it? Open a pull request.

1. Fork this repo
2. Add your route file to `routes/` — use a lowercase slug filename, e.g. `transalpina-2025.gpx`
3. Add an entry for it in `tracks.json` (pick the next available `id`, set `type` to `"onroad"` or `"offroad"`)
4. Open a PR with a short description of the route

Please keep route files in `.gpx` format where possible — it includes elevation data which powers the chart on the website. `.kml` exports from Google My Maps are also welcome.

---

## Using this data

This data is licensed under **Creative Commons Attribution 4.0 (CC BY 4.0)** — see [LICENSE](LICENSE).

You are free to use, share and adapt the routes for any purpose, including commercial, as long as you provide attribution to:

- **Alex Bartis**
- **Alex Pe Motor** — https://youtube.com/@alexpemotor
- **Comunitatea Alex Pe Motor**

A link back to this repo or the map website is appreciated.

---

## Links

- Map website: https://apm.bartis.ro
- YouTube: https://youtube.com/@alexpemotor
- Main website: https://bartis.ro
