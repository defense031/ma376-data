# Parkinsons Telemonitoring

5,875 voice recordings from 42 Parkinson's patients with jitter, shimmer, and noise measures, tracking clinician-scored symptom severity (UPDRS).

**File.** `parkinsons_telemonitoring.csv` (5,875 rows x 22 columns)

## Provenance
- Base data: UCI Machine Learning Repository, retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/189/parkinsons+telemonitoring)

## Column dictionary

| column | type | values | missing | meaning |
|---|---|---|---|---|
| `subject` | integer | 1 to 42 |  | Patient identifier, 1–42. **Not a predictor** — an index. |
| `age` | integer | 36 to 85 |  | Patient age in years. |
| `sex` | integer | 0 to 1 |  | Binary, 0/1. |
| `test_time` | numeric | -4.26 to 215 |  | Days since recruitment; decimal (integer part = day, fraction = time of day). |
| `motor_updrs` | numeric | 5.04 to 39.5 |  | Clinician-scored motor UPDRS. Secondary target. |
| `total_updrs` | numeric | 7 to 55 |  | Clinician-scored total UPDRS. Primary target. |
| `jitter_pct` | numeric | 0.00083 to 0.1 |  | Jitter as a percentage. |
| `jitter_abs` | numeric | 2.25e-06 to 0.000446 |  | Absolute jitter (seconds). |
| `jitter_rap` | numeric | 0.00033 to 0.0575 |  | Relative amplitude perturbation. |
| `jitter_ppq5` | numeric | 0.00043 to 0.0696 |  | Five-point period perturbation quotient. |
| `jitter_ddp` | numeric | 0.00098 to 0.173 |  | Difference of differences of periods. |
| `shimmer` | numeric | 0.00306 to 0.269 |  | Shimmer (proportion). |
| `shimmer_db` | numeric | 0.026 to 2.11 |  | Shimmer in decibels. |
| `shimmer_apq3` | numeric | 0.00161 to 0.163 |  | Three-point amplitude perturbation quotient. |
| `shimmer_apq5` | numeric | 0.00194 to 0.167 |  | Five-point amplitude perturbation quotient. |
| `shimmer_apq11` | numeric | 0.00249 to 0.275 |  | Eleven-point amplitude perturbation quotient. |
| `shimmer_dda` | numeric | 0.00484 to 0.488 |  | Difference of differences of amplitudes. |
| `nhr` | numeric | 0.000286 to 0.748 |  | Noise-to-harmonics ratio. |
| `hnr` | numeric | 1.66 to 37.9 |  | Harmonics-to-noise ratio. |
| `rpde` | numeric | 0.151 to 0.966 |  | Recurrence period density entropy (nonlinear dynamics). |
| `dfa` | numeric | 0.514 to 0.866 |  | Detrended fluctuation analysis (signal self-similarity). |
| `ppe` | numeric | 0.022 to 0.732 |  | Pitch period entropy. |
