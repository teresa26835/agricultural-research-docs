# Limitations and open validation work

## Critical unresolved issue: time alignment of economic-cycle indicators
The code review identified that year-over-year changes for `INDPRO` and `CPI` were computed using `pct_change(12)` **after** macroeconomic observations were merged into a crop-level panel. Since a month can appear once per crop, a 12-row shift can be approximately a four-month shift when there are three crop rows per month, rather than a twelve-month change.

**Status:** This issue has been identified and disclosed; the date-level indicators and resulting regime assignments have **not been recomputed or independently validated**. Therefore, the current cycle counts, cycle-specific regressions, significance tests, and dashboard cycle comparisons must be treated as exploratory outputs.

### Proposed repair, not executed in the present research deliverable
```python
monthly = (df_macro[['date', 'INDPRO', 'CPI']]
           .drop_duplicates('date')
           .sort_values('date')
           .copy())
monthly['INDPRO_yoy'] = monthly['INDPRO'].pct_change(12) * 100
monthly['CPI_yoy'] = monthly['CPI'].pct_change(12) * 100
panel = df_crop.merge(monthly, on='date', how='left', validate='many_to_one')
# Recreate regime labels, rerun regression/diagnostics, update Excel and Power BI.
```

Before using a 12-row lag even on monthly data, verify consecutive monthly dates, no duplicates and the exact intended growth/inflation definitions.

## Other limitations
| Issue | Evidence | Consequence |
|---|---|---|
| Regime imbalance | 9 recovery vs 242 overheating observations per crop | Underpowered or unstable regime estimates |
| Dollar-index missingness | 1,017 / 1,137 values imputed | Dollar coefficients depend heavily on model assumptions |
| Serial dependence | DW 0.229 / 0.231 / 0.313 and residual ACF | Model dynamics may be incomplete |
| Event-dummy identification | Some events absent within subsamples | Coefficients may be unidentified or misleading |
| Data provenance | Original USDA CSV query not supplied | Units and exact source filters need verification |

## Validation checklist
- [ ] Confirm exact USDA Quick Stats series, units and extraction date.
- [ ] Verify all monthly keys and source-frequency transformations.
- [ ] Recalculate macroeconomic changes on unique monthly dates.
- [ ] Compare original and corrected regime labels.
- [ ] Rerun affected cycle regressions, diagnostics and sensitivity analyses.
- [ ] Evaluate imputation sensitivity without the dollar index.
- [ ] Refresh Power BI Excel inputs while preserving schema.
- [ ] Version the revised outputs and update the public working paper.

The unchecked boxes represent **future work**, not work claimed as completed.
