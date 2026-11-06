# Missing-data investigation and imputation

## Reported data audit
The essay reports 1,137 crop–month records: 379 per crop. `USD_INDEX` is missing in 1,017 rows (89.4%), WTI and FFR in 36 each (3.2%), and CPI in 39 (3.4%). The crop prices themselves were not imputed. Only 40 records per crop were complete across regression variables, so complete-case deletion would discard most observations.

The researcher compared missingness with histograms, a full-panel heatmap, and crop-specific price distribution/boxplots using ±1σ, ±2σ, and ±3σ ranges. Most rows with missing explanatory variables had ordinary, not extreme, crop-price values. **This does not prove missing-at-random.**

## Actual imputation method
The supplied code calls:

```python
imputer = IterativeImputer(random_state=42)
```

Because no `estimator=` argument is passed, scikit-learn's default conditional estimator is **BayesianRidge**. The procedure iteratively fills missing explanatory variables and returns a single completed dataset in this implementation. The final crop-price regressions are **OLS**, not Bayesian ridge regressions. This is not pooled multiple-imputation inference.

## Challenge and trade-off
The main technical problem was preserving sample coverage without silently assuming the missing data were harmless. Imputation made the models estimable, but with 89.4% of dollar-index entries imputed, dollar-related coefficient interpretation is highly assumption-dependent.

**Recommended but not yet demonstrated:** re-estimate models excluding `USD_INDEX`, compare alternative imputation strategies, and report sensitivity of coefficient signs and intervals. Never label these proposed checks as completed tests.
