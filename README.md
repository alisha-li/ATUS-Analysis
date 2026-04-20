# ATUS Time-Use Analysis

Comparing daily time-use patterns across undergrads, graduate students, and employed new-grads using American Time Use Survey data. DS340H Spring 2026 Capstone.

## Research Question

What distinguishes the ways undergrads, graduate students, and new-grads spend their time?

## Data

[American Time Use Survey (ATUS)](https://www.bls.gov/tus/) public-use microdata (2015-2019, 2023-2024). Ages 20-26, N=2,067 respondents across three groups:

- **Undergrad** (n=1,044): enrolled in college, no bachelor's yet
- **Graduate** (n=220): enrolled in college, bachelor's or higher
- **Employed New-Grad** (n=803): not enrolled, employed, bachelor's or higher

Data files (CSV-formatted `.dat`, not tracked due to size) go in `data/`.

## Methods

1. Multinomial logistic regression predicting group from background + activity time
2. Likelihood ratio test comparing background-only vs. activity-inclusive model
3. Separate OLS regressions for each of 6 activity buckets (work, personal care, domestic cares, leisure/rec, community cares, data codes)

## Running

```bash
jupyter notebook notebooks/atus_modeling.ipynb
```

## References

Bureau of Labor Statistics, U.S. Department of Labor. *American Time Use Survey*. https://www.bls.gov/tus/
