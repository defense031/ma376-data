# Communities Crime

1,994 US communities described by 128 socioeconomic and policing variables, with violent crime rate per capita as the natural response.

**File.** `communities_crime_enriched.csv` (1,994 rows x 130 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository, retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/183/communities+and+crime)
- Merged in: Census ANSI/FIPS state codes (https://www.census.gov/library/reference/code-lists/ansi.html)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `state` | integer | 1 to 56 |  | base | U.S. state (numeric code) |
| `county` | integer | 1 to 840 | 58.9% | base | County code (frequently missing) |
| `community` | integer | 70 to 94,597 | 59.0% | base | Community code (frequently missing) |
| `community_name` | text/id | 1,828 distinct |  | base | Community/place name (text) |
| `fold` | integer | 1 to 10 |  | base | Cross-validation fold assignment (1–10) supplied with the original data |
| `V6` | numeric | 0 to 1 |  | base |  |
| `V7` | numeric | 0 to 1 |  | base |  |
| `V8` | numeric | 0 to 1 |  | base |  |
| `V9` | numeric | 0 to 1 |  | base |  |
| `V10` | numeric | 0 to 1 |  | base |  |
| `V11` | numeric | 0 to 1 |  | base |  |
| `V12` | numeric | 0 to 1 |  | base |  |
| `V13` | numeric | 0 to 1 |  | base |  |
| `V14` | numeric | 0 to 1 |  | base |  |
| `V15` | numeric | 0 to 1 |  | base |  |
| `V16` | numeric | 0 to 1 |  | base |  |
| `V17` | numeric | 0 to 1 |  | base |  |
| `V18` | numeric | 0 to 1 |  | base |  |
| `V19` | numeric | 0 to 1 |  | base |  |
| `V20` | numeric | 0 to 1 |  | base |  |
| `V21` | numeric | 0 to 1 |  | base |  |
| `V22` | numeric | 0 to 1 |  | base |  |
| `V23` | numeric | 0 to 1 |  | base |  |
| `V24` | numeric | 0 to 1 |  | base |  |
| `V25` | numeric | 0 to 1 |  | base |  |
| `V26` | numeric | 0 to 1 |  | base |  |
| `V27` | numeric | 0 to 1 |  | base |  |
| `V28` | numeric | 0 to 1 |  | base |  |
| `V29` | numeric | 0 to 1 |  | base |  |
| `V30` | numeric | 0 to 1 |  | base |  |
| `V31` | numeric | 0 to 1 | 0.1% | base |  |
| `V32` | numeric | 0 to 1 |  | base |  |
| `V33` | numeric | 0 to 1 |  | base |  |
| `V34` | numeric | 0 to 1 |  | base |  |
| `V35` | numeric | 0 to 1 |  | base |  |
| `V36` | numeric | 0 to 1 |  | base |  |
| `V37` | numeric | 0 to 1 |  | base |  |
| `V38` | numeric | 0 to 1 |  | base |  |
| `V39` | numeric | 0 to 1 |  | base |  |
| `V40` | numeric | 0 to 1 |  | base |  |
| `V41` | numeric | 0 to 1 |  | base |  |
| `V42` | numeric | 0 to 1 |  | base |  |
| `V43` | numeric | 0 to 1 |  | base |  |
| `V44` | numeric | 0 to 1 |  | base |  |
| `V45` | numeric | 0 to 1 |  | base |  |
| `V46` | numeric | 0 to 1 |  | base |  |
| `V47` | numeric | 0 to 1 |  | base |  |
| `V48` | numeric | 0 to 1 |  | base |  |
| `V49` | numeric | 0 to 1 |  | base |  |
| `V50` | numeric | 0 to 1 |  | base |  |
| `V51` | numeric | 0 to 1 |  | base |  |
| `V52` | numeric | 0 to 1 |  | base |  |
| `V53` | numeric | 0 to 1 |  | base |  |
| `V54` | numeric | 0 to 1 |  | base |  |
| `V55` | numeric | 0 to 1 |  | base |  |
| `V56` | numeric | 0 to 1 |  | base |  |
| `V57` | numeric | 0 to 1 |  | base |  |
| `V58` | numeric | 0 to 1 |  | base |  |
| `V59` | numeric | 0 to 1 |  | base |  |
| `V60` | numeric | 0 to 1 |  | base |  |
| `V61` | numeric | 0 to 1 |  | base |  |
| `V62` | numeric | 0 to 1 |  | base |  |
| `V63` | numeric | 0 to 1 |  | base |  |
| `V64` | numeric | 0 to 1 |  | base |  |
| `V65` | numeric | 0 to 1 |  | base |  |
| `V66` | numeric | 0 to 1 |  | base |  |
| `V67` | numeric | 0 to 1 |  | base |  |
| `V68` | numeric | 0 to 1 |  | base |  |
| `V69` | numeric | 0 to 1 |  | base |  |
| `V70` | numeric | 0 to 1 |  | base |  |
| `V71` | numeric | 0 to 1 |  | base |  |
| `V72` | numeric | 0 to 1 |  | base |  |
| `V73` | numeric | 0 to 1 |  | base |  |
| `V74` | numeric | 0 to 1 |  | base |  |
| `V75` | numeric | 0 to 1 |  | base |  |
| `V76` | numeric | 0 to 1 |  | base |  |
| `V77` | numeric | 0 to 1 |  | base |  |
| `V78` | numeric | 0 to 1 |  | base |  |
| `V79` | numeric | 0 to 1 |  | base |  |
| `V80` | numeric | 0 to 1 |  | base |  |
| `V81` | numeric | 0 to 1 |  | base |  |
| `V82` | numeric | 0 to 1 |  | base |  |
| `V83` | numeric | 0 to 1 |  | base |  |
| `V84` | numeric | 0 to 1 |  | base |  |
| `V85` | numeric | 0 to 1 |  | base |  |
| `V86` | numeric | 0 to 1 |  | base |  |
| `V87` | numeric | 0 to 1 |  | base |  |
| `V88` | numeric | 0 to 1 |  | base |  |
| `V89` | numeric | 0 to 1 |  | base |  |
| `V90` | numeric | 0 to 1 |  | base |  |
| `V91` | numeric | 0 to 1 |  | base |  |
| `V92` | numeric | 0 to 1 |  | base |  |
| `V93` | numeric | 0 to 1 |  | base |  |
| `V94` | numeric | 0 to 1 |  | base |  |
| `V95` | numeric | 0 to 1 |  | base |  |
| `V96` | numeric | 0 to 1 |  | base |  |
| `V97` | numeric | 0 to 1 |  | base |  |
| `V98` | numeric | 0 to 1 |  | base |  |
| `V99` | numeric | 0 to 1 |  | base |  |
| `V100` | numeric | 0 to 1 |  | base |  |
| `V101` | numeric | 0 to 1 |  | base |  |
| `V102` | numeric | 0 to 1 | 84.0% | base |  |
| `V103` | numeric | 0 to 1 | 84.0% | base |  |
| `V104` | numeric | 0 to 1 | 84.0% | base |  |
| `V105` | numeric | 0 to 1 | 84.0% | base |  |
| `V106` | numeric | 0 to 1 | 84.0% | base |  |
| `V107` | numeric | 0 to 1 | 84.0% | base |  |
| `V108` | numeric | 0 to 1 | 84.0% | base |  |
| `V109` | numeric | 0 to 1 | 84.0% | base |  |
| `V110` | numeric | 0 to 1 | 84.0% | base |  |
| `V111` | numeric | 0 to 1 | 84.0% | base |  |
| `V112` | numeric | 0 to 1 | 84.0% | base |  |
| `V113` | numeric | 0 to 1 | 84.0% | base |  |
| `V114` | numeric | 0 to 1 | 84.0% | base |  |
| `V115` | numeric | 0 to 1 | 84.0% | base |  |
| `V116` | numeric | 0 to 1 | 84.0% | base |  |
| `V117` | numeric | 0 to 1 | 84.0% | base |  |
| `V118` | numeric | 0 to 1 | 84.0% | base |  |
| `V119` | numeric | 0 to 1 |  | base |  |
| `V120` | numeric | 0 to 1 |  | base |  |
| `V121` | numeric | 0 to 1 |  | base |  |
| `V122` | numeric | 0 to 1 | 84.0% | base |  |
| `V123` | numeric | 0 to 1 | 84.0% | base |  |
| `V124` | numeric | 0 to 1 | 84.0% | base |  |
| `V125` | numeric | 0 to 1 | 84.0% | base |  |
| `V126` | numeric | 0 to 1 |  | base |  |
| `V127` | numeric | 0 to 1 | 84.0% | base |  |
| `violent_crimes_per_pop` | numeric | 0 to 1 |  | base | Normalized total number of violent crimes per 100,000 population (murder, rape, robbery, assault), scaled to `[0,1]`. |
| `state_abbr` | text/id | 46 distinct |  | Census ANSI/FIPS state codes |  |
| `state_name` | text/id | 46 distinct |  | Census ANSI/FIPS state codes |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **Census ANSI/FIPS state codes** — left join on the numeric state FIPS code. Adds: `state_abbr`, `state_name`.
