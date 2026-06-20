# DemandSense AI

## Hybrid Electricity Demand Forecasting using Trend + Residual Modeling

### Project Overview

DemandSense AI is a machine learning forecasting system designed to predict hourly electricity demand using historical PJM energy consumption data.

Traditional tree-based models often struggle to extrapolate long-term trends. To address this limitation, this project implements a hybrid forecasting architecture that combines:

* Linear Regression for long-term trend extraction
* LightGBM for residual forecasting
* Lag-based temporal feature engineering
* Rolling statistical window features
* TimeSeriesSplit validation

The final model achieved an average forecasting error of only **1.46% MAPE** across five chronological validation folds.

---

## Business Problem

Accurate electricity demand forecasting is critical for:

* Grid reliability
* Energy production planning
* Resource allocation
* Cost optimization
* Demand-response management

Overestimating demand leads to wasted resources, while underestimating demand can result in supply shortages and operational risks.

---

## Dataset

**Dataset:** PJM Hourly Energy Consumption

**Records:** 32,896 hourly observations

**Period Covered:** April 1998 – January 2002

**Target Variable:** PJM_Load_MW

**Frequency:** Hourly

---

## Project Workflow

### 1. Data Understanding

* Dataset inspection
* Missing value analysis
* Descriptive statistics
* Time range validation

### 2. Exploratory Data Analysis

* Long-term demand trends
* Hourly demand patterns
* Weekly seasonality
* Monthly seasonality

### 3. Feature Engineering

#### Calendar Features

* hour
* dayofweek
* month
* year

#### Lag Features

* lag_1 to lag_24

#### Rolling Window Features

* rolling_mean_24
* rolling_std_24
* rolling_min_24
* rolling_max_24

### 4. Trend Extraction

A Linear Regression model was trained on the time index to capture long-term demand growth.

Residuals were computed as:

Residual = Actual Demand − Trend Prediction

### 5. Residual Modeling

A LightGBM Regressor was trained on:

* Calendar features
* Lag features
* Rolling window statistics

to model the remaining short-term demand behavior.

### 6. Hybrid Forecast Construction

Final Prediction:

Forecast = Trend Prediction + Residual Prediction

---

## Architecture

```text
PJM Energy Consumption Data
            │
            ▼
   Datetime Engineering
            │
            ▼
   Feature Engineering
 (Lags + Rolling Windows)
            │
            ▼
     Linear Regression
      (Trend Model)
            │
            ▼
    Residual Extraction
            │
            ▼
        LightGBM
    (Residual Model)
            │
            ▼
      Hybrid Forecast
            │
            ▼
         Evaluation
```

---

## Model Performance

### Baseline Random Forest

| Metric | Value   |
| ------ | ------- |
| MAE    | 2211.65 |
| R²     | 0.7167  |

---

### Random Forest with Lag Features

| Metric | Value   |
| ------ | ------- |
| MAE    | 1179.24 |
| R²     | 0.9159  |

---

### Final Hybrid Model

| Metric | Value     |
| ------ | --------- |
| MAE    | 471.05 MW |
| RMSE   | 605.61 MW |
| R²     | 0.991     |
| MAPE   | 1.61%     |

---

## 5-Fold TimeSeriesSplit Validation

| Fold | MAE    | RMSE   | MAPE  |
| ---- | ------ | ------ | ----- |
| 1    | 544.90 | 718.67 | 1.88% |
| 2    | 437.24 | 594.69 | 1.41% |
| 3    | 393.90 | 506.57 | 1.33% |
| 4    | 425.91 | 530.79 | 1.43% |
| 5    | 389.63 | 553.45 | 1.25% |

### Average Validation Performance

| Metric | Value     |
| ------ | --------- |
| MAE    | 438.31 MW |
| RMSE   | 580.83 MW |
| MAPE   | 1.46%     |

---

## Key Findings

* Hour of day is the strongest predictor of electricity demand.
* Recent demand history significantly improves forecasting accuracy.
* Seasonal patterns remain important even after trend removal.
* Hybrid forecasting outperformed standalone machine learning models.
* Trend-residual decomposition improved model generalization.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-Learn
* LightGBM
* Matplotlib
* Jupyter Lab
* Git
* GitHub

---

## Future Improvements

* Real-time forecasting pipeline
* Streamlit deployment
* REST API integration
* Power BI analytics dashboard
* Deep learning forecasting models (LSTM / Transformer)

---

## Author

**Kumar Sanu**
B.Tech Data Science
Rishihood University
