# Movies Boxoffice

3,201 films with budget, US and worldwide gross, distributor, genre, rating, and critic versus audience scores.

**File.** `movies_boxoffice_enriched.csv` (3,201 rows x 17 columns, assembled from the sources below)

## Provenance
- Base data: vega-datasets movies, retrieved 12 Jul 2026. (https://github.com/vega/vega-datasets/blob/main/data/movies.json)
- Merged in: CPI-U annual average, 1913-2025 (FRED CPIAUCNS) (https://fred.stlouisfed.org/graph/fredgraph.csv?id=CPIAUCNS)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `Title` | text/id | 3,176 distinct |  | base | Film title; one row per film. |
| `US Gross` | integer | 0 to 760,167,650 | 0.2% | base | Domestic box-office gross, nominal USD. Right-skewed; some missing. |
| `Worldwide Gross` | integer | 0 to 2,767,891,499 | 0.2% | base | Global box-office gross, nominal USD. Right-skewed; some missing. |
| `US DVD Sales` | integer | 618,454 to 352,582,053 | 82.4% | base | Domestic DVD sales revenue, nominal USD. Very frequently missing. |
| `Production Budget` | integer | 218 to 300,000,000 |  | base | Reported production budget, nominal USD. Right-skewed; some missing. |
| `Release Date` | text/id | 1,600 distinct |  | base | Theatrical release date; spans roughly the 1930s–2000s. |
| `MPAA Rating` | categorical | 7 distinct | 18.9% | base | G / PG / PG-13 / R / NC-17 / Not Rated; some blanks. |
| `Running Time min` | integer | 46 to 222 | 62.2% | base | Runtime in minutes; some missing. |
| `Distributor` | text/id | 174 distinct | 7.2% | base | Releasing studio / distributor; many levels, some blanks. |
| `Source` | categorical | 18 distinct | 11.4% | base | Source material (e.g., original screenplay, based on novel, remake); some blanks. |
| `Major Genre` | categorical | 12 distinct | 8.6% | base | Primary genre (Comedy, Drama, Action, etc.); some blanks. |
| `Creative Type` | categorical | 9 distinct | 13.9% | base | Franchise / creative framing (e.g., Contemporary Fiction, Fantasy); some blanks. |
| `Director` | text/id | 550 distinct | 41.6% | base | Director name; high-cardinality, many missing. |
| `Rotten Tomatoes Rating` | integer | 1 to 100 | 27.5% | base | Critics' score, 0–100; some missing. |
| `IMDB Rating` | numeric | 1.4 to 9.2 | 6.7% | base | Audience score, 0–10; some missing. |
| `IMDB Votes` | integer | 18 to 519,541 | 6.7% | base | Count of IMDB user votes; a proxy for audience reach/popularity. |
| `cpi_u_annual_avg` | numeric | 12.9 to 322 | 0.5% | CPI-U annual average |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **CPI-U annual average, 1913-2025 (FRED CPIAUCNS)** — left join on release year; rows with unparseable release dates stay blank. Adds: `cpi_u_annual_avg`.
