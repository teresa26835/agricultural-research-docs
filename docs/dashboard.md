# Excel → Power BI dashboard and reproducibility

The reported regression and diagnostic results were exported from Python to Excel and imported into Power BI Desktop. The dashboard follows the paper's seven-part analytical flow, including research overview, cycle framework, methodology, regression comparisons, missing-data analysis, model diagnostics, and conclusions/robustness.

## Technical difficulty: making an analytical report interactive
Challenges included converting dates to proper date types, controlling aggregation of coefficients, configuring economic-cycle slicers, and ensuring diagnostics responded to slicer selections. The researcher used Power BI Desktop to build the pages and configure interactions.

## Refresh architecture
```text
USDA-derived CSV + FRED
          ↓
      MySQL / pandas
          ↓
  Imputation + OLS/HAC
          ↓
      Excel exports
          ↓
 Power BI Desktop (.pbix)
          ↓
 GitHub project showcase / controlled embed
```

To preserve the dashboard layout during a future correction, retain the Excel workbook's sheet names, field names and data types, then use **Home → Refresh**. Check any static images and slicer relationships separately. The current dashboard is based on the **original exploratory model outputs**, not corrected regime labels.

## Reproducibility manifest to publish
- Redacted Python source and `requirements.txt`.
- Data dictionary with units, frequencies and provenance URLs.
- Sample input schema (not sensitive raw data).
- Excel output sheet/column dictionary.
- Model specification, random seeds, diagnostics and limitations.
- Screenshots of dashboard pages and public link/access requirements.

Do not publish passwords, API keys, private databases, or misleadingly complete replication claims.
