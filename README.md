# 🏠 House Prices Prediction Project

This repository contains a Computational Statistics project based on the Kaggle **House Prices: Advanced Regression Techniques** dataset.

The objective is to understand and predict residential house prices using a complete statistical workflow: classical inference, ANOVA, factorial design, parametric regression, and a neural network model.

---

## 🎯 Project Objective

The main goal of this project is to predict `SalePrice`, the final sale price of houses.

However, the project is not only about prediction. It also aims to understand which housing characteristics have the strongest influence on price.

The analysis answers questions such as:

- Which variables significantly affect house prices?
- Do quality-related variables interact with each other?
- How well can a linear regression model explain prices?
- Can a neural network improve predictive performance?
- How can we generate a valid Kaggle `submission.csv` file?

---

## 📊 Dataset

The project uses the Kaggle **House Prices: Advanced Regression Techniques** dataset.

The dataset contains information about houses, including:

- overall material and finish quality,
- exterior quality,
- kitchen quality,
- basement quality,
- living area,
- basement size,
- fireplace quality,
- central air conditioning,
- sale year and month,
- final sale price.

The target variable is `SalePrice`.

Since `SalePrice` is strongly right-skewed, a logarithmic transformation was applied:

**LogSalePrice = log(1 + SalePrice)**

This transformation makes the target variable closer to a normal distribution and is also consistent with the Kaggle evaluation metric, which uses RMSE on log-transformed prices.

---

## 🧠 Project Workflow

The project is organized into six main parts.

---

## 1️⃣ Data Overview and Target Transformation

The first step was to explore the distribution of the original `SalePrice` variable.

The original distribution was strongly right-skewed, meaning that most houses had moderate prices, while a smaller number of houses were very expensive.

To make the target variable easier to model, `SalePrice` was transformed into `LogSalePrice`.

### Main result

- Original `SalePrice` skewness: approximately **1.883**
- New `LogSalePrice` skewness: approximately **0.121**

This transformation made the target variable much closer to a normal distribution.

---

## 2️⃣ Classical Statistical Inference

In this part, classical statistical methods were applied to the transformed target variable `LogSalePrice`.

The analysis included:

- sample mean,
- sample variance,
- confidence interval,
- one-sample hypothesis test,
- exploration of `GrLivArea`.

### Main results

| Statistic | Value |
|---|---:|
| Mean of `LogSalePrice` | 12.0241 |
| Variance of `LogSalePrice` | 0.1596 |
| 95% Confidence Interval | [12.0036, 12.0445] |
| t-statistic | 2.3012 |
| p-value | 0.0215 |

The hypothesis test showed that the mean of `LogSalePrice` is significantly different from 12 at the 5% significance level.

---

## 3️⃣ ANOVA — Finding Significant Features

One-way ANOVA was used to identify which variables have a statistically significant effect on `LogSalePrice`.

### Significant features

The following variables were found to be significant:

- `OverallQual`
- `ExterQual`
- `KitchenQual`
- `BsmtQual`
- `CentralAir`
- `LotShape`
- `FireplaceQu`

### Non-significant features

The following variables were not significant in the one-way ANOVA analysis:

- `LandSlope`
- `MoSold`
- `YrSold`

A two-way ANOVA was also performed to study interaction effects between significant variables. Most tested interactions were significant, showing that house prices are influenced not only by individual features, but also by combinations of quality-related features.

---

## 4️⃣ 2^k Factorial Design

A `2^3` factorial design was applied using three selected factors:

| Factor | Variable | Meaning |
|---|---|---|
| A | `OverallQual` | Overall house quality |
| B | `CentralAir` | Central air conditioning |
| C | `BsmtQual` | Basement quality |

Each factor was converted into a low/high binary variable.

The factorial analysis showed that the highest average prices were obtained for houses with:

**High overall quality + central air conditioning + good/excellent basement quality**

The factorial ANOVA showed that all three main effects were statistically significant. However, the interaction effects were not significant in this simplified factorial design.

---

## 5️⃣ Parametric Regression

A parametric regression model was built using selected significant variables from ANOVA and two required numerical variables:

- `GrLivArea`
- `TotalBsmtSF`

The main model was an Ordinary Least Squares regression model.

### OLS model results

| Metric | Value |
|---|---:|
| R² | 0.816 |
| Adjusted R² | 0.815 |
| Training RMSE on `LogSalePrice` | 0.1713 |

The model showed that house quality, living area, basement size, and comfort-related variables are important predictors of house prices.

### Validation comparison

Linear Regression, Ridge Regression, and Lasso Regression were compared on a validation set.

| Model | Validation RMSE | Validation R² |
|---|---:|---:|
| Linear Regression | 0.172853 | 0.839891 |
| Ridge Regression | 0.172873 | 0.839854 |
| Lasso Regression | 0.173128 | 0.839381 |

The standard Linear Regression model slightly outperformed Ridge and Lasso on the validation set.

---

## 6️⃣ Neural Network Model

The final predictive model is a neural network trained using all available features.

The neural network preprocessing pipeline included:

- feature engineering,
- log transformation of skewed numerical features,
- missing value treatment,
- one-hot encoding of categorical variables,
- feature scaling,
- target scaling,
- hyperparameter tuning,
- early stopping.

### Best neural network configuration

| Parameter | Value |
|---|---|
| Architecture | `(256, 128)` |
| Alpha | 0.001 |
| Learning rate | 0.001 |
| Optimizer | Adam |
| Early stopping | Enabled |

### Neural network validation performance

| Metric | Value |
|---|---:|
| Validation RMSE | 0.1537 |
| Validation R² | 0.8735 |

The neural network achieved better validation performance than the parametric regression benchmark.

The final neural network model was used to generate the Kaggle submission file.

---

## 📈 Visualizations

The project includes several figures to support the analysis:

- `SalePrice` distribution,
- `LogSalePrice` distribution,
- `GrLivArea` distribution,
- ANOVA p-values,
- factorial interaction plots,
- OLS actual vs predicted plot,
- OLS residual diagnostics,
- neural network loss curve,
- neural network validation predictions,
- neural network validation residuals.

All figures are stored in:

`outputs/figures/`

---

## 📁 Repository Structure

```text
house-prices-project/
│
├── data/
│   ├── train.csv
│   ├── test.csv
│   ├── sample_submission.csv
│   └── data_description.txt
│
├── notebooks/
│   └── project_IONID.ipynb
│
├── outputs/
│   ├── submission.csv
│   └── figures/
│       ├── saleprice_distribution.png
│       ├── logsaleprice_distribution.png
│       ├── grlivarea_distribution.png
│       ├── anova_pvalues.png
│       ├── factorial_interaction_plots.png
│       ├── ols_actual_vs_predicted.png
│       ├── ols_residual_diagnostics.png
│       ├── nn_loss_curve.png
│       ├── nn_validation_actual_vs_predicted.png
│       └── nn_validation_residual_distribution.png
│
├── report/
│   └── house_price_project.pdf
│
├── requirements.txt
└── README.md
