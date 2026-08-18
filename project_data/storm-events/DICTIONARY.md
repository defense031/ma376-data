# Storm Events

Event-level US severe weather, 2021-2025: type, location, month, deaths, injuries, and property/crop damage parsed to dollars from NOAA's K/M/B suffixes.

**File.** `storm_events_enriched.csv` (12,000 rows x 20 columns, assembled from the sources below)

## Provenance
- Base data: NOAA/NCEI Storm Events bulk files, retrieved 14 Jul 2026 (public domain). (https://www.ncei.noaa.gov/stormevents/)
- Merged in: U.S. Census Bureau, state population estimates 2020-2025 (https://www2.census.gov/programs-surveys/popest/tables/2020-2025/state/totals/NST-EST2025-POP.xlsx)
- Merged in: U.S. Bureau of Economic Analysis, real GDP by state (SAGDP) (https://apps.bea.gov/regional/downloadzip.htm)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `event_id` | integer | 927,875 to 1,310,668 |  | base | NOAA unique event identifier. |
| `year` | integer | 2,021 to 2,025 |  | base | 2021 through 2025. |
| `month` | integer | 1 to 12 |  | base | 1 through 12, from the event begin date. |
| `state` | text/id | 65 distinct |  | base | State, territory, or marine area name. **65 distinct values**, including marine zones (e.g. Gulf Of Mexico, Lake Erie) and territories. |
| `event_type` | text/id | 46 distinct |  | base | NOAA event type. **46 distinct values** in this sample; Thunderstorm Wind (3,213), Hail (1,514), and Drought (792) lead. |
| `cz_type` | categorical | C, Z |  | base | C` = county-level event (6,449 rows), `Z` = forecast-zone event (5,551 rows). |
| `deaths_direct` | integer | 0 to 11 |  | base | Deaths directly caused by the event. |
| `deaths_indirect` | integer | 0 to 8 |  | base | Deaths indirectly caused (e.g. heart attack while shoveling snow). |
| `injuries_direct` | integer | 0 to 25 |  | base | Direct injuries. |
| `injuries_indirect` | integer | 0 to 34 |  | base | Indirect injuries. |
| `damage_property_usd` | integer | 0 to 2,200,000,000 | 22.1% | base | Property damage in dollars, parsed from NOAA's K/M/B suffix notation (e.g. `10.00K` becomes 10000, `1.00B` becomes 1000000000). Blank = not reported. |
| `damage_crops_usd` | integer | 0 to 40,400,000 | 21.9% | base | Crop damage in dollars, same parsing. Blank = not reported. |
| `magnitude` | numeric | 0.25 to 113 | 48.8% | base | Wind speed in **knots** for wind events; hail diameter in **inches** for hail events; blank otherwise. The unit depends on `event_type`. |
| `magnitude_type` | categorical | EG, ES, MG, MS | 61.5% | base | EG`/`ES` = estimated gust/sustained wind, `MG`/`MS` = measured gust/sustained wind. Blank for hail rows even when `magnitude` is present. |
| `tor_f_scale` | categorical | EF0, EF1, EF2, EF3, EF4, EFU | 97.8% | base | Enhanced Fujita rating for tornadoes (EF0 through EF4 here, plus EFU = unrated). Present on all 263 tornado rows, blank elsewhere. |
| `begin_lat` | numeric | -14.3 to 62.8 | 42.3% | base |  |
| `begin_lon` | numeric | -171 to 158 | 42.3% | base |  |
| `duration_hours` | numeric | 0 to 744 |  | base | Computed as end time minus begin time in the local reporting timezone. |
| `state_population` | integer | 579,662 to 39,364,774 | 4.2% | U.S. Census Bureau |  |
| `state_real_gdp_musd` | numeric | 3.36e+04 to 3.39e+06 | 4.7% | U.S. Bureau of Economic Analysis |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **U.S. Census Bureau, state population estimates 2020-2025** — left join on state + year; marine/territorial zones have no resident population and stay blank. Adds: `state_population`.
2. **U.S. Bureau of Economic Analysis, real GDP by state (SAGDP)** — left join on state + year; same blank set as population, plus Puerto Rico. Adds: `state_real_gdp_musd`.
