# Medical Insurance Cost Prediction: Multiple Linear Regression

A statistics project for **SAIA1173 (Probability and Statistics)** that uses Multiple Linear Regression (MLR) to quantify how age, BMI, number of children, smoking status and sex influence individual medical insurance charges.

## Problem Statement

> *To what extent can age, BMI, number of children, smoking status, and sex predict individual medical insurance charges using Multiple Linear Regression?*

## Objectives

1. Perform descriptive statistical analysis and data visualisation on the dataset.
2. Examine the correlation between each predictor and insurance charges.
3. Build an MLR model that predicts insurance charges.
4. Evaluate the model using R², Adjusted R², the ANOVA F-test and residual diagnostics.
5. Identify the most significant predictors and discuss their practical implications.

## Dataset

**Medical Insurance Cost** dataset ([Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance), originally from Brett Lantz, *Machine Learning with R*).

- 1,338 records, 7 columns, no missing values

| Variable | Role | Type | Description |
|---|---|---|---|
| `charges` | Dependent (Y) | Numerical | Individual medical costs billed by insurance (USD) |
| `age` | Independent | Numerical | Age of the primary beneficiary |
| `bmi` | Independent | Numerical | Body mass index (kg/m²) |
| `children` | Independent | Numerical | Number of dependants covered |
| `smoker` | Independent | Categorical (yes = 1, no = 0) | Smoking status |
| `sex` | Independent | Categorical (male = 1, female = 0) | Sex of the beneficiary |
| `region` | Not used | Categorical | Residential area in the US |

## Methodology

1. **Load and inspect** the data, checking types and missing values
2. **Preprocess** by encoding `sex` and `smoker` as binary variables
3. **Descriptive statistics** including mean, standard deviation, coefficient of variation, skewness and kurtosis
4. **Visualisation** with histograms, scatter plots with trend lines and boxplots by group
5. **Correlation analysis** using a Pearson correlation matrix and significance tests
6. **MLR model** fitted with OLS (`statsmodels`)
7. **Model evaluation** using the ANOVA table, R², Adjusted R², AIC/BIC, RMSE, residual diagnostics and VIF
8. **Sample prediction** for a new individual

## Key Results

| Metric | Value |
|---|---|
| R² | 0.7497 |
| Adjusted R² | 0.7488 |
| F-statistic | F(5, 1332) = 798.02, p < 0.001 |
| RMSE | USD 6,069.73 |
| AIC / BIC | 27,113.89 / 27,145.08 |

**Fitted equation**

```
charges = -12,052.46 + 257.74(age) + 322.36(bmi) + 474.41(children) + 23,823.39(smoker) - 128.64(sex)
```

**Findings**

- The overall model is statistically significant and explains about **75%** of the variation in charges.
- **Smoking status** is by far the strongest predictor (r = 0.787). Holding the other variables constant, smokers are billed roughly **USD 23,800 more** than non-smokers.
- **Age**, **BMI** and **number of children** are all significant positive predictors (p < 0.05).
- **Sex** is not statistically significant (p = 0.70).
- Multicollinearity is not a concern, as all VIF values are below 1.02.

## Repository Structure

```
.
├── SAIA1173_MLR_Analysis_.ipynb   # Full analysis notebook
├── insurance.csv                  # Dataset
├── README.md
└── .gitattributes
```

Running the notebook also generates figures (`fig1_...png` to `fig7_...png`) in the working folder.

## Getting Started

**Requirements:** Python 3.9+ and the following libraries:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

**Run:**

```bash
   git clone https://github.com/k1oooo/insurance-cost-mlr-analysis.git
   cd insurance-cost-mlr-analysis
   jupyter notebook SAIA1173_MLR_Analysis_.ipynb
```

Keep `insurance.csv` in the same folder as the notebook, then run all cells.

## Limitations and Possible Improvements

- Charges are right-skewed (skewness ≈ 1.52), so a log-transformed response could be tested.
- `region` was excluded from the model and could be added as dummy variables.
- Interaction terms (for example smoker × BMI) could capture effects that a purely additive linear model misses.
- The data is US-based, so the coefficients should not be applied directly to the Malaysian context.

## Tech Stack

Python · pandas · NumPy · statsmodels · SciPy · matplotlib · seaborn · Jupyter

## Author

**Faiz**, AI student. Course project for SAIA1173 Probability and Statistics.
