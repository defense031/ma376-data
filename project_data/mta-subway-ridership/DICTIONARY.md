# Mta Subway Ridership

A balanced panel of 424 NYC subway station complexes across 26 quarters (2020Q1-2026Q2): weekday and weekend daily averages plus OMNY payment share.

**File.** `mta_subway_ridership_enriched.csv` (11,024 rows x 24 columns, assembled from the sources below)

## Provenance
- Base data: MTA hourly ridership tables via data.ny.gov SoQL, retrieved 14 Jul 2026. (https://data.ny.gov/Transportation/MTA-Subway-Hourly-Ridership-2020-2024/wujg-7c2s)
- Merged in: MTA subway stations reference table (Open NY, Socrata 39hk-dx4f) (https://data.ny.gov/resource/39hk-dx4f.csv)
- Merged in: Census ACS 5-year (2023) commuting and income, tract level (https://data.census.gov/)
- Merged in: LEHD LODES workplace jobs (2023) (https://lehd.ces.census.gov/data/lodes/LODES8/ny/)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `station_complex_id` | integer | 1 to 636 |  | base | Stable MTA identifier for the station complex. |
| `station_complex` | text/id | 462 distinct |  | base | Name with lines served, e.g. "Times Sq-42 St/Port Authority Bus Terminal (1,2,3,7,A,C,E,N,Q,R,W,S)". |
| `borough` | categorical | Bronx, Brooklyn, Manhattan, Queens |  | base | Manhattan, Brooklyn, Queens, or Bronx (the Staten Island Railway is a separate system and is not included). |
| `latitude` | numeric | 40.6 to 40.9 |  | base |  |
| `longitude` | numeric | -74 to -73.8 |  | base |  |
| `year` | integer | 2,020 to 2,026 |  | base |  |
| `quarter` | integer | 1 to 4 |  | base |  |
| `quarter_label` | text/id | 26 distinct |  | base |  |
| `total_ridership` | integer | 4 to 12,658,531 |  | base | Total fare entries (taps and swipes) at the complex that quarter. Ranges from 4 to 12,658,531. |
| `total_transfers` | integer | 0 to 1,472,035 |  | base | The source's transfers field summed over the quarter (entries via free transfer connections); see the source data dictionary for the MTA's exact definition. |
| `avg_weekday_daily` | numeric | 0 to 1.57e+05 |  | base | Mean entries per weekday (Mon-Fri), computed as weekday entries divided by the calendar count of weekdays in the quarter. Holidays count as weekdays. |
| `avg_weekend_daily` | numeric | 0 to 1.07e+05 |  | base | Mean entries per weekend day (Sat-Sun), computed the same way. |
| `omny_share` | numeric | 0 to 0.998 |  | base | Fraction of the quarter's entries paid by OMNY tap rather than MetroCard swipe. Runs 0 to 0.9981. |
| `complex_cbd` | categorical | False, True |  | MTA subway stations reference table (Open NY |  |
| `complex_ada_accessible` | categorical | False, True |  | MTA subway stations reference table (Open NY |  |
| `complex_structure` | categorical | At Grade, Elevated, Open Cut, Subway, Viaduct |  | MTA subway stations reference table (Open NY |  |
| `complex_n_routes` | integer | 1 to 12 |  | MTA subway stations reference table (Open NY |  |
| `complex_n_stations` | integer | 1 to 5 |  | MTA subway stations reference table (Open NY |  |
| `tract_wfh_pct` | numeric | 0 to 45.3 | 2.6% | Census ACS 5-year (2023) commuting and income |  |
| `tract_transit_commute_pct` | numeric | 13.3 to 100 | 2.6% | Census ACS 5-year (2023) commuting and income |  |
| `tract_median_hh_income` | integer | 11,612 to 250,001 | 3.5% | Census ACS 5-year (2023) commuting and income |  |
| `tract_geoid` | integer | 36,005,002,300 to 36,081,107,201 |  | Census ACS 5-year (2023) commuting and income |  |
| `jobs_600m_2023` | integer | 518 to 382,696 |  | LEHD LODES workplace jobs (2023) |  |
| `office_jobs_600m_2023` | integer | 3 to 221,339 |  | LEHD LODES workplace jobs (2023) |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **MTA subway stations reference table (Open NY, Socrata 39hk-dx4f)** — stations aggregated to complex, left joined on complex id: physical and service attributes. Adds: `complex_cbd`, `complex_ada_accessible`, `complex_structure`, `complex_n_routes`, `complex_n_stations`.
2. **Census ACS 5-year (2023) commuting and income, tract level** — each complex located in its census tract, tract attributes left joined; a few nonresidential tracts are suppressed by the Census and stay blank. Adds: `tract_geoid`, `tract_wfh_pct`, `tract_transit_commute_pct`, `tract_median_hh_income`.
3. **LEHD LODES workplace jobs (2023)** — block-level workplace jobs summed within 600m of each complex. Adds: `jobs_600m_2023`, `office_jobs_600m_2023`.
