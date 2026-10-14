# Telecom Customer Churn Prediction | Machine Learning

An end-to-end **customer churn classification** project built around telecom customer data, from exploratory analysis and preprocessing to trained machine-learning models and a **Streamlit prediction dashboard**.

> **Core question:** Based on a customer's contract, services, tenure, and charges, how likely are they to stop using the telecom provider?

## Overview

Customer churn is a practical classification problem: identify subscribers likely to leave so a business can better understand retention risk. This repository contains exploratory notebooks, preprocessing and modeling work, saved model artifacts, and an interactive app for entering a customer profile.

The dashboard estimates **churn probability** and includes a **what-if** interface to compare the effect of selected customer attributes. The values should be interpreted as model estimates, not causal effects.

## Features

- Explore customer demographics, contract types, subscriptions, and charges.
- Prepare tabular data and categorical features for machine learning.
- Work through data analysis, preprocessing, and modeling notebooks.
- Load serialized model, feature-name, and scaler artifacts with `joblib`.
- Predict churn probabilities from a manually entered customer profile.
- Display risk labels for estimated churn probability.
- Compare alternative scenarios in an interactive dashboard.

## Machine Learning Workflow

```text
Telco customer dataset
        |
        v
Exploratory Data Analysis (EDA)
        |
        v
Missing values / Encoding / Scaling
        |
        v
Train / Test Data
        |
        v
Modeling and Comparison
        |
        v
Saved Model + Scaler + Feature List
        |
        v
Streamlit Customer Churn Dashboard
        |
        v
Prediction Probability + What-if Scenarios
```

## Repository Structure

```text
Telco_Churn_Prediction/
├── data/
│   ├── Telco-Customer-Churn.csv    # Raw telecom churn dataset
│   └── processed/
│       ├── X_train.csv             # Training features
│       ├── X_test.csv              # Test features
│       ├── y_train.csv             # Training labels
│       └── y_test.csv              # Test labels
├── notebook/
│   ├── EDA.ipynb                   # Exploratory data analysis
│   ├── Preprocessing.ipynb         # Data cleaning / feature preparation
│   └── Modeling.ipynb             # Model development and comparison
├── models/
│   ├── best_model.pkl              # Serialized trained classifier
│   ├── scaler.pkl                  # Saved numeric scaler
│   ├── feature_names.pkl           # Feature order expected by the model
│   └── best_model_name.pkl         # Selected model identifier
├── dashboard/
│   └── app.py                      # Interactive Streamlit interface
├── Customer Churn Prediction.pptx # Project presentation
├── requirements.txt
└── README.md
```

## How It Works

### 1. Exploratory analysis

`notebook/EDA.ipynb` examines the customer dataset and helps identify patterns associated with churn, including service usage, billing, and contracts.

### 2. Preprocessing

`notebook/Preprocessing.ipynb` prepares numerical and categorical predictors. In the dashboard, a new customer profile is transformed into the saved training feature order before inference.

### 3. Model development

`notebook/Modeling.ipynb` covers the modeling workflow. The repository includes dependencies such as scikit-learn, XGBoost, LightGBM, and imbalanced-learn; consult the notebook for the algorithms actually trained and the selection criteria.

### 4. Interactive predictions

`dashboard/app.py` loads the selected classifier and preprocessing assets, collects customer attributes, and calls `predict_proba` to estimate churn risk.

### 5. What-if scenarios

The app lets users compare the current profile with alternative values. These estimates show model sensitivity and **should not be interpreted as proof that a proposed intervention will reduce churn**.

## Technology Stack

| Area | Tools | Use |
|---|---|---|
| Language | Python | Analysis and inference |
| Data | Pandas, NumPy | Preparation and transformation |
| ML | scikit-learn | Training utilities and evaluation |
| Additional modeling | XGBoost, LightGBM, imbalanced-learn | Classifier experiments and class handling |
| Visualization | Matplotlib, Seaborn | Exploratory analysis |
| Dashboard | Streamlit | Input forms and predictions |
| Serialization | joblib | Loading trained models and preprocessing |
| Notebooks | Jupyter | EDA, preprocessing, experiments |

## Getting Started

### Prerequisites

Python and pip. The saved model artifacts are tracked in `models/`, so you can explore the dashboard without retraining first, provided your Python package versions are compatible.

### 1. Clone and create a virtual environment

```bash
git clone https://github.com/Darius-Cos/Telco_Churn_Prediction.git
cd Telco_Churn_Prediction
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
```

### 2. Install dependencies

The repository's current `requirements.txt` ends with `jupyter notebook` on a single line, which is **not a valid pip requirement**. Before installing from it, change that line to `notebook` (or separate `jupyter` and `notebook` requirements). Then run:

```bash
pip install -r requirements.txt
```

### 3. Launch the dashboard

```bash
streamlit run dashboard/app.py
```

The app loads the trained artifacts from the `models/` directory and opens in your browser.

### 4. Explore the notebooks

```bash
jupyter notebook
```

Start with `EDA.ipynb`, continue with `Preprocessing.ipynb`, and then review `Modeling.ipynb`.

## Example Inputs and Output

Example customer fields: `tenure`, `MonthlyCharges`, `Contract`, `InternetService`, `OnlineSecurity`, `TechSupport`, `PaymentMethod`, and other subscribed services.

**Output:** an estimated probability of churn expressed as a percentage, together with a risk indicator and scenario comparison. No particular accuracy score is claimed here because model metrics should be taken from a reproducible evaluation on held-out data.

## Concepts Demonstrated

- Binary classification on structured customer data.
- One-hot encoding and consistent feature ordering at inference time.
- Training/test separation and persisted preprocessing assets.
- Model selection and evaluation in notebooks.
- Serving a trained ML model through a simple UI.
- Distinguishing predictive relationships from causal claims.

## Limitations and Future Improvements

- Persist a single scikit-learn `Pipeline` that includes all preprocessing to reduce training/inference drift.
- Add reproducible evaluation metrics and a confusion matrix to this README after re-running the notebook.
- Check model calibration and false-positive/false-negative trade-offs.
- Make the dashboard text consistent in English if targeting international recruiters.
- Validate the source and licensing of the dataset and presentation before public release.

## Disclaimer

Predictions are educational estimates and must not be used as the sole basis for decisions affecting customers.

## Author

**Darius Costache** · [GitHub](https://github.com/Darius-Cos)
