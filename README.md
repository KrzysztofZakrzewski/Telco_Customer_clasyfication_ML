# 📊 Customer Churn Prediction – End-to-End ML Project

## 🧠 Project Overview

This project focuses on predicting customer churn using machine learning, with a strong emphasis on:

* model interpretability
* iterative improvement
* business-oriented evaluation
* deployment readiness

The project evolved from a simple interpretable baseline model into a comparison between linear and ensemble machine learning approaches for churn prediction.

The goal was not only to build an accurate model, but also to understand:

* why customers churn
* how different models behave
* how threshold tuning changes business outcomes
* how to prepare models for real-world deployment

---

# ⚙️ Project Workflow

## 1. Exploratory Data Analysis (EDA)

* Analyzed data distribution, missing values, and feature types
* Identified key numerical features:

  * `MonthlyCharges`
  * `TotalCharges`
  * `tenure`

* Used quantile binning to better understand churn patterns

📌 Key insight:

> Customers with short tenure and higher monthly charges were significantly more likely to churn.

---

# 2. Baseline Model – Logistic Regression

A Logistic Regression model was used as the initial baseline because of its simplicity and interpretability.

The model was evaluated using:

* Accuracy
* Precision / Recall
* ROC AUC

📊 Initial Results:

* Accuracy ≈ 0.82
* Recall (churn) ≈ 0.58

📌 Problem:

> The default model failed to detect a significant portion of churn cases.

---

# 3. Threshold Tuning

Instead of relying on the default classification threshold (0.5), multiple thresholds were tested to improve churn detection performance.

Threshold comparison:

* 0.5 → recall ≈ 0.56
* 0.4 → recall ≈ 0.68
* 0.3 → recall ≈ 0.80 (but too many false positives)

📌 Decision:

> Threshold = 0.4 provided the best balance between recall and precision.

---

# 4. Model Simplification – L1 Regularization

L1 regularization was applied to:

* reduce feature space
* simplify the model
* improve interpretability

📌 Results:

* many coefficients were reduced to zero
* model complexity decreased
* performance remained stable

---

# 5. Advanced Model – Gradient Boosting

To explore non-linear relationships and potentially improve predictive performance, a Gradient Boosting Classifier was introduced.

The following parameters were tuned:

* `learning_rate`
* `n_estimators`
* classification threshold

### Final Configuration

* learning_rate = 0.05
* n_estimators = 100
* threshold = 0.4

📊 Performance:

* ROC AUC ≈ 0.86
* Recall ≈ 0.68
* Precision ≈ 0.64

📌 Key insight:

> Gradient Boosting improved the balance between recall and precision while maintaining strong overall generalization performance.

---

# 6. Feature Importance Analysis

Gradient Boosting feature importance identified:

* tenure
* contract type
* internet service type
* payment method

as the strongest churn predictors.

📌 Additional experiment:

Features with near-zero importance were removed and tested again.

Result:

> Removing weak predictors produced almost identical results, suggesting that the Gradient Boosting model already handled low-information features effectively.

---

# 7. Cross-Validation

10-fold cross-validation was performed to validate model stability and generalization performance.

📊 Results:

* Mean ROC AUC ≈ 0.85
* Standard deviation ≈ 0.013

📌 Insight:

> The model demonstrated stable performance across different data splits and generalized consistently to unseen data.

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

* trained model
* selected features
* classification threshold

This allows easy integration into an application (e.g. Streamlit app).

---

# 🧪 Interactive Testing

The notebook includes a commented playground section that allows testing custom customer scenarios.

Users can modify:

* contract type
* tenure
* payment method
* internet services

and observe how predictions change across different models.

---

## 🧩 Key Lessons

* Threshold tuning can significantly improve business-oriented performance
* Logistic Regression provides strong interpretability and simplicity
* Gradient Boosting improves predictive flexibility and class separation
* ROC AUC measures ranking quality, while thresholds define business behavior
* Feature importance and regularization help simplify models without major performance loss

---

## 📌 Final Conclusion

* from data exploration
* through model development and tuning
* to model comparison and deployment preparation

Both Logistic Regression and Gradient Boosting were evaluated not only on raw metrics, but also on:

* interpretability
* generalization
* deployment usability
* business practicality

The final solution balances:

* predictive performance
* interpretability
* practical usability
* deployment readiness

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
