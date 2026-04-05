# Predictive Modeling of Chronic Kidney Disease and Analysis of Key Risk Factors

This project analyzes a **Chronic Kidney Disease (CKD)** dataset from the **UCI Machine Learning Repository** to identify important clinical risk factors and build a robust prediction model for CKD diagnosis. The study combines **exploratory data analysis, hypothesis testing, missing-data analysis, and logistic regression modeling** to evaluate both statistical relationships and predictive performance. 

## Project Overview

The project is built around two main goals:

1. **Hypothesis 1 (H1):** Test whether mean blood pressure differs between patients with **good appetite** and **poor appetite**.
2. **Hypothesis 2 (H2):** Build a **multivariable logistic regression model** to predict CKD status and identify the most important clinical predictors. 

A key contribution of this project is its focus on **missing-data robustness**. We evaluate how both inference and prediction behave under simulated **Missing Completely at Random (MCAR)** and **Missing Not at Random (MNAR)** 

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
- **Data characteristics:** mixed numerical and categorical features, uneven missingness, moderate class imbalance 

Examples of variables used in the analysis include:

- **Numerical:** age, blood pressure (`bp`), blood glucose random (`bgr`), blood urea (`bu`), serum creatinine (`sc`), hemoglobin (`hemo`), specific gravity (`sg`)
- **Categorical:** appetite (`appet`), hypertension (`htn`), diabetes mellitus (`dm`), anemia (`ane`)

---

## Workflow

## 1. Data Preprocessing
- Load and inspect the CKD dataset
- Standardize missing-value symbols such as `"?"` into `NA`
- Summarize missingness across all variables
- Separate numerical and categorical variables for downstream analysis 
<img width="543" height="406" alt="MissingType" src="https://github.com/user-attachments/assets/33d06ec0-50c2-49b8-9a07-c4657224aa7c" />

## 2. Exploratory Data Analysis
- Examine target distribution
  
  <img width="500" height="400" alt="HISTtarget" src="https://github.com/user-attachments/assets/64ae1af0-4ab8-423e-a605-2b5c76c3380f" />

- Compute summary statistics
- Visualize missing-value counts
- 
  <img width="500" height="500" alt="HISTmissing" src="https://github.com/user-attachments/assets/595a91d8-e794-43e7-ae43-61ef4088387f" />

- Build a correlation heatmap for numeric variables
  
  <img width="490" height="481" alt="Correlation" src="https://github.com/user-attachments/assets/c6e5e5a0-5ef6-4dff-b39b-c09bc4728f4b" />
  
- Identify high-correlation pairs and potential multicollinearity issues

## 3. Hypothesis Testing (H1)
- Research question: **Does blood pressure differ by appetite group?**
- Use:
  - **F-test** for equality of variances
  - **Welch’s t-test** for mean comparison when variances are unequal
- For H1, missingness is low, so **listwise deletion** is used instead of imputation
  

## 4. Logistic Regression Modeling (H2)
- Select clinically relevant predictors
- Apply **dummy encoding** to categorical variables
- Use **KNN imputation** (`k = 5`) for missing predictor values
- Check multicollinearity with **Variance Inflation Factor (VIF)**
- 
  <img width="237" height="261" alt="VIF" src="https://github.com/user-attachments/assets/1d41023b-986e-4bba-bd1a-07e4ba8cbaa5" />

- Perform **backward stepwise AIC selection**
- Diagnose quasi-complete separation
- 
  <img width="500" height="300" alt="Albumin" src="https://github.com/user-attachments/assets/06289220-59a9-4175-95af-143358a24556" />

- Remove **albumin (`al`)** due to instability
- Fit the final logistic regression model using:
  - **bgr**
  - **hemo**
  - **sg** 

## 5. Model Evaluation
- Train/test split
- Confusion matrix
- Accuracy
- Sensitivity
- Specificity
- ROC curve
- AUC
<img width="300" height="300" alt="ROC" src="https://github.com/user-attachments/assets/eac08cdb-1f66-400c-a95d-2f5179af7566" />

## 6. Missing-Data Robustness Analysis
- Simulate **MCAR** at multiple missingness levels
- Simulate **MNAR** scenarios based on clinically motivated assumptions
- Re-run H1 and H2 after missing-data injection and KNN imputation
- Compare performance and statistical conclusions across scenarios

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
- **MCAR/MNAR simulation**

---

## Key Results

### H1: Appetite vs Blood Pressure
- The F-test showed unequal variances between appetite groups
- Welch’s t-test found a **significant difference in mean blood pressure** between patients with good and poor appetite 
<img width="648" height="90" alt="H1" src="https://github.com/user-attachments/assets/23e312cd-8b4d-496e-b105-c549408eb324" />

### H2: CKD Prediction Model
- The final logistic regression model retained **three predictors**:
  - `bgr`
  - `hemo`
  - `sg`
- The final model achieved approximately:
  - **96.3% accuracy**
  - **AUC ≈ 0.993**
- This indicates strong discrimination between CKD and non-CKD patients 
<img width="672" height="392" alt="LogSummary" src="https://github.com/user-attachments/assets/03b57b4b-050e-4478-886b-2405cb3fc6b5" />

### Missing-Data Robustness
- H1 became less stable as missingness increased
- H2 remained highly robust under both **MCAR** and **MNAR** simulations
- The final multivariable model preserved strong predictive performance even under substantial missingness 
<img width="732" height="200" alt="h1MCARMNAR" src="https://github.com/user-attachments/assets/cf2789b7-1792-43c1-8e2e-9e8d448c8840" />
<img width="732" height="201" alt="h2MCARMNAR" src="https://github.com/user-attachments/assets/38c4df4f-ce6b-49c9-bf21-4821ed800c6f" />

---
## References

1. Bobbitt, Zach. “Understanding the Null Hypothesis for Logistic Regression.” *Statology*, 29 September 2021. Available at: `https://www.statology.org/null-hypothesis-of-logistic-regression/`. Accessed 24 November 2025.

2. “CHAPTER 25 Missing-data imputation.” *Columbia University*. Available at: `https://sites.stat.columbia.edu/gelman/arm/missing.pdf`. Accessed 24 November 2025.

3. “Chronic Kidney Disease.” *UCI Machine Learning Repository*. Available at: `https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease`. Accessed 24 November 2025.

4. “Stepwise Regression in Python.” *GeeksforGeeks*, 23 July 2025. Available at: `https://www.geeksforgeeks.org/machine-learning/stepwise-regression-in-python/`. Accessed 24 November 2025.

5. Tamhane, Ajit C., and Dorothy D. Dunlop. *Statistics and Data Analysis: From Elementary to Intermediate*. Prentice Hall, 2000. Accessed 24 November 2025.

6. James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). *An Introduction to Statistical Learning* (2nd ed.). Springer.  
   Reference used for multicollinearity and VIF.
