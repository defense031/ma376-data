# Absenteeism Courier

740 absence records from a Brazilian courier company: hours absent, ICD-coded reason, season, distance, tenure, workload, and personal attributes.

**File.** `absenteeism_courier_enriched.csv` (740 rows x 23 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository, retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/445/absenteeism+at+work)
- Merged in: WHO ICD-10 chapter reference (22 chapters) (https://icd.who.int/browse10/2019/en)
- Merged in: WHO BMI classification cutoffs (https://www.who.int/data/gho/data/themes/topics/topic-details/GHO/body-mass-index)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `ID` | integer | 1 to 36 |  | base | Employee id; **repeats across rows** — many events per employee. |
| `Reason for absence` | integer | 0 to 28 |  | base | ICD disease groups 1–21, plus non-ICD administrative categories 22–28 (e.g. dental, physiotherapy, medical follow-up, patient follow-up). **0 = no reason / no absence. |
| `Month of absence` | integer | 0 to 12 |  | base | Calendar month 1–12; 0 present for zero-absence records. |
| `Day of the week` | integer | 2 to 6 |  | base | 2 = Monday, 3 = Tuesday, 4 = Wednesday, 5 = Thursday, 6 = Friday. |
| `Seasons` | integer | 1 to 4 |  | base | 1 = summer, 2 = autumn, 3 = winter, 4 = spring (Southern Hemisphere calendar). |
| `Transportation expense` | integer | 118 to 388 |  | base | Cost of transportation to work. |
| `Distance from Residence to Work` | integer | 5 to 52 |  | base | Commute distance, km. |
| `Service time` | integer | 1 to 29 |  | base | Years at the company (tenure). |
| `Age` | integer | 27 to 58 |  | base | Employee age, years. |
| `Work load Average/day` | numeric | 206 to 379 |  | base | Site's average daily workload. |
| `Hit target` | integer | 81 to 100 |  | base | Percentage of performance target met. |
| `Disciplinary failure` | integer | 0 to 1 |  | base | 1 = disciplinary failure on record. |
| `Education` | integer | 1 to 4 |  | base | 1 = high school, 2 = graduate, 3 = postgraduate, 4 = master/doctor. |
| `Son` | integer | 0 to 4 |  | base | Number of children. |
| `Social drinker` | integer | 0 to 1 |  | base | 1 = social drinker. |
| `Social smoker` | integer | 0 to 1 |  | base | 1 = social smoker. |
| `Pet` | integer | 0 to 8 |  | base | Number of pets. |
| `Weight` | integer | 56 to 108 |  | base | Body weight, kg. |
| `Height` | integer | 163 to 196 |  | base | Height, cm. |
| `Body mass index` | integer | 19 to 38 |  | base | BMI, derived from weight and height. |
| `Absenteeism time in hours` | integer | 0 to 120 |  | base | PRIMARY RESPONSE.** Hours absent for the event; 0 for no-absence records. |
| `icd10_chapter_title` | categorical | 22 distinct |  | WHO ICD-10 chapter reference (22 chapters) |  |
| `who_bmi_class` | categorical | normal_range, obese_class_i, obese_class_ii, overweight_pre_obese |  | WHO BMI classification cutoffs |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **WHO ICD-10 chapter reference (22 chapters)** — reason codes 1-21 are ICD-10 chapters and join directly; codes 0 and 22-28 are the source's own administrative categories, labeled 'non-ICD administrative reason'. Adds: `icd10_chapter_title`.
2. **WHO BMI classification cutoffs** — each Body mass index value binned into the six WHO classes. Adds: `who_bmi_class`.
