# Data acquisition, MySQL and integration

## Goal and inputs
The study uses three crop-price series loaded from a local `crop_price.csv` attributed to USDA NASS, together with FRED macroeconomic series. The essay states 379 observations per crop (1,137 crop–month rows), although the effective model sample may differ because FRED retrieval begins in January 1996 and regime classification excludes some dates.

| Input | Role | Verification still needed |
|---|---|---|
| USDA-derived crop price CSV | Dependent variable `price`; crop/date keys | Exact NASS query, units, original download date |
| FRED `MCOILWTICO` | WTI oil price | Aggregation of daily to monthly frequency |
| FRED `FEDFUNDS` | Federal funds rate | Frequency and alignment |
| FRED `TWEXB` | Trade-weighted dollar index | Sparse overlap and historical coverage |
| FRED `CPIAUCSL` | CPI/inflation proxy | Date-level YoY construction |
| FRED `INDPRO` | Industrial production/growth proxy | Date-level YoY construction |

## Technical challenge: learning SQL and connecting Python to MySQL
**Challenge (researcher-reported):** I was initially unfamiliar with SQL syntax and database connection setup. Moving a local CSV into MySQL and then using Python to retrieve the records introduced several practical difficulties: connection configuration, matching column types, checking dates, and joining data from different sources.

**Process to document honestly:**
1. Identify the required database fields: `date`, `commodity_desc`, `price`.
2. Create or inspect a table with compatible date and numeric types.
3. Import crop-price rows and check the number of records by crop.
4. Use a Python database client to query records into pandas.
5. Merge monthly macroeconomic data by date; check unmatched dates and duplicate keys.
6. Compare SQL counts against pandas counts to detect accidental duplication.

The following is an **illustrative verification query**, not a preserved query from the original project:

```sql
SELECT commodity_desc,
       COUNT(*) AS observations,
       MIN(date) AS first_month,
       MAX(date) AS last_month
FROM crop_prices
GROUP BY commodity_desc;
```

And a suggested pandas merge check:

```python
assert df_crop[['date', 'commodity_desc']].duplicated().sum() == 0
assert df_macro['date'].duplicated().sum() == 0
panel = df_crop.merge(df_macro, on='date', how='left', validate='many_to_one')
print(panel.groupby('commodity_desc').size())
```

**Lessons learned:** A successful database connection is not the same as a correct analytical dataset. Row counts, join cardinality, date formats, units and frequency must all be verified before modeling.

## Credential safety
Do not publish database passwords, FRED API tokens or other credentials in a public repository. Replace them with environment variables and rotate any secrets previously exposed. Provide a `.env.example` containing placeholder names, never real values.
