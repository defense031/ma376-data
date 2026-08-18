# Online Retail

541,909 raw line items from one UK online retailer over a year: invoice, product, quantity, price, customer, country. No target variable exists until you build one.

**File.** `online_retail_enriched.csv` (541,909 rows x 10 columns, assembled from the sources below)

## Provenance
- Base data: UCI Machine Learning Repository, retrieved 12 Jul 2026. (https://archive.ics.uci.edu/dataset/352/online+retail)
- Merged in: Nager.Date UK public holidays, 2010-2011 (https://date.nager.at/api/v3/PublicHolidays/2010/GB)

## Column dictionary

| column | type | values | missing | source | meaning |
|---|---|---|---|---|---|
| `InvoiceNo` | text/id | 1,406 distinct |  | base | Invoice/transaction number. **Codes starting with `C` are CANCELLATIONS** — these pair with negative quantities and must be handled deliberately. |
| `StockCode` | text/id | 2,645 distinct |  | base | Product code. **A few codes are non-products** (e.g. `POST`/POSTAGE, `MANUAL`, `BANK CHARGES`, `DOTCOM POSTAGE`, `AMAZONFEE`, adjustments) — not catalog items. |
| `Description` | text/id | 2,586 distinct | 0.4% | base | Product name, free text. Inconsistent casing/spelling; some blank; some carry manual annotations rather than product names. |
| `Quantity` | integer | -9,360 to 2,880 |  | base | Units on the line. **NEGATIVE for returns and cancellations. |
| `InvoiceDate` | text/id | 1,209 distinct |  | base | Date and time of the transaction (01 Dec 2010 – 09 Dec 2011). |
| `UnitPrice` | numeric | 0 to 1.35e+04 |  | base | Price per unit in pounds sterling. **Some values are 0 or negative** (adjustments, freebies, bad rows). |
| `CustomerID` | integer | 12,347 to 18,269 | 33.5% | base | Customer identifier. **~135,000 rows are BLANK** — guest checkouts or unmatched orders that cannot be attributed to a customer. |
| `Country` | categorical | 19 distinct |  | base | Customer country. **Heavily dominated by United Kingdom;** the rest is a thin international tail. |
| `uk_holiday_name` | numeric |  | 100.0% | Nager.Date UK public holidays |  |
| `is_uk_holiday` | integer | 0 to 0 |  | Nager.Date UK public holidays |  |

## How the file was assembled
The base dataset was extended with the following merges. The base columns are unchanged;
every merged column is attributed in the table above.

1. **Nager.Date UK public holidays, 2010-2011** — left join on invoice date; is_uk_holiday is 0/1, holiday name blank on non-holidays by construction. Adds: `uk_holiday_name`, `is_uk_holiday`.
