# Regression design, interactions and multicollinearity

## Baseline analytical approach
The essay reports separate OLS regressions for corn, soybeans and wheat, and additional regressions within Merrill-clock regimes. HAC/Newey–West standard errors use `maxlags=12` in the supplied code. Coefficients describe **conditional associations**, not causal impacts.

## Technical difficulty: too many interaction variables
**Researcher-reported experiment:** I initially constructed interaction variables between Merrill-clock economic-regime indicators and macroeconomic explanatory variables, hoping to allow the oil-price, interest-rate and dollar-price relationships to differ across cycles. The resulting specification suffered from multicollinearity/numerical instability. I removed the broad set of cycle-by-macro interaction terms and used separate regressions for each regime in the reported analysis.

### Why the experimental interaction specification was still linear regression

An interaction between a regime dummy and a macroeconomic variable does **not** make the model nonlinear in its coefficients. For example, the *experimental* specification

\[P_t = \beta_0 + \beta_1 X_t + \beta_2 D_t + \beta_3(X_t D_t) + \varepsilon_t\]

is linear in the parameters and can be estimated by OLS. Here `D` is a regime indicator. This example illustrates the attempted idea; **it is not the final estimated specification**. In a pooled regression, one regime should serve as the reference when including an intercept. Redundant dummy coding or interacting variables within a single-regime subset can create exact collinearity.

### Final reported approach

The final essay reports **separate OLS linear regressions by crop and by economic regime**, with Newey–West HAC standard errors (`maxlags=12`). Broad regime-by-macro interactions were removed after multicollinearity concerns. Two targeted interactions, `WTI_DROUGHT` and `FFR_SEASON`, remained in the documented model. HAC changes standard-error estimation, not the linear OLS coefficient specification.

### What changed
| Design stage | Intended benefit | Difficulty / decision |
|---|---|---|
| Pooled OLS with macro regressors | Baseline conditional relationships | Retained as a comparison |
| Broad cycle × macro interactions | Directly model cycle-dependent slopes | Researcher reports multicollinearity; broad interactions removed |
| Separate OLS per regime and crop | Easier to describe within-regime patterns | Retained, but small and unequal samples limit reliability |
| `WTI_DROUGHT` and `FFR_SEASON` | Specific oil–drought and rate–season interactions | **Retained** in the essay; do not claim all interaction terms were deleted |

### Important precision
The original experimental model output, variance inflation factors, design-matrix rank, and exact deleted variable list are **not preserved in the supplied essay**. Therefore, the documentation should say the researcher *encountered* multicollinearity and revised the specification, not invent VIF numbers, error messages, or quantitative improvements.

### Recommended reproducibility diagnostics (not yet verified)
```python
import numpy as np
from statsmodels.stats.outliers_influence import variance_inflation_factor
X = model_matrix.dropna().astype(float)
print('rank:', np.linalg.matrix_rank(X), 'columns:', X.shape[1])
print('condition number:', np.linalg.cond(X))
vifs = {name: variance_inflation_factor(X.values, i)
        for i, name in enumerate(X.columns)}
print(vifs)
```

Interpret VIF and condition numbers with context; multicollinearity may reflect deterministic dummy coding, insufficient variation or correlated regressors. Removing interactions simplifies estimation but sacrifices direct pooled tests of slope differences. Separate-regime significance patterns do **not** by themselves establish that coefficients differ statistically between regimes.

## Other identification challenges
Recovery has 9 observations per crop and recession 21, compared with 242 in overheating and 91 in stagflation. Event dummies with no within-regime variation cannot be identified. Treat very large or highly significant estimates in tiny subsamples with caution.
