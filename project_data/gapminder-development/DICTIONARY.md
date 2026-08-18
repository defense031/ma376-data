# Gapminder Development

A 142-country panel at five-year steps, 1952-2007: life expectancy, GDP per capita, and population, with continent labels.

**File.** `gapminder_development_enriched.csv` (1,704 rows x 15 columns, assembled from the sources below)

## Provenance
- Base data: Gapminder via the gapminder R package, retrieved 12 Jul 2026. (https://cran.r-project.org/package=gapminder)
- Merged in: UN IGME child mortality via Our World in Data (https://ourworldindata.org/grapher/child-mortality)
- Merged in: V-Dem democracy indices (CY-Core v15) (https://v-dem.net/data/the-v-dem-dataset/)
- Merged in: Barro-Lee educational attainment v2.2 (population 15+) (https://barrolee.github.io/BarroLeeDataSet/)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `country` | text/id | 142 distinct |  | base | 142 countries; each appears in all 12 years (balanced panel). |
| `year` | integer | 1,952 to 2,007 |  | base | 1952 to 2007, every 5 years (12 distinct values). Treat as time index or as a factor depending on your question. |
| `pop` | integer | 60,011 to 1,318,683,096 |  | base | Total population (count of people). Heavily right-skewed; also a natural weighting variable. |
| `continent` | categorical | Africa, Americas, Asia, Europe, Oceania |  | base | 5 levels: Africa, Americas, Asia, Europe, Oceania. A natural grouping variable. |
| `lifeExp` | numeric | 23.6 to 82.6 |  | base | Life expectancy at birth, in years. A common candidate response. |
| `gdpPercap` | numeric | 241 to 1.14e+05 |  | base | GDP per capita, inflation-adjusted international dollars (fixed 2005 PPP). Strongly right-skewed. |
| `child_mortality_pct` | numeric | 0.28 to 54.3 | 12.7% | UN IGME child mortality via Our World in Data |  |
| `owid_covered` | categorical | False, True |  | UN IGME child mortality via Our World in Data |  |
| `v2x_polyarchy` | numeric | 0.007 to 0.923 | 4.5% | V-Dem democracy indices (CY-Core v15) |  |
| `v2x_libdem` | numeric | 0.005 to 0.897 | 5.0% | V-Dem democracy indices (CY-Core v15) |  |
| `v2x_regime` | integer | 0 to 3 | 4.5% | V-Dem democracy indices (CY-Core v15) |  |
| `vdem_covered` | categorical | False, True |  | V-Dem democracy indices (CY-Core v15) |  |
| `bl_yr_sch` | numeric | 0.02 to 12.9 | 14.8% | Barro-Lee educational attainment v2.2 (population 15+) |  |
| `bl_match_year` | integer | 1,950 to 2,005 | 14.8% | Barro-Lee educational attainment v2.2 (population 15+) |  |
| `barrolee_covered` | categorical | False, True |  | Barro-Lee educational attainment v2.2 (population 15+) |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **UN IGME child mortality via Our World in Data** — left join on country + year; early waves predate the series for some countries, flagged in owid_covered. Adds: `child_mortality_pct`, `owid_covered`.
2. **V-Dem democracy indices (CY-Core v15)** — left join on country + year; pre-independence successor states are the unmatched rows, flagged in vdem_covered. Adds: `v2x_polyarchy`, `v2x_libdem`, `v2x_regime`, `vdem_covered`.
3. **Barro-Lee educational attainment v2.2 (population 15+)** — left join on country + nearest 5-year wave; 21 countries uncovered, flagged in barrolee_covered. Adds: `bl_yr_sch`, `bl_match_year`, `barrolee_covered`.
