# 📋 Project Description: AQI Prediction using Machine Learning

## Project Summary

This project presents a **systematic comparative study** of machine learning and deep learning approaches for **Air Quality Index (AQI) prediction**. The core research question explored is:

> *How do different missing-data imputation strategies affect the predictive performance of machine learning models on multivariate air quality time-series data?*

To answer this, we designed a controlled experimental pipeline where the same dataset — imputed using three distinct strategies (KNN, MICE, IDW) — was fed into seven different predictive models. This design isolates the effect of imputation quality on model accuracy, providing actionable insights for environmental data science practitioners.

---

## 🎯 Problem Statement

Air Quality Index (AQI) is a standardized measure of how polluted the air is on a given day. Accurate AQI forecasting enables:
- Timely health advisories for vulnerable populations
- Governmental policy decisions for emission control
- Smart city environmental monitoring systems

The main challenges in AQI prediction include:
1. **Missing sensor data** — due to hardware failures, power outages, or transmission errors
2. **Complex non-linear relationships** — between pollutants and meteorological variables
3. **Temporal dependencies** — AQI is a time series with seasonal and daily patterns
4. **High dimensionality** — multiple pollutants (PM₂.₅, PM₁₀, NO₂, SO₂, CO, O₃) + weather variables

---

## 🔬 Methodology

### Phase 1 — Data Cleaning & Imputation

Three scientifically grounded imputation methods were applied independently to the raw dataset:

**KNN Imputer**
- Replaces missing values using the *k* most similar samples in feature space
- Similarity measured via Euclidean distance
- Exploits strong inter-pollutant correlations (e.g., NO₂ and PM₂.₅)
- Preserves local data structure and relational consistency between sensors

**MICE Imputer (Best Performer)**
- Multivariate Imputation by Chained Equations
- Iteratively regresses each incomplete variable on all other features
- Multiple rounds until convergence — statistically robust
- Particularly powerful for air quality data where pollutants and meteorological factors share complex conditional dependencies
- Produces imputations with the highest multivariate statistical fidelity

**IDW Imputer**
- Inverse Distance Weighting — a spatial interpolation technique
- Closer monitoring stations/data points get higher weight (inverse power law)
- Preserves spatial continuity in pollutant gradients
- Best suited for geographically distributed sensor networks where proximity matters

### Phase 2 — Model Development & Training

Seven models were trained on each of the three imputed datasets:

**Deep Learning**
- **LSTM (Long Short-Term Memory):** Recurrent architecture with gating mechanisms for long-range temporal dependency modeling. Input sequences with sliding window of lagged AQI + pollutant features.

**Gradient Boosting Ensemble Methods**
- **XGBoost:** Extreme Gradient Boosting — sequential tree ensemble with regularization (L1/L2). Industry gold standard for tabular regression.
- **LightGBM:** Histogram-based gradient boosting with leaf-wise growth. Faster training, highly scalable for high-dimensional features.
- **CatBoost:** Ordered boosting with symmetric trees. Excellent regularization, minimal need for hyperparameter tuning.

**Bagging Ensemble Methods**
- **Random Forest:** Parallel ensemble of decision trees with feature bagging. Robust to overfitting and noise.

**Classical Time-Series Models (Baselines)**
- **SARIMA:** Seasonal ARIMA. Captures seasonal and autoregressive patterns in univariate AQI.
- **SARIMAX:** Extends SARIMA with exogenous variables (meteorological inputs).

### Phase 3 — Evaluation

Models were evaluated using two standard regression metrics:
- **RMSE (Root Mean Squared Error):** Penalizes large prediction errors — lower is better
- **R² Score:** Proportion of variance explained — higher (closer to 1.0) is better

---

## 📊 Findings & Discussion

### Finding 1: MICE Outperforms KNN and IDW

Across all 7 models, datasets imputed with MICE produced consistently better or comparable results. This is attributed to MICE's regression-based iterative approach which preserves the multivariate conditional structure of air quality data — the very structure that ML models learn from.

### Finding 2: Gradient Boosting > Deep Learning > Classical Methods

| Tier | Models | Typical R² |
|------|--------|-----------|
| 🥇 Top | XGBoost, LightGBM, CatBoost | 0.97–0.98 |
| 🥈 Mid | Random Forest, LSTM | 0.94–0.97 |
| 🥉 Baseline | SARIMAX, SARIMA | -2.75–0.83 |

Gradient boosting models dominated, demonstrating that with proper feature engineering (lagged variables, rolling statistics), ensemble tree methods capture temporal dynamics nearly as well as LSTM — with far less complexity.

### Finding 3: SARIMA Fails on Multivariate AQI

SARIMA and even SARIMAX showed poor performance (negative R² under MICE). Classical time-series models struggle because:
- AQI is driven by many interacting variables (not just past AQI values)
- Non-linear feature interactions cannot be captured by linear models
- Real-world AQI data has complex irregular patterns beyond simple seasonality

### Finding 4: XGBoost is the Overall Best Model

XGBoost consistently ranked #1 across all imputer variants:
- **RMSE: 6.22, R²: 0.98** (KNN imputed)
- **RMSE: 6.42, R²: 0.98** (MICE imputed)

Its ability to sequentially correct prediction errors through boosting, combined with robust regularization, makes it the most reliable model for AQI forecasting in this study.

---

## 🛠️ Tech Stack

| Category | Tools / Libraries |
|----------|------------------|
| Language | Python 3.8+ |
| Data Processing | pandas, NumPy, scikit-learn |
| Imputation | scikit-learn (KNN, MICE), custom IDW |
| Visualization | Matplotlib, Seaborn |
| ML Models | XGBoost, LightGBM, CatBoost, scikit-learn |
| Deep Learning | TensorFlow / Keras (LSTM) |
| Time Series | statsmodels (SARIMA, SARIMAX) |
| Notebook | Jupyter Notebook |

---

## 🚀 Future Work

- [ ] Hyperparameter tuning using Optuna / Bayesian Optimization
- [ ] Ensemble/stacking of top-performing models (XGBoost + LightGBM + CatBoost)
- [ ] Real-time AQI prediction with a Streamlit / FastAPI web app
- [ ] Geospatial visualization of AQI predictions across monitoring stations
- [ ] Incorporation of satellite imagery and weather API data
- [ ] Explainability with SHAP values for feature importance analysis

---

## ⚠️ Data Confidentiality Notice

The dataset used in this project is **proprietary and confidential**. It has not been published in this repository. The raw CSV file(s) are excluded via `.gitignore`. If you wish to reproduce the experiments, please use a publicly available air quality dataset and adapt the data loading cells in the notebooks accordingly.

Refer to `data/README_DATA.md` for the expected schema and feature descriptions.
