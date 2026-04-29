# ATUS Time-Use Analysis

Comparing daily time-use patterns across undergrads, graduate students, and employed new-grads using American Time Use Survey data. DS340H Spring 2026 Capstone.

## Research Question

What distinguishes the ways undergrads, graduate students, and new-grads spend their time?

## Data

[American Time Use Survey (ATUS)](https://www.bls.gov/tus/data.htm) public-use microdata, years 2015–2019 and 2023–2024. Ages 20–26. Final analysis sample N = 2,067 across three proxy groups:

- **Undergrad** (n=1,044): enrolled in college, no bachelor's yet
- **Graduate** (n=220): enrolled in college, bachelor's or higher
- **Employed New-Grad** (n=803): not enrolled, employed, bachelor's or higher

### Downloading the data

Data files are not tracked in this repo (too large, public-use microdata). Before running, download from BLS:

1. Visit https://www.bls.gov/tus/data.htm
2. Under each year (2015, 2016, 2017, 2018, 2019, 2023, 2024) download the **CPS file**, **Activity Summary file**, and **Respondent file**
3. Place all `.dat` files into a `data/` folder at the project root

Required files:
```
data/atuscps_YYYY.dat       # CPS demographic / education
data/atussum_YYYY.dat       # activity summary (time-use columns t01–t18)
data/atusresp_YYYY.dat      # respondent-level variables
```
where `YYYY` ∈ {2015, 2016, 2017, 2018, 2019, 2023, 2024}.

Records are linked across files by `TUCASEID`.

## Activity Buckets

Time-use columns (`t01`–`t18`) are grouped into 6 buckets:

- `personal_care` — sleep, grooming, eating
- `leisure_rec` — leisure, sports, socializing
- `work` — paid + educational work
- `domestic_cares` — household chores, care of household members
- `community_cares` — volunteering, civic activity
- `data_codes` — unclassified / NA time

Each respondent's daily total sums to 1,440 minutes.

## Methods

1. **Multinomial logistic regression** predicting group membership from background variables alone (sex, year, weekend, school break) vs. background + activity buckets
2. **Likelihood Ratio Test** comparing the nested models — confirms activities improve group prediction
3. **Two-part (hurdle) models** for each activity bucket:
    - **Logit** for participation (P(y > 0)) — produces average marginal effects in percentage points
    - **OLS on positive subset** for intensity (E[y | y > 0]) — log-transformed for skewed buckets (`domestic_cares`, `community_cares`, `data_codes`); raw minutes otherwise
4. **Diagnostics:** ROC + calibration + Pearson residuals for logit; residuals vs fitted, Q-Q, scale-location, residual histograms for OLS
5. **Reference group** for all coefficients: Undergrad

## Running

```bash
jupyter notebook notebooks/atus_modeling.ipynb
```

Run cells top to bottom. Order:
1. Data loading & bucket prep
2. EDA (occupations, weekend/break, daily allocation)
3. Multinomial logit + LRT
4. Hurdle models + log transform + final coefficient heatmap
5. Diagnostics
6. Results visualizations (sina plot, predicted profiles)

## References

Bureau of Labor Statistics, U.S. Department of Labor. *American Time Use Survey*, 2015–2019 and 2023–2024. https://www.bls.gov/tus/data.htm
