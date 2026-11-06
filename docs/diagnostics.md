# Model diagnostics and robustness

## Residual autocorrelation
The essay reports full-sample Durbin–Watson statistics of **0.229 for corn, 0.231 for soybeans, and 0.313 for wheat**. Residual ACF and Ljung–Box diagnostics likewise raise concerns about serial dependence. Newey–West HAC standard errors help adjust inference for dependence but **do not eliminate autocorrelation** or fix missing dynamic structure.

## Rolling-window sensitivity
The study plots the `WTI_DROUGHT` coefficient with 48-, 60- and 72-month windows. Central patterns are sometimes similar, but sharp spikes and sign changes near event boundaries suggest sensitivity to window composition. Limited variation in the drought dummy within a rolling window can make an interaction poorly identified.

## Event-split sensitivity
Before/after comparisons cover RFS, 2012 drought, trade war, COVID-19 and Russia–Ukraine conflict. The essay notes very large RFS coefficient differences, which should not be interpreted as causal policy effects: a dummy may have no variation on one side of an event cutoff.

## Future tests — not completed
- Add lagged dependent and macroeconomic terms and reassess residual dependence.
- Report uncertainty intervals and identification flags for rolling coefficients.
- Use comparable pre/post windows and avoid plotting unidentifiable coefficients as zero.
- Test cross-regime differences formally in a correctly specified pooled model.
