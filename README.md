# Week 03 - Classical Machine Learning Model Comparison

## Overview

This project was completed as part of the **Week 03 AI Engineering practical assessment**.

The objective of the project is to build and compare multiple classical machine learning models using industrial machine sensor data.

The main task is to predict whether a machine is likely to experience a **failure on the next day** based on historical sensor readings, machine information, error records, and other operational features.

---

## Project Objectives

The main objectives of this project are to:

- Prepare industrial machine data for machine learning.
- Perform feature engineering using daily machine observations.
- Build a binary classification problem for machine failure prediction.
- Train multiple classical machine learning models.
- Compare model performance using appropriate classification metrics.
- Evaluate the effect of class imbalance.
- Use cross-validation to check model stability.
- Understand and demonstrate the risk of data leakage.
- Interpret model results from an operational/business perspective.

---

## Dataset

The project uses industrial predictive maintenance data containing information such as:

- Machine ID
- Machine model
- Machine age
- Voltage
- Rotation
- Pressure
- Vibration
- Machine errors
- Maintenance/failure information

Sensor readings were aggregated into **daily machine-level features** for modelling.

Examples of engineered features include:

- Mean voltage
- Maximum voltage
- Mean rotation
- Maximum rotation
- Mean pressure
- Maximum pressure
- Mean vibration
- Maximum vibration
- Error count

The final modelling task predicts whether a machine will experience a **failure on the following day**.

> Note: Some dataset files are large. `PdM_telemetry.csv` is approximately 75 MB.

---

## Machine Learning Models

Three classification algorithms were trained and compared:

### 1. Logistic Regression

Used as a simple and interpretable baseline classification model.

### 2. Random Forest

An ensemble tree-based model capable of identifying nonlinear relationships between machine conditions and failures.

### 3. XGBoost

A gradient-boosting model used to capture more complex patterns in the machine data.

---

## Model Evaluation

Since machine failures are relatively rare, **accuracy alone is not sufficient** for evaluating the models.

The following metrics were considered:

- **Precision** - How many predicted failures were actual failures.
- **Recall** - How many actual failures were successfully detected.
- **F1 Score** - Balance between precision and recall.
- **ROC-AUC** - Ability of the model to distinguish between failure and non-failure cases.
- **Confusion Matrix** - Analysis of true positives, true negatives, false positives, and false negatives.

---

## Model Comparison

The models showed different trade-offs.

| Model | Main Observation |
|---|---|
| Logistic Regression | Very high recall but produced more false alarms |
| Random Forest | Strong balance between detecting failures and limiting false alarms |
| XGBoost | Performance similar to Random Forest with good overall classification results |

### Confusion Matrix Results

| Model | True Negative | False Positive | False Negative | True Positive |
|---|---:|---:|---:|---:|
| Logistic Regression | 8767 | 179 | 6 | 173 |
| Random Forest | 8924 | 22 | 14 | 165 |
| XGBoost | 8922 | 24 | 16 | 163 |

Logistic Regression detected the highest number of actual failures but also generated considerably more false alarms.

Random Forest and XGBoost produced fewer false alarms while still detecting most failure cases.

Therefore, model selection should consider the operational cost of both **missed machine failures** and **unnecessary maintenance alerts**, rather than relying on a single evaluation metric.

---

## Cross-Validation

**Stratified 5-fold cross-validation** was used to evaluate model stability.

Stratification was important because the target variable is highly imbalanced, with considerably fewer failure cases than normal machine observations.

F1 score was used as one of the main cross-validation metrics.

---

## Data Leakage Demonstration

An intentional data leakage experiment was also performed.

Failure-related information was introduced into the model features to demonstrate how information connected to the outcome can affect model evaluation.

The leakage experiment produced:

**Leaky F1 Score: 0.7195**

This demonstrates the importance of ensuring that information unavailable at prediction time is not included as an input feature.

The intentionally leaky configuration is **not used as the final predictive model**.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Jupyter Notebook
- Git
- GitHub

---

## Project Structure

```text
Week03_Hasandi/
│
├── data/
│   └── Industrial machine datasets
│
├── notebooks/
│   └── Machine learning analysis notebook
│
├── .gitignore
├── README.md
└── Other project files
