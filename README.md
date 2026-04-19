# house-prices-project 
# 🏠 House Prices Project

## 📌 Objective
The objective of this project is to predict house sale prices using statistical methods and machine learning techniques.  
The analysis is based on the Ames Housing dataset and follows a structured approach combining classical statistics and modern modeling.

---

## 📊 Dataset
- Source: *House Prices: Advanced Regression Techniques (Kaggle)*
- Files used:
  - `train.csv`
  - `test.csv`
  - `data_description.txt`

---

## 🧠 Methodology

The project is divided into five main parts:

### 1. Classical Statistical Inference
- Descriptive statistics (mean, variance)
- Confidence intervals
- Hypothesis testing

### 2. ANOVA (Analysis of Variance)
- Identify significant features affecting house prices
- Study main effects and interactions

### 3. Factorial Design (2^k)
- Analyze combined effects of selected features
- Evaluate interactions between variables

### 4. Parametric Regression
- Build linear regression models
- Interpret coefficients and model performance

### 5. Non-Parametric Model (Neural Network)
- Train a neural network using all features
- Generate predictions for Kaggle submission

---

## ⚙️ Data Preprocessing

- Handling missing values
- Encoding categorical variables
- Feature selection
- Log transformation of the target variable (`SalePrice`)

---

## 📈 Evaluation Metric

The model is evaluated using **Root Mean Squared Error (RMSE)** on the logarithm of predicted and actual prices:

\[
RMSE = \sqrt{\frac{1}{n} \sum (\log(y_i + 1) - \log(\hat{y}_i + 1))^2}
\]

---
## 🚀 How to Run

1. Clone the repository ,Install dependencies:
```bash
git clone https://github.com/Ziedellouzi/house-prices-project.git

pip install -r requirements.txt
