# Nyc Collisions

40,000 recent NYC motor-vehicle collision reports: borough, time, contributing factors, vehicle types, injuries, and fatalities, exactly as the city records them.

**File.** `nyc_collisions_enriched.csv` (113,626 rows x 39 columns, assembled from the sources below)

## Provenance
- Base data: NYC Open Data, fresh slice retrieved 12 Jul 2026. (https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95)
- Merged in: NOAA GHCN-Daily, Central Park station USW00094728 (https://www.ncei.noaa.gov/access/services/data/v1)
- Merged in: NYC Open Data, Motor Vehicle Collisions - Person table (https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Person/f55k-p6yu)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `crash_date` | text/id | 467 distinct |  | base |  |
| `crash_time` | text/id | 1,438 distinct |  | base |  |
| `borough` | categorical | BRONX, BROOKLYN, MANHATTAN, QUEENS, STATEN ISLAND | 34.7% | base |  |
| `zip_code` | integer | 10,000 to 11,697 | 34.7% | base |  |
| `latitude` | numeric | 0 to 40.9 | 8.2% | base |  |
| `longitude` | numeric | -74.3 to 0 | 8.2% | base |  |
| `location` | text/id | 19,845 distinct | 8.2% | base | borough` and `zip_code` are **blank on ~30%+ of rows**. `latitude`/`longitude` are sometimes missing or `0` (bad geocode). Street fields are **inconsistent free text**; `location` is a `(lat, long)` string. |
| `on_street_name` | text/id | 2,906 distinct | 27.0% | base |  |
| `off_street_name` | text/id | 3,148 distinct | 53.7% | base |  |
| `cross_street_name` | text/id | 7,680 distinct | 73.0% | base |  |
| `number_of_persons_injured` | integer | 0 to 18 |  | base |  |
| `number_of_persons_killed` | integer | 0 to 3 |  | base |  |
| `number_of_pedestrians_injured` | integer | 0 to 3 |  | base |  |
| `number_of_pedestrians_killed` | integer | 0 to 1 |  | base |  |
| `number_of_cyclist_injured` | integer | 0 to 3 |  | base |  |
| `number_of_cyclist_killed` | integer | 0 to 1 |  | base |  |
| `number_of_motorist_injured` | integer | 0 to 18 |  | base |  |
| `number_of_motorist_killed` | integer | 0 to 3 |  | base |  |
| `contributing_factor_vehicle_1` | text/id | 55 distinct | 0.5% | base |  |
| `contributing_factor_vehicle_2` | text/id | 40 distinct | 22.3% | base |  |
| `contributing_factor_vehicle_3` | categorical | 17 distinct | 89.5% | base |  |
| `contributing_factor_vehicle_4` | categorical | 10 distinct | 97.2% | base |  |
| `contributing_factor_vehicle_5` | categorical | 7 distinct | 99.2% | base |  |
| `collision_id` | integer | 4,136,992 to 4,762,491 |  | base |  |
| `vehicle_type_code1` | text/id | 160 distinct | 1.2% | base |  |
| `vehicle_type_code2` | text/id | 206 distinct | 32.8% | base |  |
| `vehicle_type_code_3` | text/id | 37 distinct | 90.2% | base |  |
| `vehicle_type_code_4` | categorical | 22 distinct | 97.3% | base |  |
| `vehicle_type_code_5` | categorical | 10 distinct | 99.2% | base |  |
| `wx_prcp_in` | numeric | 0 to 7.13 |  | NOAA GHCN-Daily |  |
| `wx_snow_in` | numeric | 0 to 5.8 |  | NOAA GHCN-Daily |  |
| `wx_snwd_in` | integer | 0 to 14 |  | NOAA GHCN-Daily |  |
| `wx_tmax_f` | integer | 15 to 98 |  | NOAA GHCN-Daily |  |
| `wx_tmin_f` | integer | 7 to 78 |  | NOAA GHCN-Daily |  |
| `persons_involved` | integer | 1 to 56 | 0.5% | NYC Open Data |  |
| `occupants` | integer | 0 to 56 | 0.5% | NYC Open Data |  |
| `pedestrians` | integer | 0 to 5 | 0.5% | NYC Open Data |  |
| `persons_injured_persontable` | integer | 0 to 18 | 0.5% | NYC Open Data |  |
| `median_person_age` | numeric | -966 to 6.23e+03 | 4.3% | NYC Open Data |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **NOAA GHCN-Daily, Central Park station USW00094728** — left join on crash date; every date in the span is present. Adds: `wx_prcp_in`, `wx_snow_in`, `wx_snwd_in`, `wx_tmax_f`, `wx_tmin_f`.
2. **NYC Open Data, Motor Vehicle Collisions - Person table** — person rows aggregated to counts per collision_id, then left joined; 0.5% of collisions have no person record and stay blank (absence of a record, not a count of zero). Adds: `persons_involved`, `occupants`, `pedestrians`, `persons_injured_persontable`, `median_person_age`.
