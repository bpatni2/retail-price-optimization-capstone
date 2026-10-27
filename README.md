# Retail Price Optimization Capstone

Repository: https://github.com/bpatni2/retail-price-optimization-capstone

## Project Overview

This capstone examines competitive retail price positioning and develops preliminary demand-prediction models using public product-month data. The demand target is `qty`, while `unit_price` is treated as a pricing decision variable. The project uses chronological validation, explicit leakage controls, and conservative interpretation of observational relationships.

The current project phase provides data validation, exploratory analysis, sample-size sensitivity analysis, formal statistical tests, and preliminary model comparisons. Later price recommendations, if developed, will be constrained simulations of predicted revenue rather than proven causal uplift or profit optimization.

## Dataset

Source: [Retail Price Optimization on Kaggle](https://www.kaggle.com/datasets/suddharshan/retail-price-optimization)

Verified structure:

- 676 product-month observations
- 52 products
- 9 product categories
- 20 monthly periods
- January 2017 through August 2018
- 30 source columns
- No missing values
- No exact duplicate rows
- No duplicate product-month records

The public data publisher does not provide complete organizational provenance or a detailed generation method for every field. The dataset is therefore treated as an anonymized analytical case-study dataset rather than independently verified raw company data.

## Research Questions

1. Does mean relative price differ across product categories?
2. How are unit price, competitor price, freight price, product score, and justified controls associated with sales quantity?
3. Can preliminary predictive models improve out-of-time quantity prediction over simple baselines?
4. Is there an interaction between product category and competitive-price position in relation to quantity sold?

## Repository Structure

- `data/raw`: Original data or data-access instructions
- `data/processed`: Analysis-ready data and metadata
- `notebooks`: Analysis notebooks in execution order
- `reports/figures`: Report-ready figures
- `reports/tables`: Report-ready result tables
- `outputs`: Executed notebook exports and interim report, when available

## Notebook Execution Order

1. `notebooks/01_data_understanding.ipynb`
2. `notebooks/02_eda_and_preprocessing_updated.ipynb`
3. `notebooks/03_statistical_analysis_and_preliminary_models.ipynb`

## Data Preparation and Leakage Controls

- Dates are validated from January 2017 through August 2018.
- `total_price` is excluded from demand predictors because it contains current quantity information and showed inconsistencies with `qty * unit_price`.
- The publisher-provided `lag_price` is excluded pending validation.
- Historical features use product-level chronological shifts so future values are not used.
- Predictive preprocessing is fitted on training data inside scikit-learn pipelines.
- A chronological train-validation-test split is used instead of random splitting.

## Chronological Split

- Train: 418 rows, January 2017 through February 2018
- Validation: 138 rows, March through May 2018
- Test: 120 rows, June through August 2018

The test period remained untouched during preliminary model selection.

## Preliminary Findings

- Relative price differs across product categories in preliminary omnibus tests.
- Welch ANOVA statistic: approximately 15.11, with `p < .001`.
- Descriptive eta-squared: approximately 0.168.
- The conditional log-unit-price coefficient is approximately -0.0042 and is interpreted as an association rather than a causal effect.
- The previous-quantity baseline achieved the best validation performance: MAE approximately 8.93, RMSE approximately 13.68, and R-squared approximately 0.457.
- Ridge regression, Random Forest, and Histogram Gradient Boosting did not improve validation RMSE over the previous-quantity baseline.
- The category by competitive-price-position analysis is exploratory because five cells contain fewer than five observations.

## Setup

Create a Python environment and install dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks sequentially from the `notebooks` folder.

## Important Limitations

- The data are aggregated at product-month level rather than transaction level.
- The same products appear repeatedly across months, so observations are not fully independent.
- Historical associations do not establish causal price effects.
- The dataset does not contain reliable product cost or margin data.
- Revenue simulation is not profit optimization.
- Simulated uplift does not represent realized business impact.
- The public dataset has limited organizational provenance.

## Interim Report

The supplied project archive did not include `Retail_Price_Optimization_Interim_Report.pdf`, `PROJECT_CONTEXT_README.md`, or the optional HTML notebook exports. These files have not been fabricated. The intended report location is `outputs/Retail_Price_Optimization_Interim_Report.pdf` when the report becomes available.

## Author

Bhupesh Patni  
QM640 Data Analytics Capstone  
Walsh College
