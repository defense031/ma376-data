# Forest Fires

517 forest fires in Portugal's Montesinho park: location, month, weather, fire-danger indices, and hectares burned.

**File.** `forest_fires_enriched.csv` (517 rows x 23 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository (Cortez & Morais), retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/162/forest+fires)
- Merged in: Canadian FWI system / EFFIS danger classes (https://forest-fire.emergency.copernicus.eu/about-effis/technical-background/fire-danger-forecast)
- Merged in: WorldClim 2.1 climate normals (2.5-arcmin) (https://worldclim.org/data/worldclim21.html)
- Merged in: Copernicus GLO-30 digital elevation model (https://copernicus-dem-30m.s3.amazonaws.com/)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `X` | integer | 1 to 9 |  | base | Spatial grid x-coordinate within the park map |
| `Y` | integer | 2 to 9 |  | base | Spatial grid y-coordinate within the park map |
| `month` | categorical | 12 distinct |  | base | Month of observation, `jan`–`dec |
| `day` | categorical | 7 distinct |  | base | Day of week, `mon`–`sun |
| `FFMC` | numeric | 18.7 to 96.2 |  | base | Fine Fuel Moisture Code — moisture of surface litter; governs ignition ease |
| `DMC` | numeric | 1.1 to 291 |  | base | Duff Moisture Code — moisture of shallow organic layers |
| `DC` | numeric | 7.9 to 861 |  | base | Drought Code — moisture of deep, compact organic layers; a slow seasonal signal |
| `ISI` | numeric | 0 to 56.1 |  | base | Initial Spread Index — expected rate of fire spread (combines wind and FFMC) |
| `temp` | numeric | 2.2 to 33.3 |  | base | Air temperature (°C) |
| `RH` | integer | 15 to 100 |  | base | Relative humidity (%) |
| `wind` | numeric | 0.4 to 9.4 |  | base | Wind speed (km/h) |
| `rain` | numeric | 0 to 6.4 |  | base | Rain (mm/m²) in the observation window |
| `area` | numeric | 0 to 1.09e+03 |  | base | Response:** total burned area (hectares) |
| `BUI` | numeric | 2.2 to 316 |  | Canadian FWI system / EFFIS danger classes |  |
| `FWI` | numeric | 0 to 90.4 |  | Canadian FWI system / EFFIS danger classes |  |
| `effis_danger_class` | categorical | Extreme, High, Low, Moderate, Very Extreme, Very High |  | Canadian FWI system / EFFIS danger classes |  |
| `normal_tavg_c` | numeric | 3.15 to 19.7 |  | WorldClim 2.1 climate normals (2.5-arcmin) |  |
| `normal_prec_mm` | integer | 23 to 134 |  | WorldClim 2.1 climate normals (2.5-arcmin) |  |
| `normal_wind_ms` | numeric | 2.86 to 3.9 |  | WorldClim 2.1 climate normals (2.5-arcmin) |  |
| `normal_srad_kj_m2_day` | integer | 5,000 to 25,889 |  | WorldClim 2.1 climate normals (2.5-arcmin) |  |
| `mean_elev_m` | numeric | 649 to 1.02e+03 |  | Copernicus GLO-30 digital elevation model |  |
| `mean_slope_deg` | numeric | 6.57 to 18.9 |  | Copernicus GLO-30 digital elevation model |  |
| `max_elev_m` | numeric | 795 to 1.31e+03 |  | Copernicus GLO-30 digital elevation model |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **Canadian FWI system / EFFIS danger classes** — BUI and FWI computed from the base file's own FFMC/DMC/DC/ISI components by the standard equations, then classed on the EFFIS thresholds. Adds: `BUI`, `FWI`, `effis_danger_class`.
2. **WorldClim 2.1 climate normals (2.5-arcmin)** — monthly normals sampled at each fire's park grid cell and month. Adds: `normal_tavg_c`, `normal_prec_mm`, `normal_wind_ms`, `normal_srad_kj_m2_day`.
3. **Copernicus GLO-30 digital elevation model** — terrain summarized per park grid cell (registration of the 9x9 park grid documented in the kit's provenance). Adds: `mean_elev_m`, `mean_slope_deg`, `max_elev_m`.
