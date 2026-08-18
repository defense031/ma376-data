# Garment Productivity

1,197 team-day records from a garment factory: targeted versus actual productivity, incentives, overtime, idle time, department, and team.

**File.** `garment_productivity_enriched.csv` (1,197 rows x 20 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository, retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/597/productivity+prediction+of+garment+employees)
- Merged in: Open-Meteo ERA5 historical archive, Dhaka (https://archive-api.open-meteo.com/v1/archive)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `date` | text/id | 59 distinct |  | base | Calendar date of the record. |
| `quarter` | categorical | Quarter1, Quarter2, Quarter3, Quarter4, Quarter5 |  | base | Quarter of the month: Quarter1–Quarter4, plus a stray **Quarter5** (see caveats). |
| `department` | categorical | finishing, finishing , sweing |  | base | Two values, but the sewing department is misspelled **`sweing`** in the raw data — literally. Also a `finishing` value. |
| `day` | categorical | Monday, Saturday, Sunday, Thursday, Tuesday, Wednesday |  | base | Day of the week. |
| `team` | integer | 1 to 12 |  | base | Team number. Numeric in the file but a factor in analysis. |
| `targeted_productivity` | numeric | 0.07 to 0.8 |  | base | Management-set target for the team that day. |
| `smv` | numeric | 2.9 to 54.6 |  | base | Standard minute value — allotted time for a task. |
| `wip` | integer | 7 to 23,122 | 42.3% | base | Work in progress: count of unfinished items. **Empty in 506 rows** — all `finishing` records (see caveats). |
| `over_time` | integer | 0 to 25,920 |  | base | Overtime, in minutes. |
| `incentive` | integer | 0 to 3,600 |  | base | Financial incentive, in BDT. |
| `idle_time` | integer | 0 to 300 |  | base | Minutes of production idle time. |
| `idle_men` | integer | 0 to 45 |  | base | Number of idle workers during downtime. |
| `no_of_style_change` | integer | 0 to 2 |  | base | Count of product style changes on the line that day. |
| `no_of_workers` | numeric | 2 to 89 |  | base | Number of workers on the team. |
| `actual_productivity` | numeric | 0.234 to 1.12 |  | base | Realized productivity — **the primary response. |
| `wx_temp_max_c` | numeric | 21.6 to 32.2 |  | Open-Meteo ERA5 historical archive |  |
| `wx_temp_min_c` | numeric | 10.6 to 21 |  | Open-Meteo ERA5 historical archive |  |
| `wx_temp_mean_c` | numeric | 16.5 to 26.1 |  | Open-Meteo ERA5 historical archive |  |
| `wx_precipitation_mm` | numeric | 0 to 7.5 |  | Open-Meteo ERA5 historical archive |  |
| `wx_rel_humidity_mean_pct` | integer | 48 to 86 |  | Open-Meteo ERA5 historical archive |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **Open-Meteo ERA5 historical archive, Dhaka** — left join on date; every base date is covered. Adds: `wx_temp_max_c`, `wx_temp_min_c`, `wx_temp_mean_c`, `wx_precipitation_mm`, `wx_rel_humidity_mean_pct`.
