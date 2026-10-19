# Credit Default Association Using Chi-Square and Cramer's V

A statistics practice project in Excel. It tests whether a loan applicant's checking-account status is associated with defaulting (bad credit risk), using a chi-square test of independence, and then measures how strong that association is with Cramer's V. The data is 1,000 loan applicants from the German Credit dataset.

## Method

1. **Describe the data.** Build a 4 x 2 table of observed counts: checking-account status by outcome (good / bad), with the bad rate for each group.
2. **Hypotheses.**
   - H0: Checking-account status is not associated with default.
   - Ha: Checking-account status is associated with default.
3. **Expected counts under H0.** Expected = row total x column total / grand total.
4. **Check assumptions.** Every expected count is at least 5 (Cochran's rule), observed and expected totals match, observations are independent, and the categories are mutually exclusive.
5. **Test statistic.** Chi-square = sum of (observed - expected)^2 / expected, with df = (4 - 1)(2 - 1) = 3. The p-value comes from `CHISQ.DIST.RT` and is cross-checked with `CHISQ.TEST`.
6. **Effect size.** Cramer's V = sqrt(chi-square / (n x min(r - 1, c - 1))).

## Data source

[UCI Machine Learning Repository: Statlog (German Credit Data)](https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data), dataset 144. Donated by Prof. Hans Hofmann, Universitat Hamburg (1994). License: CC BY 4.0. It has 1,000 applicants and 21 columns (700 good, 300 bad), with no missing values.

## Workbook

`Credit_Default_Association_Using_Chi_Square_and_Cramers_V.xlsx`

| Sheet | Contents |
|---|---|
| README | Dataset documentation and notes |
| Data | 1,000 applicants with codes decoded to labels, plus a 0/1 `bad` column |
| Assumptions | Observed and expected tables, assumption checks, chi-square test and Cramer's V |
| Data_RawCodes | The same rows with the original UCI codes (A11, A12, ...) |
| Codebook | Every variable, its type and what each code means |

## How to run

Open the workbook in Microsoft Excel 2010 or later (it uses `CHISQ.DIST.RT`, `CHISQ.TEST` and `CHISQ.INV.RT`). You don't need any other software.

## Key results

| Checking status | Good | Bad | Total | Bad rate |
|---|---:|---:|---:|---:|
| < 0 DM | 139 | 135 | 274 | 49.3% |
| 0 to < 200 DM | 164 | 105 | 269 | 39.0% |
| >= 200 DM or salary assignment | 49 | 14 | 63 | 22.2% |
| No checking account | 348 | 46 | 394 | 11.7% |
| **Total** | **700** | **300** | **1,000** | **30.0%** |

| Statistic | Value |
|---|---:|
| Chi-square | 123.72 |
| df | 3 |
| p-value | 1.22e-26 |
| Critical value (alpha = 0.05) | 7.81 |
| Cramer's V | 0.35 |

- **Decision:** p < 0.05, so H0 is rejected. Checking-account status is associated with default.
- **Effect size:** A Cramer's V of 0.35 is a medium association. The bad rate falls from 49% for applicants with a negative balance to 12% for applicants with no checking account.
- All assumptions are met. The smallest expected count is well above 5.
