# Energy Efficiency

768 simulated building designs varying compactness, glazing, orientation, and size, with heating and cooling loads as twin responses.

**File.** `energy_efficiency.csv` (768 rows x 10 columns)

## Provenance
- Base data: UCI Machine Learning Repository (Tsanas & Xifara), retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/242/energy+efficiency)

## Column dictionary

| column | type | values | missing | meaning |
|---|---|---|---|---|
| `relative_compactness` | numeric | 0.62 to 0.98 |  | Compactness of the building form (volume-to-surface efficiency); higher = more compact. |
| `surface_area` | numeric | 514 to 808 |  | Total external surface area. |
| `wall_area` | numeric | 245 to 416 |  | Total wall area. |
| `roof_area` | numeric | 110 to 220 |  | Total roof area. |
| `overall_height` | numeric | 3.5 to 7 |  | Building height — **only two values** in the data (effectively a two-level factor). |
| `orientation` | integer | 2 to 5 |  | Compass orientation, coded 2 / 3 / 4 / 5. Categorical, not a magnitude. |
| `glazing_area` | numeric | 0 to 0.4 |  | Fraction of facade that is glazed (window-to-wall). |
| `glazing_distribution` | integer | 0 to 5 |  | How the glazing is distributed across facades (coded). |
| `heating_load` | numeric | 6.01 to 43.1 |  | Simulated heating energy load. |
| `cooling_load` | numeric | 10.9 to 48 |  | Simulated cooling energy load, same energy units as Y1. |
