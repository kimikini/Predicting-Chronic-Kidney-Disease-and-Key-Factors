# Predictive Modeling of Chronic Kidney Disease and Analysis of Key Risk Factors

This project analyzes a **Chronic Kidney Disease (CKD)** dataset from the **UCI Machine Learning Repository** to identify important clinical risk factors and build a robust prediction model for CKD diagnosis. The study combines **exploratory data analysis, hypothesis testing, missing-data analysis, and logistic regression modeling** to evaluate both statistical relationships and predictive performance. :contentReference[oaicite:0]{index=0}

## Project Overview

The project is built around two main goals:

1. **Hypothesis 1 (H1):** Test whether mean blood pressure differs between patients with **good appetite** and **poor appetite**.
2. **Hypothesis 2 (H2):** Build a **multivariable logistic regression model** to predict CKD status and identify the most important clinical predictors. :contentReference[oaicite:1]{index=1}

A key contribution of this project is its focus on **missing-data robustness**. We evaluate how both inference and prediction behave under simulated **Missing Completely at Random (MCAR)** and **Missing Not at Random (MNAR)** settings. :contentReference[oaicite:2]{index=2}

## Contributors
- **Alan Rodriguez**
- **Xiaoyan Lin**
- **Yeonbi Han**
---

## Dataset

- **Source:** UCI Machine Learning Repository  
- **Samples:** 400 patients  
- **Variables:** 25 clinical variables  
- **Target:** CKD status (`ckd` vs `notckd`)  
- **Data characteristics:** mixed numerical and categorical features, uneven missingness, moderate class imbalance :contentReference[oaicite:3]{index=3}

Examples of variables used in the analysis include:

- **Numerical:** age, blood pressure (`bp`), blood glucose random (`bgr`), blood urea (`bu`), serum creatinine (`sc`), hemoglobin (`hemo`), specific gravity (`sg`)
- **Categorical:** appetite (`appet`), hypertension (`htn`), diabetes mellitus (`dm`), anemia (`ane`) :contentReference[oaicite:4]{index=4}

---

## Workflow

## 1. Data Preprocessing
- Load and inspect the CKD dataset
- Standardize missing-value symbols such as `"?"` into `NA`
- Summarize missingness across all variables
- Separate numerical and categorical variables for downstream analysis :contentReference[oaicite:5]{index=5}

## 2. Exploratory Data Analysis
- Examine target distribution
- Compute summary statistics
- Visualize missing-value counts
- Build a correlation heatmap for numeric variables
- Identify high-correlation pairs and potential multicollinearity issues :contentReference[oaicite:6]{index=6}

## 3. Hypothesis Testing (H1)
- Research question: **Does blood pressure differ by appetite group?**
- Use:
  - **F-test** for equality of variances
  - **Welch’s t-test** for mean comparison when variances are unequal
- For H1, missingness is low, so **listwise deletion** is used instead of imputation :contentReference[oaicite:7]{index=7}

## 4. Logistic Regression Modeling (H2)
- Select clinically relevant predictors
- Apply **dummy encoding** to categorical variables
- Use **KNN imputation** (`k = 5`) for missing predictor values
- Check multicollinearity with **Variance Inflation Factor (VIF)**
- Perform **backward stepwise AIC selection**
- Diagnose quasi-complete separation
- Remove **albumin (`al`)** due to instability
- Fit the final logistic regression model using:
  - **bgr**
  - **hemo**
  - **sg** :contentReference[oaicite:8]{index=8}

## 5. Model Evaluation
- Train/test split
- Confusion matrix
- Accuracy
- Sensitivity
- Specificity
- ROC curve
- AUC :contentReference[oaicite:9]{index=9}

## 6. Missing-Data Robustness Analysis
- Simulate **MCAR** at multiple missingness levels
- Simulate **MNAR** scenarios based on clinically motivated assumptions
- Re-run H1 and H2 after missing-data injection and KNN imputation
- Compare performance and statistical conclusions across scenarios :contentReference[oaicite:10]{index=10}

---

## Methods Used

- **Exploratory Data Analysis**
- **F-test**
- **Welch’s t-test**
- **KNN imputation**
- **Dummy encoding**
- **Variance Inflation Factor (VIF)**
- **Backward stepwise AIC**
- **Logistic regression**
- **ROC/AUC analysis**
- **MCAR/MNAR simulation** :contentReference[oaicite:11]{index=11}

---

## Key Results

### H1: Appetite vs Blood Pressure
- The F-test showed unequal variances between appetite groups
- Welch’s t-test found a **significant difference in mean blood pressure** between patients with good and poor appetite :contentReference[oaicite:12]{index=12}

### H2: CKD Prediction Model
- The final logistic regression model retained **three predictors**:
  - `bgr`
  - `hemo`
  - `sg`
- The final model achieved approximately:
  - **96.3% accuracy**
  - **AUC ≈ 0.993**
- This indicates strong discrimination between CKD and non-CKD patients :contentReference[oaicite:13]{index=13}

### Missing-Data Robustness
- H1 became less stable as missingness increased
- H2 remained highly robust under both **MCAR** and **MNAR** simulations
- The final multivariable model preserved strong predictive performance even under substantial missingness :contentReference[oaicite:14]{index=14}

---
## References

1. Bobbitt, Zach. “Understanding the Null Hypothesis for Logistic Regression.” *Statology*, 29 September 2021. Available at: `https://www.statology.org/null-hypothesis-of-logistic-regression/`. Accessed 24 November 2025.

2. “CHAPTER 25 Missing-data imputation.” *Columbia University*. Available at: `https://sites.stat.columbia.edu/gelman/arm/missing.pdf`. Accessed 24 November 2025.

3. “Chronic Kidney Disease.” *UCI Machine Learning Repository*. Available at: `https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease`. Accessed 24 November 2025.

4. “Stepwise Regression in Python.” *GeeksforGeeks*, 23 July 2025. Available at: `https://www.geeksforgeeks.org/machine-learning/stepwise-regression-in-python/`. Accessed 24 November 2025.

5. Tamhane, Ajit C., and Dorothy D. Dunlop. *Statistics and Data Analysis: From Elementary to Intermediate*. Prentice Hall, 2000. Accessed 24 November 2025.

6. James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). *An Introduction to Statistical Learning* (2nd ed.). Springer.  
   Reference used for multicollinearity and VIF.
