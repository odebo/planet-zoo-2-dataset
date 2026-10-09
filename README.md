# Planet Zoo 2 launch dataset (130 animals)

Machine-readable data for **Planet Zoo 2**, extracted from Frontier's official
Zoopedia payload on **2026-10-01**, plus a cohabitation matrix derived from the
same source.

Maintained alongside the reference site at **https://pz2tools.wiki/** — if you
only need to read the data, the site renders it as browsable tables.

## What's in here

| File | Rows | What it is |
|---|---|---|
| `data/animals.json` | 130 | One object per launch species: biome, enclosure type, class, order, family, genus, conservation status, weight, barrier requirements, base-vs-Deluxe |
| `data/animals.csv` | 130 | The same table in flat CSV form |
| `data/cohabitation.json` | 1,221 | Every unordered species pair that shares a biome and an enclosure type, with a compatibility verdict and the rule that produced it |

## Where the data comes from

All of it is **second-hand from the publisher's own pages**, not datamined and
not invented:

* `biomes`, `enclosure_types`, taxonomy, conservation status, weights and
  barrier specs come from the Nuxt payload behind
  `planetzoogame.com/en-GB/2/zoopedia/<slug>` (exported 2026-10-01).
* Release date, price, PC system requirements and store metadata come from the
  official Steam appdetails feed for appid **3219030**.
* Compatibility verdicts are **derived**, using the published rule below. They
  are not Frontier statements.

## Launch facts used in the data

* Release date: **2026-10-13**, single global unlock at **15:00 BST**.
  PC (Steam, Epic), PlayStation 5 and Xbox Series X|S on the same day.
  Physical disc editions follow on 2026-10-20 for PS5 and Xbox.
* Steam pre-load for pre-purchasers from **15:00 BST on 2026-10-12**.
* 130 species at launch: **124** in the base game, **6** Deluxe-only
  (Axolotl, Blue and Gold Fusilier, Golden Eagle, Golden Lion Tamarin,
  Great Hammerhead, Longfin Batfish).
* Retail SRP: Standard £39.99 / $49.99 / €49.99, Deluxe £54.99 / $64.99 / €64.99.

## Enclosure types

An animal can require more than one enclosure type.

| Enclosure type | Species |
|---|---|
| HabitatTerrestrial | 54 |
| Exhibit | 30 |
| HabitatAquarium | 19 |
| HabitatAquarium + Exhibit | 15 |
| HabitatFlying | 12 |

## Conservation status (130 species)

`LeastConcern 63 · Endangered 22 · Vulnerable 18 · CriticallyEndangered 12 ·
NotEvaluated 8 · NearThreatened 5 · Domesticated 1 · DataDeficient 1`

## The cohabitation rule (read this before using the verdicts)

A pair appears in `cohabitation.json` only if both animals share at least one
biome **and** at least one enclosure type. Then:

1. Either animal documented as **solitary** → `no`
2. Both animals documented as **social** or **mixed** → `likely`
3. Anything else → `unverified` (the source does not settle it)

Result: **376 likely, 106 unverified, 739 no** out of 1,221 biome/enclosure-valid
pairs. `unverified` is a real category, not a rounding error — treat it as
"check in game" rather than "probably fine".

## Fields in `animals.json`

```jsonc
{
  "common_name": "Aardvark",
  "slug_en": "aardvark",              // zoopedia slug
  "conservation_status": "LeastConcern",
  "class": "Mammalia",
  "order": "Tubulidentata",
  "family": "Orycteropodidae",
  "genus": "Orycteropus",
  "biomes": ["Savannah"],             // normalised to an array here
  "enclosure_types": ["HabitatTerrestrial"],
  "content_pack": "BaseGame",         // BaseGame | Deluxe
  "size_measurement": "Shoulder",
  "weight_male_kg": "50",
  "weight_female_kg": "50",
  "barrier_grade": "2",
  "barrier_min_height_m": "1",
  "barrier_climb_proof": "false",
  "barrier_allow_water": "false"
}
```

`animals.csv` keeps the raw delimiter-separated form: multi-value fields
(`biomes`, `continents`, `enclosure_types`) are `;`-separated as published.

## License

Data: **CC BY 4.0** — use it, republish it, build on it, just credit
`https://pz2tools.wiki/`. See `LICENSE`.

Planet Zoo and Planet Zoo 2 are trademarks of Frontier Developments plc. This
project is unofficial and not affiliated with or endorsed by Frontier. No game
art, audio or other assets are included in this repository.
