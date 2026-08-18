# College Scorecard

The June 2026 College Scorecard institution file cut to 2,663 four-year institutions and 39 columns: admissions, price, completion, debt, and earnings ten years after entry.

**File.** `college_scorecard_enriched.csv` (2,663 rows x 40 columns, assembled from the sources below)

## Provenance
- Base data: US Dept of Education College Scorecard, June 2026 release, retrieved 14 Jul 2026. (https://collegescorecard.ed.gov/data/)
- Merged in: BEA regional price parities by state, 2024 (https://apps.bea.gov/regional/downloadzip.htm)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `unitid` | integer | 100,654 to 501,549 |  | base | Federal (IPEDS) institution ID; unique key |
| `institution` | text/id | 2,645 distinct |  | base | Institution name |
| `city` | text/id | 1,291 distinct |  | base |  |
| `state` | text/id | 58 distinct |  | base |  |
| `region` | categorical | 10 distinct |  | base | Census-based region name (New England, Southeast, Far West, ...) |
| `locale_type` | categorical | City, Rural, Suburb, Town | 0.5% | base | City, Suburb, Town, or Rural |
| `control` | categorical | Private for-profit, Private nonprofit, Public |  | base | Public, Private nonprofit, or Private for-profit |
| `main_campus` | integer | 0 to 1 |  | base | 1 = main campus, 0 = branch |
| `hbcu` | integer | 0 to 1 |  | base | 1 = Historically Black College or University (90 schools) |
| `pred_degree` | integer | 1 to 4 |  | base | Predominant award: 1 certificate, 2 associate, 3 bachelor's, 4 graduate |
| `highest_degree` | integer | 3 to 4 |  | base | Highest award: 3 bachelor's, 4 graduate (filtered to these) |
| `open_admissions` | integer | 1 to 2 | 13.4% | base | 1 = open admissions, 2 = not open admissions |
| `admission_rate` | numeric | 0 to 1 | 36.2% | base | Fraction of applicants admitted |
| `sat_avg` | integer | 820 to 1,560 | 61.4% | base | Average SAT equivalent of admitted students |
| `sat_verbal_mid` | integer | 395 to 760 | 64.4% | base |  |
| `sat_math_mid` | integer | 395 to 785 | 64.4% | base |  |
| `act_composite_mid` | integer | 14 to 35 | 63.8% | base | ACT composite midpoint |
| `undergrad_enrollment` | integer | 0 to 163,164 | 9.9% | base | Degree-seeking undergraduate headcount |
| `share_women` | numeric | 0 to 1 | 9.9% | base | Share of undergraduates who are women |
| `share_white` | numeric | 0 to 1 | 9.9% | base |  |
| `share_black` | numeric | 0 to 1 | 9.9% | base |  |
| `share_hispanic` | numeric | 0 to 1 | 9.9% | base |  |
| `share_asian` | numeric | 0 to 1 | 9.9% | base |  |
| `tuition_in_state` | integer | 0 to 72,097 | 15.6% | base |  |
| `tuition_out_state` | integer | 0 to 72,097 | 15.6% | base |  |
| `cost_of_attendance` | integer | 6,024 to 93,512 | 19.6% | base | Average annual total cost of attendance, $ |
| `net_price` | integer | -778 to 73,043 | 18.0% | base | Average net price after aid for aided students, $ (public and private source columns merged) |
| `avg_faculty_salary_month` | integer | 729 to 25,354 | 4.0% | base | Average faculty salary per month, $ |
| `share_faculty_full_time` | numeric | 0.0043 to 1 | 10.5% | base | Share of faculty who are full time |
| `student_faculty_ratio` | integer | 1 to 147 | 10.1% | base | Undergraduate student-to-faculty ratio |
| `instruction_spend_per_student` | integer | 0 to 695,895 | 0.8% | base | Instructional expenditure per full-time-equivalent student, $ |
| `pell_share` | numeric | 0 to 1 | 10.7% | base | Share of undergraduates receiving Pell grants |
| `fed_loan_share` | numeric | 0 to 1 | 10.7% | base | Share of undergraduates taking federal loans |
| `first_gen_share` | numeric | 0.0887 to 0.851 | 21.2% | base | Share of students who are first generation |
| `median_family_income` | numeric | 0 to 1.8e+05 | 13.4% | base | Median family income of aided students, $ |
| `retention_rate` | numeric | 0 to 1 | 23.5% | base | First-to-second-year retention, full-time students |
| `completion_rate` | numeric | 0 to 1 | 17.0% | base | Completion within 150 percent of normal time (6 years for a bachelor's) |
| `median_earnings_10yr` | integer | 17,360 to 143,372 | 17.1% | base | Median earnings of federally-aided students 10 years after entry, $ |
| `median_debt_completers` | integer | 2,959 to 43,021 | 20.5% | base | Median cumulative federal loan debt of students who completed, $ |
| `rpp_all_items_2024` | numeric | 86.9 to 111 | 2.7% | BEA regional price parities by state |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **BEA regional price parities by state, 2024** — left join on state; territories have no RPP and stay blank. Adds: `rpp_all_items_2024`.
