# Did the Ads Work? A/B Test of a Marketing Campaign

A beginner-friendly A/B testing project in Python that measures whether an ad campaign actually increased purchases, using a control group that saw a Public Service Announcement (PSA) instead of ads.

## Business Question

Did showing ads make more users buy, and if so, by how much?

## Dataset

[Kaggle: Marketing A/B Testing](https://www.kaggle.com/) (`marketing_AB.csv`), with 588,101 users.

| Column | Description |
|---|---|
| `user id` | Unique user identifier |
| `test group` | `ad` (treatment) or `psa` (control) |
| `converted` | Whether the user bought (True/False) |
| `total ads` | Number of ads the user saw |
| `most ads day` | Day of the week the user saw the most ads |
| `most ads hour` | Hour of the day the user saw the most ads |

**Groups:** 564,577 users in the ad group and 23,524 users in the PSA control group (about 4%).

## Approach

1. **Load and clean the data:** tidy column names, convert `converted` to 1/0, check for missing values and duplicate users.
2. **Compare conversion rates** between the two groups.
3. **Hypothesis test:** two-proportion z-test.
   - H0: ads make no difference to conversion rate
   - H1: conversion rates are different
   - Significance level: 0.05
4. **Estimate the effect size** with a 95% confidence interval and relative lift.
5. **Translate to business impact:** extra conversions and extra revenue.
6. **Exploratory analysis:** conversion rate by number of ads seen.

## Key Results

| Metric | Value |
|---|---|
| Ad group conversion rate | 2.55% |
| PSA group conversion rate | 1.79% |
| Absolute difference | +0.77 percentage points (95% CI: +0.60 to +0.94) |
| Relative lift | +43% |
| z-statistic | 7.37 |
| p-value | 1.7e-13 (reject H0) |
| Extra conversions caused by ads | about 4,343 (roughly 30% of ad group conversions) |
| Extra revenue | about $217K, assuming $50 per conversion |

**Conclusion:** The ads significantly increased conversion compared with the PSA control.

**Exploratory finding:** Up to about 25 ads seen, both groups convert at similar rates. Above 50 ads seen, the ad group converts far more (for example, 11.63% vs 5.77% at 51-100 ads). This is a pattern only and not proof of cause, because ads seen is measured after users are assigned to groups.

## Limitations

- Revenue per conversion ($50) is an assumption, not in the data.
- Campaign cost is unknown, so profit cannot be calculated.
- The control group is small (4% of users), so its estimate is less precise.
- The exposure analysis is exploratory and may be confounded by user engagement.
- Randomization cannot be verified from the data provided.

## Next Steps

- Compare extra revenue with campaign cost to estimate ROI.
- Test whether showing fewer ads to light users saves money without losing sales.

## Tools

Python, pandas, NumPy, matplotlib, statsmodels (Jupyter / Google Colab)

## Repository Contents

- `beginner_ab_test_project.ipynb`: full analysis notebook
- `ab_test_project_presentation.pptx`: summary presentation (7 slides)

## How to Run

1. Download `marketing_AB.csv` from Kaggle and place it in the same folder as the notebook (or upload it when prompted in Google Colab).
2. Install dependencies: `pip install pandas numpy matplotlib statsmodels`
3. Open the notebook and run all cells.
