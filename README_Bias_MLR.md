# CRJA Multiple Linear Regression Bias Analysis

Statistical analysis tools for California Racial Justice Act (CRJA) compliance, detecting sentencing disparities between racial groups.

## Overview

This project provides two Jupyter notebooks that transform raw CDCR data into court-ready evidence of racial bias in sentencing:

1. **Data Preparation** - Aggregates offense history into one row per person
2. **MLR Analysis** - Tests for sentencing disparities while controlling for legally relevant factors

## Requirements

```
pandas
numpy
statsmodels
```

## Workflow

### Step 1: Prepare Analysis Data

**Notebook:** `01_prepare_analysis_data.ipynb`

**Input:** 
- demographics.csv (95k+ individuals)
- current_commitments.csv (369k+ rows)
- prior_commitments.csv (191k+ rows)

**Output:** 
- `analysis_data.csv` - One row per person with all features pre-calculated

**What it does:**
- Counts current offenses by category per person
- Counts prior offenses by category per person
- Flags enhancements and in-prison offenses
- Caps sentences at 1080 months (90 years)
- Merges everything into one clean dataset

**Runtime:** ~2-3 minutes

---

### Step 2: Run MLR Analysis

**Notebook:** `02_mlr_bias_analysis.ipynb`

**Input:** 
- `analysis_data.csv` (from Step 1)

**Output:** 
- Regression results with disparity estimate
- Model diagnostics

**What it does:**
- Filters to Black vs White defendants
- Runs multiple linear regression controlling for:
  - Current offense counts by category
  - Prior offense counts by category
  - Enhancements (current and prior)
  - In-prison offenses (current and prior)
  - Sentencing county
- Produces court-ready disparity estimate with confidence interval and p-value

**Runtime:** ~30 seconds

---

## Interpreting Results

### Key Output

```
Adjusted Difference: 4.54 months
95% Confidence Interval: [1.34, 7.73]
P-value: 0.0053
```

**Translation:** After controlling for all measurable legally relevant factors, Black defendants receive sentences that are 4.54 months longer than White defendants. This difference is statistically significant (p < 0.01).

### Model Diagnostics

- **Durbin-Watson ≈ 2.0:** No autocorrelation (good)
- **Breusch-Pagan p < 0.05:** Heteroscedasticity present but handled with HC3 robust standard errors
- **R² ≈ 0.25-0.30:** Typical for sentencing data

---

## Usage

1. Run `01_prepare_analysis_data.ipynb` top to bottom
2. Verify `analysis_data.csv` was created
3. Run `02_mlr_bias_analysis.ipynb` top to bottom
4. Extract disparity estimate for court filing

---

## Customization

To compare different groups, edit `02_mlr_bias_analysis.ipynb`:

```python
exposed = "White"      # Reference group
unexposed = "Hispanic" # Comparison group
```

---

## Project Structure

```
├── 01_prepare_analysis_data.ipynb  # Data aggregation
├── 02_mlr_bias_analysis.ipynb      # MLR model
├── analysis_data.csv                # Prepared dataset (generated)
└── README.md                        # This file
```

---
