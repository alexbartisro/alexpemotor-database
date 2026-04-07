# Alex Pe Motor — Route Database

Public data repository for [Alex Pe Motor](https://youtube.com/@alexpemotor) — motorcycle routes, GPS tracks and placemarks covering Romania and beyond.

This repo is the data backend for the interactive map at **apm.bartis.ro** (or whichever subdomain is current). The website itself lives in a separate private repo; this one contains only the route files and the manifest that drives the map.

---

## What's in here

```
alexpemotor-database/
├── tracks.json              ← route manifest: baseUrl + tracks[]
├── placemarks/
│   └── placemarks.json      ← all points of interest (281 entries)
└── routes/                  ← one file per route (101 routes)
    ├── *.gpx                ←   GPS device recordings (includes elevation)
    ├── *.kml                ←   Google My Maps exports (2D only)
    └── *.kmz                ←   zipped KML (also supported)
```

The website fetches both files independently on load:
- `tracks.json` → route list, sidebar, polylines
- `placemarks/placemarks.json` → map pins, popups

### tracks.json structure

```json
{
  "baseUrl": "https://raw.githubusercontent.com/alexbartisro/alexpemotor-database/main",
  "_regions_ref": "Transilvania; Oltenia; Muntenia; ...",
  "tracks": [
    {
      "id": 1,
      "title": "Vascau → Varfurile",
      "date": "2025-06-15",
      "type": "onroad",
      "file": "routes/vascau-varfurile.kml",
      "youtube": "https://youtu.be/VIDEO_ID",
      "description": "Optional short description.",
      "country": ["Romania"],
      "region": ["Crisana"],
      "county": ["Bihor"]
    }
  ]
}
```

**Track fields:**

| Field | Required | Notes |
|-------|----------|-------|
| `id` | ✅ | unique integer, increment from last |
| `title` | ✅ | display name shown in sidebar |
| `date` | ✅ | `YYYY-MM-DD` |
| `type` | ✅ | `"onroad"` or `"offroad"` |
| `file` | ✅ | path relative to `baseUrl` |
| `youtube` | — | full `https://youtu.be/...` URL or empty string |
| `description` | — | short text shown in route detail |
| `country` | ✅ | array, e.g. `["Romania"]` |
| `region` | ✅ | array from: `Transilvania`, `Oltenia`, `Muntenia`, `Moldova`, `Bucovina`, `Dobrogea`, `Crisana`, `Banat`, `Maramures` |
| `county` | ✅ | array of Romanian county names |

Route colours are applied automatically by the website based on `type` — no colour field needed. Onroad renders in blue, offroad in amber.

### placemarks/placemarks.json structure

```json
{
  "placemarks": [
    {
      "id": 1,
      "title": "Cheile Turzii viewpoint",
      "lat": 46.5585,
      "lng": 23.6847,
      "type": "viewpoint",
      "description": "Great pull-off with a view over the gorge.",
      "county": "Cluj",
      "image_url": "https://...",
      "address": "DN75, ...",
      "phone": "+40 ...",
      "website": "https://...",
      "business_name": "...",
      "contact_person": "...",
      "email": "..."
    }
  ]
}
```

**Placemark fields:** `id`, `title`, `lat`, `lng`, `type` and `description` are the core fields. All others are optional and shown in the popup when present.

**Placemark types:** `viewpoint` 👁, `fuel` ⛽, `food` 🍴, `camp` ⛺, `danger` ⚠️, `photo` 📷, `pgl` 🍽️, `school` 🏫, `service` 🔧 — anything else renders as 📍

---

## Contributing

Found a great road and want to add it? Open a pull request.

1. Fork this repo
2. Add your route file to `routes/` — use a lowercase slug filename, e.g. `transalpina-2025.gpx`
3. Add an entry for it in `tracks.json` (pick the next available `id`, set `type` to `"onroad"` or `"offroad"`)
4. Open a PR with a short description of the route

Please keep route files in `.gpx` format where possible — it includes elevation data which powers the chart on the website. `.kml` exports from Google My Maps are also welcome.

**By submitting a pull request or contributing content in any other way, you agree to the contributor licence below.**

---

## Contributor licence

By contributing any content to this repository (route files, placemarks, edits or otherwise), you grant **Alex Bartis**, **Alex Pe Motor** and **Comunitatea Alex Pe Motor** a perpetual, irrevocable, worldwide, royalty-free licence to use, reproduce, modify, distribute and display that content in any form and for any purpose, without restriction. You waive any right to claim payment, royalties or any other form of compensation for your contribution — now or at any point in the future.

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
