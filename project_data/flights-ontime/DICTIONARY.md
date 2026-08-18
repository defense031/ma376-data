# Flights Ontime

12,000 of 597,919 US domestic flights from the April 2026 BTS on-time file: schedule, delays, cancellations, and delay-cause minutes across 34 columns.

**File.** `flights_ontime_enriched.csv` (12,000 rows x 46 columns, assembled from the sources below)

## Provenance
- Base data: BTS TranStats prezip, April 2026 file, retrieved 14 Jul 2026. (https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FGJ&QO_fu146_anzr=b0-gvzr)
- Merged in: OpenFlights airports database (https://raw.githubusercontent.com/jpatokal/openflights/master/data/airports.dat)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `flight_date` | text/id | 30 distinct |  | base |  |
| `day_of_week` | integer | 1 to 7 |  | base |  |
| `carrier` | categorical | 13 distinct |  | base |  |
| `tail_number` | text/id | 4,662 distinct | 0.1% | base |  |
| `flight_number` | integer | 1 to 8,801 |  | base |  |
| `origin` | text/id | 297 distinct |  | base |  |
| `origin_city_name` | text/id | 291 distinct |  | base |  |
| `origin_state` | text/id | 51 distinct |  | base |  |
| `dest` | text/id | 301 distinct |  | base |  |
| `dest_city_name` | text/id | 295 distinct |  | base |  |
| `dest_state` | text/id | 51 distinct |  | base |  |
| `crs_dep_time` | integer | 15 to 2,359 |  | base |  |
| `dep_time` | integer | 1 to 2,359 | 0.8% | base |  |
| `dep_delay` | integer | -28 to 1,642 | 0.8% | base |  |
| `dep_del15` | integer | 0 to 1 | 0.8% | base |  |
| `dep_time_blk` | categorical | 19 distinct |  | base |  |
| `taxi_out` | integer | 1 to 183 | 0.8% | base |  |
| `taxi_in` | integer | 1 to 219 | 0.8% | base |  |
| `crs_arr_time` | integer | 5 to 2,359 |  | base |  |
| `arr_time` | integer | 1 to 2,400 | 0.8% | base |  |
| `arr_delay` | integer | -57 to 1,639 | 1.1% | base |  |
| `arr_del15` | integer | 0 to 1 | 1.1% | base |  |
| `cancelled` | integer | 0 to 1 |  | base |  |
| `cancellation_code` | categorical | A, B, C | 99.2% | base |  |
| `diverted` | integer | 0 to 1 |  | base |  |
| `crs_elapsed_time` | integer | 25 to 662 |  | base |  |
| `actual_elapsed_time` | integer | 23 to 669 | 1.1% | base |  |
| `air_time` | integer | 10 to 647 | 1.1% | base |  |
| `distance` | integer | 31 to 4,962 |  | base |  |
| `carrier_delay` | integer | 0 to 1,639 | 79.3% | base |  |
| `weather_delay` | integer | 0 to 1,155 | 79.3% | base |  |
| `nas_delay` | integer | 0 to 834 | 79.3% | base |  |
| `security_delay` | integer | 0 to 79 | 79.3% | base |  |
| `late_aircraft_delay` | integer | 0 to 692 | 79.3% | base |  |
| `origin_name_ap` | text/id | 295 distinct | 0.1% | OpenFlights airports database |  |
| `origin_city_ap` | text/id | 286 distinct | 0.1% | OpenFlights airports database |  |
| `origin_lat_ap` | numeric | 17.7 to 66.9 | 0.1% | OpenFlights airports database |  |
| `origin_lon_ap` | numeric | -163 to -64.8 | 0.1% | OpenFlights airports database |  |
| `origin_elevation_ft_ap` | integer | 3 to 7,820 | 0.1% | OpenFlights airports database |  |
| `origin_timezone_ap` | categorical | 10 distinct | 0.1% | OpenFlights airports database |  |
| `dest_name_ap` | text/id | 300 distinct |  | OpenFlights airports database |  |
| `dest_city_ap` | text/id | 289 distinct |  | OpenFlights airports database |  |
| `dest_lat_ap` | numeric | 17.7 to 71.3 |  | OpenFlights airports database |  |
| `dest_lon_ap` | numeric | -165 to -64.8 |  | OpenFlights airports database |  |
| `dest_elevation_ft_ap` | integer | 3 to 7,820 |  | OpenFlights airports database |  |
| `dest_timezone_ap` | categorical | 9 distinct |  | OpenFlights airports database |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **OpenFlights airports database** — left join on the origin and destination IATA codes separately; two small airports (EAR, XWA) are absent and stay blank. Adds: `origin_name_ap`, `origin_city_ap`, `origin_lat_ap`, `origin_lon_ap`, `origin_elevation_ft_ap`, `origin_timezone_ap`, `dest_name_ap`, `dest_city_ap`, `dest_lat_ap`, `dest_lon_ap`, `dest_elevation_ft_ap`, `dest_timezone_ap`.
