# Ny Dmv Crashes

12,000 police-reported 2024 crashes from six Hudson Valley counties: severity class, lighting, weather, road character, collision type, and contributing factors.

**File.** `ny_dmv_crashes_enriched.csv` (12,000 rows x 25 columns, assembled from the sources below)

## Provenance
- Base data: data.ny.gov (Socrata), NYS DMV case table, retrieved 14 Jul 2026. (https://data.ny.gov/Transportation/Motor-Vehicle-Crashes-Case-Information-Four-Year-W/e8ky-4vqe)
- Merged in: NYS county population estimates (Open NY, Socrata krt9-ym2k) (https://data.ny.gov/resource/krt9-ym2k.csv)
- Merged in: NYS DEC 2024 deer harvest report (parsed from the published PDF) (https://dec.ny.gov/sites/default/files/2025-05/2024deerrpt.pdf)
- Merged in: NYSDOT traffic volume (AADT, 2019, latest published) (https://data.ny.gov/resource/6amx-2pbv.csv)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `year` | integer | 2,024 to 2,024 |  | base | Constant 2024. |
| `accident_descriptor` | categorical | Fatal Accident, Injury Accident, Property Damage & Injury Accident, Property Damage Accident |  | base | Severity class: Property Damage (9,281), Property Damage & Injury (2,360), Injury (325), Fatal (34). The natural raw material for a response. |
| `time` | text/id | 1,372 distinct |  | base | Clock time as `H:MM` 24-hour text (e.g. `17:35`). Parse it yourself; hour-of-day is rich. |
| `date` | text/id | 366 distinct |  | base | YYYY-MM-DD`, spanning 2024-01-01 to 2024-12-31. |
| `day_of_week` | categorical | 7 distinct |  | base | Monday through Sunday, pre-extracted. |
| `police_report` | categorical | N, Y |  | base | Y`/`N`; `N` (civilian self-reported cases) is 3.3 percent. |
| `lighting_conditions` | categorical | Dark-Road Lighted, Dark-Road Unlighted, Dawn, Daylight, Dusk, Unknown |  | base | Daylight, Dark-Road Lighted, Dark-Road Unlighted, Dusk, Dawn, Unknown (221 rows). |
| `municipality` | text/id | 149 distinct | 0.8% | base | 149 distinct city/town/village names; blank on 0.8 percent. |
| `collision_type_descriptor` | categorical | 11 distinct |  | base | 11 levels; `OTHER` dominates (4,557 rows, and nearly all single-vehicle crashes land here), plus DMV code leftovers like `LEFT TURN (3)` vs `LEFT TURN (0)`; `Unknown` on 326 rows. |
| `county_name` | categorical | DUTCHESS, ORANGE, PUTNAM, ROCKLAND, ULSTER, WESTCHESTER |  | base | WESTCHESTER (4,364), ORANGE (2,489), ROCKLAND (1,987), DUTCHESS (1,581), ULSTER (1,067), PUTNAM (512). |
| `road_descriptor` | categorical | 7 distinct |  | base | Straight/curve by level/grade/hill crest, 7 levels plus Unknown. |
| `weather_conditions` | categorical | 8 distinct |  | base | Clear, Cloudy, Rain, Snow, Sleet/Hail/Freezing Rain, Fog/Smog/Smoke, Other*, Unknown (1.9 percent). |
| `traffic_control_device` | categorical | 16 distinct | 59.7% | base | Blank on 59.7 percent of rows, with a separate explicit `Unknown` level. Blank plausibly means no device present, but the DMV does not say so; handle deliberately. |
| `road_surface_conditions` | categorical | 8 distinct |  | base | Dry, Wet, Snow/Ice (496 rows), Slush, Flooded Water, Muddy, Other, Unknown. |
| `dot_reference_marker_location` | text/id | 3,792 distinct | 52.9% | base | Highway reference marker; blank on 52.9 percent (mostly non-state roads). The only location finer than municipality. |
| `pedestrian_bicyclist_action` | categorical | 15 distinct |  | base | Not Applicable` on 97.4 percent; the remainder describes what the pedestrian/cyclist was doing. |
| `event_descriptor` | text/id | 31 distinct |  | base | First harmful event, 31 levels: Other Motor Vehicle (70.7 percent), Deer (803 rows), fixed objects (guide rail, tree, pole, embankment), Pedestrian (211 rows). |
| `number_of_vehicles_involved` | integer | 1 to 9 |  | base | 1 vehicle 28.8 percent, 2 vehicles 65.8 percent, 3+ the rest. |
| `county_population_2024` | integer | 98,842 to 1,009,165 |  | NYS county population estimates (Open NY |  |
| `county_fips` | integer | 36,027 to 36,119 |  | NYS county population estimates (Open NY |  |
| `county_deer_take_2024` | integer | 259 to 4,753 |  | NYS DEC 2024 deer harvest report (parsed from the published PDF) |  |
| `county_antlerless_deer_per_sqmi_2024` | numeric | 0.3 to 2.6 |  | NYS DEC 2024 deer harvest report (parsed from the published PDF) |  |
| `county_daily_vmt_2019` | integer | 2,746,105 to 18,110,248 |  | NYSDOT traffic volume (AADT |  |
| `county_mean_aadt_2019` | numeric | 3.94e+03 to 9.99e+03 |  | NYSDOT traffic volume (AADT |  |
| `county_aadt_segments_2019` | integer | 375 to 3,354 |  | NYSDOT traffic volume (AADT |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **NYS county population estimates (Open NY, Socrata krt9-ym2k)** — left join on county name, 2024 vintage; turns raw crash counts into rates. Adds: `county_population_2024`, `county_fips`.
2. **NYS DEC 2024 deer harvest report (parsed from the published PDF)** — left join on county; a deer-density proxy behind the animal-strike pattern. Adds: `county_deer_take_2024`, `county_antlerless_deer_per_sqmi_2024`.
3. **NYSDOT traffic volume (AADT, 2019, latest published)** — AADT segments aggregated to county, left joined; the exposure denominator for crash rates. Adds: `county_daily_vmt_2019`, `county_mean_aadt_2019`, `county_aadt_segments_2019`.
