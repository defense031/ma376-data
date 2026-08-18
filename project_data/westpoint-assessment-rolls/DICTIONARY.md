# Westpoint Assessment Rolls

The official 2025 New York assessment roll for six Orange County towns ringing West Point: 12,000 residential parcels with values, lot dimensions, exemptions, and school districts.

**File.** `westpoint_assessment_rolls_enriched.csv` (12,000 rows x 27 columns, assembled from the sources below)

## Provenance
- Base data: data.ny.gov (Socrata), 2025 roll, retrieved 14 Jul 2026. (https://data.ny.gov/Government-Finance/Property-Assessment-Data-from-Local-Assessment-Rol/7vem-aaz7)
- Merged in: NYS ORPTS equalization rates (Open NY, Socrata e6pv-77bh) (https://data.ny.gov/Government-Finance/Equalization-Rates-Beginning-Rate-Year-1954/e6pv-77bh)
- Merged in: NYS assessment equity statistics (Open NY, Socrata 4sut-q3dt) (https://data.ny.gov/Government-Finance/Real-Property-Assessment-Equity-Statistics-By-Muni/4sut-q3dt)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `roll_year` | integer | 2,025 to 2,025 |  | base | Constant 2025 (the roll year of this extract). |
| `municipality_name` | categorical | Cornwall, Highlands, Monroe, New Windsor, Newburgh, Woodbury |  | base | Town: Newburgh (4,742), New Windsor (2,449), Monroe (2,039), Cornwall (1,153), Woodbury (1,135), Highlands (482). West Point itself sits in Highlands. |
| `school_district_name` | categorical | 8 distinct |  | base | 8 districts (Newburgh, Monroe-Woodbury, Cornwall, Highland Falls, ...). Crosses town lines. |
| `swis_code` | integer | 331,100 to 335,809 |  | base | State-assigned municipality code; distinguishes villages from their surrounding towns. `swis_code` + `print_key_code` is the unique parcel key. |
| `tax_class` | categorical | H, N | 87.8% | base | Blank on 87.8 percent of rows; only some assessing units use it. |
| `property_class` | integer | 210 to 240 |  | base | 210 one-family (10,975), 220 two-family (715), 230 three-family (196), 215 one-family with accessory apartment (89), 240 rural residence with acreage (25). |
| `property_class_description` | categorical | One Family Year-Round Residence, One Family Year-Round Residence with Accessory Apartment, Rural Residence with Acreage, Three Family Year-Round Residence, Two Family Year-Round Residence |  | base | Plain-language label for `property_class`. |
| `print_key_code` | text/id | 11,353 distinct |  | base | Parcel print key (section-block-lot). NOT unique alone; unique jointly with `swis_code`. |
| `parcel_address_number` | text/id | 1,245 distinct | 0.1% | base |  |
| `parcel_address_street` | text/id | 1,684 distinct |  | base |  |
| `parcel_address_suff` | text/id | 34 distinct | 4.7% | base |  |
| `front` | numeric | 0 to 626 |  | base |  |
| `depth` | numeric | 0 to 670 |  | base |  |
| `bank` | text/id | 270 distinct | 46.8% | base | Escrow bank code (e.g. `C000000`, `C080370`). Blank on 46.8 percent: blank means no escrow bank on file, a rough no-mortgage-escrow signal. |
| `grid_coordinates_east` | integer | 0 to 5,945,291 |  | base |  |
| `grid_coordinates_north` | integer | 0 to 9,898,064 |  | base |  |
| `full_market_value` | integer | 0 to 1,836,200 |  | base | Assessor's estimate of full market value, in dollars, equalized across towns. Median 378,200; quartiles 283,200 and 513,400; max 1,836,200. The natural response. |
| `assessment_land` | integer | 0 to 267,200 |  | base |  |
| `assessment_total` | integer | 0 to 1,001,700 |  | base |  |
| `county_taxable_value` | integer | 0 to 1,001,700 |  | base |  |
| `town_taxable_value` | integer | 0 to 1,001,700 |  | base |  |
| `school_taxable` | integer | 0 to 1,001,700 |  | base |  |
| `n_exemptions` | integer | 0 to 6 |  | base | DERIVED by the curator: count of non-blank exemption codes (the source carries 10 exemption slots per parcel). 0 on 61.0 percent of rows; max 6. |
| `exemption_school_total` | integer | 0 to 605,614 |  | base | DERIVED by the curator: sum of the 10 school exemption amount slots, 0 where none. On the town-ratio assessed scale. Max 605,614. |
| `town_equalization_rate_2025` | numeric | 9.78 to 100 |  | NYS ORPTS equalization rates (Open NY |  |
| `town_residential_cod` | numeric | 9.91 to 15.1 | 12.2% | NYS assessment equity statistics (Open NY |  |
| `town_residential_prd` | numeric | 0.99 to 1.03 | 12.2% | NYS assessment equity statistics (Open NY |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **NYS ORPTS equalization rates (Open NY, Socrata e6pv-77bh)** — parcel SWIS code rolled up to its town SWIS (first four digits + 00), 2025 rate year. Adds: `town_equalization_rate_2025`.
2. **NYS assessment equity statistics (Open NY, Socrata 4sut-q3dt)** — same town-SWIS rollup, latest survey year. Adds: `town_residential_cod`, `town_residential_prd`.
