# Concrete Strength

1,030 concrete mixtures: seven ingredient quantities plus age, with compressive strength as the response. A near-designed experiment in observational clothing.

**File.** `concrete_strength_enriched.csv` (1,030 rows x 11 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository (Yeh), retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/165/concrete+compressive+strength)
- Merged in: USGS Mineral Commodity Summaries 2025 unit prices (plus cited market estimates for fly ash, water, superplasticizer) (https://www.usgs.gov/centers/national-minerals-information-center/mineral-commodity-summaries)
- Merged in: ICE (Inventory of Carbon and Energy) V3.0 embodied-carbon factors (https://circularecology.com/embodied-carbon-footprint-database.html)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `cement` | numeric | 102 to 540 |  | base | Portland cement dosage. Most expensive binder; primary strength driver. |
| `slag` | numeric | 0 to 359 |  | base | Blast-furnace slag, a supplementary cementitious material (cheaper substitute). |
| `fly_ash` | numeric | 0 to 200 |  | base | Fly ash, a second supplementary cementitious material (cheaper substitute). Many mixes use 0. |
| `water` | numeric | 122 to 247 |  | base | Mixing water. Numerator of the water/cement ratio. |
| `superplasticizer` | numeric | 0 to 32.2 |  | base | Chemical admixture that improves workability at low water content. Many mixes use 0. |
| `coarse_agg` | numeric | 801 to 1.14e+03 |  | base | Coarse aggregate (gravel/stone); bulk filler. |
| `fine_agg` | numeric | 594 to 993 |  | base | Fine aggregate (sand); bulk filler. |
| `age_days` | integer | 1 to 365 |  | base | Curing age at which the specimen was tested; ranges 1–365. Strongly nonlinear driver. |
| `compressive_strength_mpa` | numeric | 2.33 to 82.6 |  | base | Primary response.** Measured compressive strength. |
| `cost_usd_per_m3` | numeric | 63.8 to 183 |  | USGS Mineral Commodity Summaries 2025 unit prices (plus cited market estimates for fly ash |  |
| `embodied_co2_kg_per_m3` | numeric | 115 to 547 |  | ICE (Inventory of Carbon and Energy) V3.0 embodied-carbon factors |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **USGS Mineral Commodity Summaries 2025 unit prices (plus cited market estimates for fly ash, water, superplasticizer)** — computed per mix: each ingredient quantity (kg/m3) times its published unit price, summed. Adds: `cost_usd_per_m3`.
2. **ICE (Inventory of Carbon and Energy) V3.0 embodied-carbon factors** — computed per mix: each ingredient quantity times its published kgCO2e factor, summed. Adds: `embodied_co2_kg_per_m3`.
