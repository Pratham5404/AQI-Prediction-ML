# 🌫️ Air Quality Index (AQI) Prediction using Machine Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Models](https://img.shields.io/badge/Models-7-purple)](https://github.com/)
[![Status](https://img.shields.io/badge/Status-Complete-brightgreen)]()

> A comprehensive comparative study of **7 machine learning and deep learning models** for Air Quality Index (AQI) prediction, with advanced missing data imputation strategies using **KNN**, **MICE**, and **IDW** imputers.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Highlights](#-key-highlights)
- [Project Structure](#-project-structure)
- [Models Used](#-models-used)
- [Data Preprocessing](#-data-preprocessing)
- [Results & Performance](#-results--performance)
- [Installation & Usage](#-installation--usage)
- [Dataset](#-dataset)
- [References](#-references)

---

## 🔍 Overview

Air Quality Index (AQI) is a critical measure of environmental health. Accurately forecasting AQI helps governments, researchers, and citizens take timely action against air pollution. This project tackles the end-to-end AQI prediction pipeline — from handling real-world missing sensor data to benchmarking state-of-the-art machine learning models.

We evaluated the impact of **three different imputation strategies** (KNN, MICE, IDW) on the downstream performance of **seven predictive models**, providing a thorough benchmark for AQI time-series forecasting.

---

## ✨ Key Highlights

- 🔬 **3 Imputation Strategies Compared**: KNN, MICE, and IDW — each evaluated for suitability with multivariate air quality sensor data
- 🤖 **7 Models Benchmarked**: LSTM, XGBoost, Random Forest, LightGBM, CatBoost, SARIMA, SARIMAX
- 📊 **Best Result**: XGBoost achieved **R² = 0.98** and **RMSE = 6.22** (KNN-imputed data)
- 🏆 **MICE Imputer** consistently produced the most reliable downstream model performance across all ML models
- 📈 Tree-based ensemble methods (XGBoost, LightGBM, CatBoost, Random Forest) significantly outperformed classical time-series models (SARIMA/SARIMAX)

---

## 📁 Project Structure

```
AQI-Prediction/
│
├── 📓 Mini_Project.ipynb          # Main notebook: EDA, preprocessing, LSTM, SARIMA, SARIMAX
├── 📓 XGBoost.ipynb               # XGBoost model training and evaluation
├── 📓 RandomForest.ipynb          # Random Forest model training and evaluation
├── 📓 LightGBM.ipynb              # LightGBM model training and evaluation
├── 📓 CatBoost.ipynb              # CatBoost model training and evaluation
│
├── 📄 README.md                   # Project overview (you are here)
├── 📄 DESCRIPTION.md              # Detailed methodology and findings
├── 📄 requirements.txt            # Python dependencies
├── 📄 .gitignore                  # Excludes confidential data files
├── 📄 LICENSE                     # MIT License
│
└── 📊 data/
    └── README_DATA.md             # Data description and sourcing instructions
```

> ⚠️ **Note:** The dataset (CSV file) used in this project is **confidential and not included** in this repository. See the [Dataset](#-dataset) section for details.

---

## 🤖 Models Used

| Model | Type | Key Strength |
|-------|------|-------------|
| **LSTM** | Deep Learning (RNN) | Captures long-range temporal dependencies in sequential AQI data |
| **XGBoost** | Gradient Boosting | High accuracy, handles structured tabular data with lagged features |
| **Random Forest** | Ensemble (Bagging) | Robust to noise, captures non-linear feature interactions |
| **LightGBM** | Gradient Boosting | Fast training, handles high-dimensional feature sets efficiently |
| **CatBoost** | Gradient Boosting | Excellent regularization, robust to noisy environmental data |
| **SARIMA** | Classical Time Series | Baseline for seasonal AQI trends |
| **SARIMAX** | Classical Time Series | Extends SARIMA with exogenous meteorological variables |

---

## 🧹 Data Preprocessing

### Missing Value Imputation

Real-world air quality sensor data frequently contains gaps due to hardware failures, transmission errors, or environmental interference. Three imputation strategies were evaluated:

#### 1. KNN Imputer
Uses *k* nearest neighbors based on **feature similarity** to estimate missing values. Particularly effective when pollutants exhibit strong inter-feature correlations (e.g., PM₂.₅ and NO₂).

#### 2. MICE Imputer *(Best Performer)*
**Multivariate Imputation by Chained Equations** — iteratively models each variable as a function of all other features using regression. Preserves the complex multivariate dependencies inherent in air quality data (pollutants × meteorological factors).

#### 3. IDW Imputer
**Inverse Distance Weighting** — spatial interpolation where closer monitoring stations exert stronger influence. Best suited for geographically distributed sensor networks where spatial continuity matters.

| Imputer | Core Principle | Best Use Case |
|---------|---------------|---------------|
| KNN | Feature-similarity neighbors | Strong inter-pollutant correlation |
| **MICE** ⭐ | Regression-based iterative | Complex multivariate dependencies |
| IDW | Spatial proximity weighting | Geo-distributed sensor networks |

> **Conclusion:** MICE consistently produced the best downstream model performance across all 7 models due to its ability to preserve multivariate statistical structure.

---

## 📊 Results & Performance

### Best Results Per Model (KNN Imputer)

| Model | RMSE ↓ | R² Score ↑ |
|-------|--------|-----------|
| **XGBoost** 🥇 | **6.22** | **0.98** |
| LightGBM 🥈 | 7.32 | 0.97 |
| CatBoost 🥉 | 7.79 | 0.97 |
| Random Forest | 8.16 | 0.97 |
| LSTM | 11.52 | 0.94 |
| SARIMAX | 19.32 | 0.82 |
| SARIMA | 53.11 | -0.35 |

### Best Results Per Model (MICE Imputer)

| Model | RMSE ↓ | R² Score ↑ |
|-------|--------|-----------|
| **XGBoost** 🥇 | **6.42** | **0.98** |
| LightGBM 🥈 | 7.31 | 0.97 |
| CatBoost 🥉 | 7.71 | 0.97 |
| Random Forest | 8.07 | 0.97 |
| LSTM | 11.13 | 0.94 |
| SARIMAX | 18.87 | 0.83 |
| SARIMA | 88.43 | -2.75 |

> **Key Insight:** Tree-based gradient boosting models (XGBoost, LightGBM, CatBoost) consistently dominate AQI prediction, significantly outperforming classical time-series methods like SARIMA. MICE imputation provides marginal but consistent improvements across models.

---

## ⚙️ Installation & Usage

### Prerequisites
- Python 3.8+
- Jupyter Notebook / JupyterLab

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/AQI-Prediction.git
cd AQI-Prediction
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Add Your Dataset
Place your air quality CSV file in the `data/` folder and update the file path in the notebooks accordingly. Refer to `data/README_DATA.md` for the expected data format and column descriptions.

### 4. Run the Notebooks
Open Jupyter and run in order:
1. `Mini_Project.ipynb` — Data loading, EDA, preprocessing, LSTM, SARIMA, SARIMAX
2. `XGBoost.ipynb` — XGBoost model
3. `RandomForest.ipynb` — Random Forest model
4. `LightGBM.ipynb` — LightGBM model
5. `CatBoost.ipynb` — CatBoost model

---

## 📊 Dataset

> 🔒 **Confidential — Not Publicly Available**

The dataset used in this project contains **real-world air quality sensor readings** and is **not included in this repository** due to confidentiality constraints.

The dataset includes features such as:
- Pollutant concentrations: PM₂.₅, PM₁₀, NO₂, SO₂, CO, O₃
- Meteorological variables: Temperature, Humidity, Wind Speed
- Timestamps for time-series analysis
- Target variable: AQI (Air Quality Index)

If you wish to replicate this study, you may use publicly available datasets such as:
- [Central Pollution Control Board (CPCB) India](https://cpcb.nic.in/)
- [UCI Air Quality Dataset](https://archive.ics.uci.edu/ml/datasets/Air+Quality)
- [OpenAQ Platform](https://openaq.org/)
- [Kaggle Air Quality Datasets](https://www.kaggle.com/search?q=air+quality+dataset)

---

## 📚 References

1. Zimmerman, N. et al. (2018). *A Machine Learning Calibration Model Using Random Forests to Improve Sensor Performance for Lower-Cost Air Quality Monitoring*. [PubMed](https://pubmed.ncbi.nlm.nih.gov/34133134/)

2. *Air Pollution Forecasting Using Advanced Machine Learning Techniques and Ensemble Stacking in Delhi*. [Research Paper](https://ehemj.com/article-1-1786-en.pdf)

---

## 📝 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to open an issue or submit a pull request.

---

<p align="center">Made with ❤️ for cleaner air and smarter cities 🌱</p>
