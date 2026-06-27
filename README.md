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
coordinates (geohash-based). We use 7-digit geohashes, which help keep
releases diffable even when park coordinates are changed slightly: parks are
sorted by `sk8tag` with a fixed field order, so each update shows exactly which
parks were added, changed, or removed.

sk8tags are intended to be shared on social media, print and the like and
can always be looked up on sk8tags.com to find the latest community-maintained version.

## Why geohashes?

A `sk8tag` is built on the open geohash standard, and that choice is
deliberate. The obvious comparison is what3words, which also turns a
location into something more shareable than raw coordinates — but the two
behave very differently when a human is involved.

People misremember things. Someone reads a sk8tag off a sticker, repeats
it to a mate, types it in a week later from memory. Get it slightly wrong
and a sk8tag still puts you in roughly the right place — the earlier
characters pin the area, and only the fine detail is lost. You land near
the spot and can take it from there.

what3words is the opposite by design: neighbouring squares are given
deliberately unrelated words, so a single wrong or forgotten word doesn't
land you nearby — it sends you somewhere completely random, often on the
other side of the world, with no way to tell you're off. Robust to error
it is not.

On top of that, geohash is open. Anyone can read or generate a sk8tag with
no API, no licence, and no per-lookup cost — what3words conversions run
through a proprietary service you can't self-host. Building on an open
standard is what lets us give this data away in the first place.

## License & attribution

This dataset is published under the **Open Database License (ODbL) v1.0**. See
[`LICENSE`](./LICENSE) for the full text.

> Contains data derived from OpenStreetMap.
> © OpenStreetMap contributors — <https://www.openstreetmap.org/copyright>

**Attribution.** If you publicly use this data or anything built from it,
please credit it as:

> Skatepark data from [sk8tags.com](https://sk8tags.com),
> © OpenStreetMap contributors, licensed under ODbL.

Most of these parks were seeded from an OpenStreetMap extract. OSM data is ODbL,
and ODbL is share-alike, so this derived dataset **must** also be ODbL — that's
inherited, not a choice. In practice that means: use it freely, including
commercially, but if you publicly redistribute it or a derivative, keep it ODbL
and keep both the sk8tags.com and OpenStreetMap attributions intact.

## Can I use this? (plain-English guide)

Short version: yes, almost certainly, including in commercial projects — and
no, you don't have to make your own app or database public. Here's how the
licence plays out for the most common things people actually do.

**"I want to show these parks as pins on my website or app."**
Go for it. Displaying the data — a map, a list, search results — is fine, even
in a paid or commercial product. All you need to do is credit the source
(see below). You do **not** have to open up your own app, code, or database
to do this.

**"I want to load the data into my own app's database to power features."**
Also fine, same as above. Storing the parks so your app can use them doesn't
oblige you to share anything — as long as what you're *publishing* to the
public is your app and its features (a "produced work"), not the park dataset
itself repackaged as a dataset.

**"I want to mix this with my own data and republish the combined dataset
as a download / API / data product."**
This is the one case where share-alike kicks in. If you build a new *dataset*
out of this one and hand that dataset out to the public, that combined dataset
also has to be ODbL, and you keep the attribution. (Note: this is about
publishing *data*. Publishing an app that merely uses the data is the previous
case, and is fine.)

**"I just want to look something up / use it for myself / inside my org."**
Nothing to worry about — private and internal use carries no obligations at
all.

**In every public case, keep the attribution line** (sk8tags.com + OpenStreetMap,
above). That's the one constant.

**Where do I put the attribution?** You don't have to label every pin or row.
The rule of thumb is "somewhere a reasonable person would look":

- **A map** — a small credit line in a corner works (the same way OSM-based
  maps show "© OpenStreetMap contributors"). One line covering the whole map
  is fine; you don't credit each marker.
- **A website or app** — an "About", "Credits", or "Data sources" page, or a
  footer link, is enough. It just needs to be reasonably findable, not on
  every screen.
- **If you're redistributing the data itself** (the dataset as a download or
  API) — keep the attribution and the licence *with the data*: in the file, or
  in a README/notice right alongside it, so it travels with the data rather
  than living only on a web page.

The point is that someone using or seeing your work can find out where the
data came from and that it's ODbL. A clear, discoverable credit does that —
you don't need to clutter the map or the interface.

---

*This is a friendly summary, not legal advice. The binding terms are in
[`LICENSE`](./LICENSE). If you're doing something where the difference
matters — especially building a data product out of this — read it, and get
proper advice if you're unsure.*

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