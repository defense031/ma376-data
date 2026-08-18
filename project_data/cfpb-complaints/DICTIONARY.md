# Cfpb Complaints

12,000 of 490,966 consumer-finance complaints filed from New York, January 2025 through July 2026: product, issue, company, response, and timeliness.

**File.** `cfpb_complaints_ny_enriched.csv` (12,000 rows x 16 columns, assembled from the sources below)

## Provenance
- Base data: CFPB Consumer Complaint Database API, retrieved 14 Jul 2026. (https://www.consumerfinance.gov/data-research/consumer-complaints/)
- Merged in: FRED (NY unemployment rate, monthly; credit-card delinquency rate, quarterly) (https://fred.stlouisfed.org/graph/fredgraph.csv?id=NYUR)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `complaint_id` | integer | 11,340,030 to 24,147,261 |  | base | Unique CFPB complaint ID |
| `date_received` | text/id | 559 distinct |  | base | Date the CFPB received the complaint (YYYY-MM-DD) |
| `date_sent` | text/id | 558 distinct |  | base | Date the CFPB routed the complaint to the company |
| `product` | categorical | 11 distinct |  | base | Product category (11 values, e.g. Credit reporting, Debt collection, Credit card, Mortgage) |
| `sub_product` | text/id | 46 distinct |  | base | Finer product type (46 values) |
| `issue` | text/id | 64 distinct |  | base | Consumer's stated issue (64 values, e.g. Incorrect information on your report) |
| `sub_issue` | text/id | 134 distinct | 2.0% | base | Finer issue type |
| `company` | text/id | 264 distinct |  | base | Company the complaint was sent to (264 distinct in this sample) |
| `state` | categorical | NY |  | base | Consumer state; always NY in this extract |
| `zip_code` | text/id | 729 distinct |  | base | Consumer 5-digit ZIP; partially masked (see caveats) |
| `tags` | categorical | Older American, Older American, Servicemember, Servicemember | 98.4% | base | Servicemember and/or Older American flag; blank otherwise |
| `submitted_via` | categorical | Phone, Postal mail, Referral, Web |  | base | Channel: Web, Referral, Phone, Postal mail |
| `company_response` | categorical | Closed with explanation, Closed with monetary relief, Closed with non-monetary relief, In progress, Untimely response |  | base | How the complaint closed: Closed with explanation / non-monetary relief / monetary relief, In progress, Untimely response |
| `timely_response` | categorical | No, Yes |  | base | Yes/No, whether the company responded within the required window |
| `nyur_unemployment_rate` | numeric | 4.1 to 4.6 | 14.4% | FRED (NY unemployment rate |  |
| `drcclacbs_cc_delinquency_rate` | numeric | 2.92 to 3.06 | 73.3% | FRED (NY unemployment rate |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **FRED (NY unemployment rate, monthly; credit-card delinquency rate, quarterly)** — left join on the month of date_received; the newest 1-2 months have no published value yet. Adds: `nyur_unemployment_rate`, `drcclacbs_cc_delinquency_rate`.
