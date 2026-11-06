# U.S. Agricultural Commodity Prices Across Business Cycles

**Project type:** Exploratory empirical analysis and data visualization  
**Crops:** Corn, soybeans, wheat  
**Historical coverage described in essay:** approximately 1995–2025  
**Methods:** USDA-derived price data, FRED macroeconomic series, MySQL/Python processing, iterative imputation, crop- and regime-specific OLS with HAC standard errors, residual diagnostics, Power BI.

## Research question
How do the statistical associations between U.S. agricultural prices and macroeconomic variables vary across four Merrill-clock economic regimes, and do these patterns differ across crops?

## Research workflow
1. Gather local USDA-derived crop price CSV and FRED macroeconomic series.
2. Load and query crop records through MySQL; standardize dates and merge monthly data.
3. Audit missing observations and compare price distributions.
4. Impute explanatory variables using `IterativeImputer(random_state=42)` (default estimator: BayesianRidge).
5. Construct regime labels from industrial production and CPI movements.
6. Estimate OLS regressions by crop and regime with Newey–West HAC standard errors (12 lags in supplied code).
7. Examine residual dependence (Durbin–Watson, ACF, Ljung–Box) and rolling/event-split sensitivity.
8. Export result tables to Excel and visualize in Power BI.

## What this site is — and is not
This documentation reconstructs the **reported** workflow from the essay and the researcher's stated experience. It is not a full executable reproduction because the original USDA extraction request, full dataset, SQL history, intermediate experiments, and verification logs are not supplied here. Do not interpret pseudocode or recommended checks as evidence they were already executed.

**Current status:** The cycle-specific results and dashboard are original exploratory outputs. A possible time-alignment problem in the year-over-year regime indicators has been identified but **not corrected or re-estimated**.

## Evidence provenance
- [USDA NASS Quick Stats](https://quickstats.nass.usda.gov/) — official agricultural price data portal.
- [FRED](https://fred.stlouisfed.org/) — macroeconomic series (`MCOILWTICO`, `FEDFUNDS`, `TWEXB`, `CPIAUCSL`, `INDPRO`).
- Essay: *U.S. Agricultural Commodity Prices Across Business Cycles* (user-provided revision 3).

## Research outputs
- **Working paper PDF:** add final public PDF URL.
- **Zenodo paper DOI:** add your published DOI URL.
- **Interactive Power BI dashboard:** add public or access-controlled URL with access note.
- **GitHub repository:** add repository URL.
