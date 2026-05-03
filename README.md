# 📊 Customer Churn Prediction – End-to-End ML Project

## 🧠 Project Overview

This project focuses on predicting customer churn using machine learning, with a strong emphasis on **model interpretability, iterative improvement, and practical deployment readiness**.

The goal was not only to build an accurate model, but also to understand:

* **why customers churn**
* **how to improve detection**
* **how to make the model usable in a real-world application**

---

## ⚙️ Project Workflow

### 1. Exploratory Data Analysis (EDA)

* Analyzed data distribution, missing values, and feature types
* Identified key numerical features:

  * `MonthlyCharges`
  * `TotalCharges`
  * `tenure`
* Used binning (quantiles) to better understand relationships with churn

📌 Key insight:

> Customers with short tenure and higher monthly charges are more likely to churn.

---

### 2. Baseline Model – Logistic Regression

* Built initial Logistic Regression model
* Evaluated using:

  * Accuracy
  * Precision / Recall
  * ROC AUC

📊 Result:

* Accuracy ≈ 0.82
* Recall (churn) ≈ 0.58

📌 Problem:

> The model failed to detect a significant portion of churn cases.

---

### 3. Threshold Tuning

Instead of using the default threshold (0.5), different thresholds were tested:

* 0.5 → recall = 0.58
* 0.4 → recall ≈ 0.68
* 0.3 → recall ≈ 0.79 (but too many false positives)

📌 Decision:

> Threshold = **0.4** provides the best balance between recall and precision.

---

### 4. Model Simplification – L1 Regularization

Applied L1 penalty to:

* reduce feature space
* improve interpretability

📌 Result:

* many coefficients reduced to zero
* model became simpler
* performance remained stable

---

### 5. Final Model

Final configuration:

* Model: **Logistic Regression (L1)**
* Threshold: **0.4**

📊 Performance:

* Accuracy ≈ 0.80
* Recall (churn) ≈ 0.68
* AUC ≈ 0.85

📌 Key takeaway:

> Improved churn detection while maintaining model simplicity.

---

### 6. Cross-Validation

Performed 10-fold cross-validation:

* AUC range: ~0.82 – 0.87
* Mean AUC: ~0.84

📌 Insight:

> The model is stable and generalizes well to unseen data.

---

## 📈 Model Interpretation

Using Logistic Regression coefficients:

### 🔴 Factors increasing churn:

* Fiber optic internet
* Streaming services
* Electronic billing
* Month-to-month contracts

### 🟢 Factors reducing churn:

* Long-term contracts (1–2 years)
* Online security / tech support
* Longer tenure

📌 Business insight:

> Contract type and service usage are the strongest drivers of churn.

---

## 🚀 Deployment Preparation

The final model was exported using `joblib` along with:

* selected features
* classification threshold

This allows easy integration into an application (e.g. Streamlit app).

---

## 🧩 Key Lessons

* **Threshold tuning can be more impactful than changing models**
* **Model simplicity (L1) improves usability without hurting performance**
* **AUC evaluates model quality, while threshold defines business behavior**
* **Understanding the model is more valuable than just using it**

---

## 📌 Final Conclusion

This project demonstrates a complete ML workflow:

* from data exploration
* through model building and optimization
* to a deployable solution

The final model strikes a balance between:

* performance
* interpretability
* practical usability

---

## 🛠️ Tech Stack

* Python
* Pandas / NumPy
* Scikit-learn
* Matplotlib / Plotly
* Joblib

🛠️ In cluster_env.yml

dependencies:
  - python=3.11
  - pip=24.0
  - numpy=1.26.4
  - pandas
  - seaborn=0.13.2
  - matplotlib
  - plotly=5.22.0
  - ipython=8.25.0


  - pycaret==3.3.2
  - scikit-learn=1.4.2

---

## 🔥 To activate 

conda env create -f environment.yml
conda activate churn-env
jupyter notebook

## 🧪 Interactive Testing

The notebook includes a commented "playground" section that allows testing the model on custom input data.

To use it:
1. Uncomment the section at the end of the notebook
2. Modify customer features (e.g. contract type, tenure, payment method)
3. Run the cells to see how predictions change

This helps understand how different features influence churn predictions.

## 📎 Next Steps

* Build interactive app (Streamlit)
* Add feature engineering improvements

---
