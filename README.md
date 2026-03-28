# Real-Time Air Quality Monitoring Agent
> AI-powered AQI prediction and health advisory system | Assignment Submission

---

## 📋 Project Overview

This project develops an AI agent that monitors air quality in real time, predicts the Air Quality Index (AQI) using a trained Random Forest model, and provides personalised health advisories based on CPCB and WHO guidelines.

---

## 📁 Repository Structure

```
air_quality_project/
│
├── 01_data_understanding_preprocessing.ipynb  ← Run FIRST
├── 02_feature_engineering.ipynb               ← Run SECOND
├── 03_unsupervised_modelling.ipynb            ← Run THIRD
├── 04_visualization_analysis.ipynb            ← Run FOURTH
├── 05_interpretation_ethics.ipynb             ← Run FIFTH
│
├── data/                                      ← Auto-created by notebooks
│   ├── air_quality_clean.csv
│   ├── air_quality_scaled.csv
│   ├── air_quality_features.csv
│   └── predictions.csv
│
├── models/                                    ← Auto-created by Notebook 03
│   ├── rf_regressor.pkl
│   ├── rf_classifier.pkl
│   ├── kmeans.pkl
│   ├── pca.pkl
│   └── scaler.pkl
│
├── plots/                                     ← Auto-created by Notebook 04
│   ├── city_aqi_bar.png
│   ├── monthly_aqi_heatmap.png
│   ├── aqi_timeseries.png
│   └── ...
│
├── Air_Quality_Presentation.pptx             ← PowerPoint slides
└── README.md                                  ← This file
```

---

## ⚡ Execution Order

**CRITICAL:** Notebooks must be run in numbered order. Each notebook depends on outputs from the previous one.

| Step | Notebook | Output |
|------|----------|--------|
| 1 | `01_data_understanding_preprocessing.ipynb` | `data/air_quality_clean.csv` |
| 2 | `02_feature_engineering.ipynb` | `data/air_quality_features.csv` |
| 3 | `03_unsupervised_modelling.ipynb` | `models/*.pkl`, `data/predictions.csv` |
| 4 | `04_visualization_analysis.ipynb` | `plots/*.png` |
| 5 | `05_interpretation_ethics.ipynb` | Advisory agent demo |

---

## 🔧 Software Environment

### Python Version
```
Python 3.10.x  (recommended: 3.10.12)
```

### Required Libraries

Install all dependencies with:
```bash
pip install -r requirements.txt
```

**requirements.txt contents:**
```
pandas==2.1.4
numpy==1.26.3
matplotlib==3.8.2
seaborn==0.13.1
scikit-learn==1.4.0
scipy==1.11.4
joblib==1.3.2
jupyter==1.0.0
notebook==7.0.6
```

### Install Jupyter
```bash
pip install jupyter
jupyter notebook
```

---

## 🗂️ Dataset

The notebooks use a synthetic dataset that mirrors the structure of the **CPCB city_day.csv** dataset available on Kaggle:

🔗 https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india

To use the **real dataset**:
1. Download `city_day.csv` from Kaggle
2. Place it in the project root directory
3. In **Notebook 01, Cell 2**, replace the synthetic data generation block with:
   ```python
   df = pd.read_csv('city_day.csv', parse_dates=['Date'])
   ```

---

## 📊 Model Details

| Model | Algorithm | Purpose | Metric |
|-------|-----------|---------|--------|
| AQI Regressor | Random Forest | Predict numeric AQI | R² ≈ 0.97 |
| AQI Classifier | Random Forest | Predict AQI category | F1 macro ≈ 0.93 |
| Clustering | KMeans (K=5) | Discover pollution groups | Inertia plot |
| Dimensionality | PCA (10 components) | Noise reduction & visualisation | 90%+ variance |

---

## 🏥 Health Advisory Categories

| AQI Range | Category | Colour | Action |
|-----------|----------|--------|--------|
| 0–50 | Good | 🟢 | Enjoy outdoors |
| 51–100 | Satisfactory | 🟡 | Generally safe |
| 101–200 | Moderate | 🟡 | Sensitive groups be cautious |
| 201–300 | Poor | 🟠 | Avoid outdoor exertion |
| 301–400 | Very Poor | 🔴 | Stay indoors, wear mask |
| 401–500 | Severe | 🟣 | Health emergency |

---

## 🔍 Quick Demo

After running all notebooks, the advisory agent can be used as follows:

```python
from dataclasses import dataclass
import joblib

# Load models
rf_regr = joblib.load('models/rf_regressor.pkl')
rf_clf  = joblib.load('models/rf_classifier.pkl')

# See Notebook 05 for full AQIAdvisoryAgent class and usage
```

---

## 👤 Author

Submitted as part of the AI/ML course assignment.
Dataset source: CPCB / Kaggle (Air Quality Data in India)

---

## 📄 Evaluation Rubric Coverage

| Rubric Item | Covered In | Marks |
|-------------|-----------|-------|
| Data Preprocessing | Notebook 01 | 5 |
| AQI Prediction Model | Notebook 03 | 10 |
| Health Advisory Logic | Notebook 05 | 5 |
| Reporting & Visualisation | Notebooks 04 + 05 + PPTX | 10 |
| **Total** | | **30** |
