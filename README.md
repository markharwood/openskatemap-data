# openskatemap-data

A list of global skatepark names and locations as an open dataset.

This repository is the open data layer of [sk8tags.com](https://sk8tags.com) —
a community-maintained map of the world's skateparks. The location data lives
here, in the open, under the same license as OpenStreetMap, so anyone can use
it, build on it, or fork it.

## What's in here

- **`parks.geojson`** — every real skatepark we know about, as a GeoJSON
  `FeatureCollection`. GitHub renders it as an interactive map above (scroll up
  and click the file). Each park has a name, a point coordinate, and its
  `sk8tag`.
- **`parks.csv`** — the same data as a flat table, for spreadsheets, pandas, or
  anything that prefers rows to geometry.

Each park carries three fields and nothing else:

| field | what it is |
|-------|------------|
| `name` | the park's name |
| `lat` / `lon` | its location (GeoJSON stores these as `[lon, lat]`) |
| `sk8tag` | a stable, unique geohash-based identifier for the location |

The `sk8tag` is the join key. It's stable per location, so you can match a park
here against the same park in a later release, or against the live site.

## What a `sk8tag` is

A `sk8tag` is a short, deterministic identifier derived from a park's
coordinates (geohash-based). We use 7 digit geohashes whic help keep
releases diffable even when park coordinates are changed slightly: parks are sorted by `sk8tag` with a fixed field order, so each update shows exactly which parks were added, changed, or removed.

sk8tags are intended to be shared on social media, print and the like and
can always be looked up on sk8tags.com to find the latest community-maintained version.

## License & attribution

This dataset is published under the **Open Database License (ODbL) v1.0**. See
[`LICENSE`](./LICENSE) for the full text.

> Contains data derived from OpenStreetMap.
> © OpenStreetMap contributors — <https://www.openstreetmap.org/copyright>

Most of these parks were seeded from an OpenStreetMap extract. OSM data is ODbL,
and ODbL is share-alike, so this derived dataset **must** also be ODbL — that's
inherited, not a choice. In practice that means: use it freely, including
commercially, but if you publicly redistribute it or a derivative, keep it ODbL
and keep this attribution intact.

## Releases

Releases are **manual and periodic** — we push a fresh snapshot when there's
enough new and corrected data to be worth it and has survived public scrutiny by sk8tags.com users.
The file path never changes
(`parks.geojson` is always `parks.geojson`); git keeps the full history, and
tagged releases (`vYYYY.MM.DD`) mark named snapshots. So:

- the canonical URL is stable and always points at the latest data;
- `git log` / the Releases page shows every prior version;
- a published snapshot lags the live site, which always has the freshest truth.

## Found a wrong or missing park?

We do not monitor issues on this github repo for issues with individual parks - only the bulk exports as a whole e.g. if we were to publish invalid JSON for the data format.

The best place to fix individual park data is at the source:

- **On the map directly:** sk8tags.com has a community editing workflow — add a
  missing park, correct a location, flag a closure.
- **In OpenStreetMap:** since these parks are OSM-derived, fixing them in OSM
  improves the commons for everyone, us included. However, names used on sk8tags.com are 
  those agreed on by the skater community and may differ from those used by OSM. 


## Getting involved.
At this early stage a close inspection of the data will reveal many skateparks lack a proper name.
However, at sk8tags.com we are assembling a community of committed maintainers from the 
global skate community to take direct control over editing the data. Maintainers are
vetted members of the skate community and sk8tags.com provides a dedicated platform 
for them to edit park data directly or process anonymous change request submissions 
from the wider public. Each maintainer can focus on their local area and using their local
knowledge to give on-the-ground updates to changing data.
DM @sk8_tags at instagram to get involved


## Using the data

```bash
# clone it
git clone https://github.com/markharwood/openskatemap-data.git

# or just grab the latest file
curl -O https://raw.githubusercontent.com/markharwood/openskatemap-data/main/parks.geojson
```

```python
# pandas
import pandas as pd
parks = pd.read_csv(
    "https://raw.githubusercontent.com/markharwood/openskatemap-data/main/parks.csv"
)
print(len(parks), "skateparks")
```

Drop the GeoJSON into Leaflet, Mapbox, QGIS, or any OSM tooling and it just
works.

---

*Part of [sk8tags.com](https://sk8tags.com) · open data maintained by trusted members of the global skate community.*