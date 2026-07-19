# Life-Expectancy-Prediction
<div align="center">

# 🌍 Life Expectancy Prediction
### A Regression-Based Analysis of Global Health, Economic & Social Indicators

*Predicting life expectancy across 193 countries (2000–2015) using WHO Global Health Observatory data*

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat&logo=scikitlearn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat&logo=pandas&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Complete-success)

[📓 View Notebook](Life_expectancy.ipynb) · [📊 Results](#-model-building--results) · [💡 Insights](#-key-insights)

</div>

---

## 📌 Overview

Life expectancy is one of the clearest single indicators of a nation's healthcare quality, economic stability, and social development — which is exactly why the UN tracks it as a core Sustainable Development Goal metric, and why governments, insurers, and public health bodies build entire policy and pricing models around it.

This project builds an end-to-end regression pipeline that predicts a country's life expectancy from 20 health, economic, and social indicators — immunization coverage, healthcare expenditure, mortality rates, education, and income — using **18 years of real WHO Global Health Observatory data across 193 countries**. Beyond just fitting a model, the project systematically benchmarks four regression algorithms, tunes them with exhaustive cross-validated grid search, and uses regularization to interpret *which* factors actually move the needle on national health outcomes.

**In short:** given a country's health and economic profile, the best model predicts its life expectancy to within **~2 years**, explaining **95.3%** of the variance in the data.

---

## ✨ Key Highlights

| | |
|---|---|
| 🎯 **Best Model R² Score** | **0.953** (Tuned KNN Regressor) |
| 📏 **Best Model RMSE** | **± 2.02 years** |
| 🗂️ **Dataset Size** | 2,938 records · 193 countries · 16 years (2000–2015) |
| 🧹 **Data Cleaning** | 0 duplicates · 5 missing-value strategies · IQR outlier treatment |
| 🤖 **Algorithms Benchmarked** | Linear Regression, KNN, SVR, Decision Tree |
| 🛠️ **Hyperparameter Search** | GridSearchCV, 5-fold CV, **780 model fits** |
| 📊 **Visualizations Produced** | 86 charts across univariate, bivariate & diagnostic analysis |
| 🧮 **Feature Engineering** | Binary + target (mean) encoding, standardized scaling |

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Key Highlights](#-key-highlights)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Data Preprocessing](#-data-preprocessing)
- [Feature Correlation](#-feature-correlation)
- [Model Building & Results](#-model-building--results)
- [Key Insights](#-key-insights)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation & Usage](#-installation--usage)
- [Future Enhancements](#-future-enhancements)
- [Author](#-author)
- [License](#-license)

---

## 🗂 Dataset

**Source:** [Life Expectancy (WHO)](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who) — compiled from the WHO Global Health Observatory (GHO) and United Nations data repositories.

| Property | Value |
|---|---|
| Records | 2,938 |
| Raw columns | 22 (21 predictors + 1 target) |
| Countries | 193 |
| Time span | 2000 – 2015 (16 years) |
| Target variable | `Life expectancy` (years) |
| File | `Life_Expectancy_Data.csv` |

<details>
<summary><b>Click to expand the full feature dictionary</b></summary>

| Feature | Description |
|---|---|
| Country | Country name |
| Year | Year of record |
| Status | Developed / Developing |
| Adult Mortality | Probability of dying between 15–60 years, per 1,000 population |
| infant deaths | Infant deaths per 1,000 population |
| Alcohol | Recorded per-capita alcohol consumption (litres, ages 15+) |
| percentage expenditure | Health expenditure as % of GDP per capita |
| Hepatitis B | HepB3 immunization coverage among 1-year-olds (%) |
| Measles | Reported measles cases per 1,000 population |
| BMI | Average Body Mass Index of the population |
| under-five deaths | Deaths of children under 5, per 1,000 population |
| Polio | Pol3 immunization coverage among 1-year-olds (%) |
| Total expenditure | Government health spend as % of total government expenditure |
| Diphtheria | DTP3 immunization coverage among 1-year-olds (%) |
| HIV/AIDS | Deaths per 1,000 live births due to HIV/AIDS (ages 0–4) |
| GDP | Gross Domestic Product per capita (USD) |
| Population | Total population |
| thinness 1–19 years | Prevalence of thinness among children/adolescents (%) |
| thinness 5–9 years | Prevalence of thinness among children aged 5–9 (%) |
| Income composition of resources | Human Development Index in terms of income composition (0–1) |
| Schooling | Average number of years of schooling |

</details>

---

## 🔄 Project Workflow

```mermaid
flowchart LR
    A["Raw WHO Data<br/>2,938 × 22"] --> B["Data Cleaning<br/>rename & dedupe"]
    B --> C["EDA<br/>Univariate + Bivariate"]
    C --> D["Missing Value<br/>Imputation"]
    D --> E["Outlier Treatment<br/>IQR Method"]
    E --> F["Encoding<br/>Binary + Target"]
    F --> G["Correlation<br/>Analysis"]
    G --> H["Train/Test Split<br/>80 / 20"]
    H --> I["Feature Scaling<br/>StandardScaler"]
    I --> J["Model Building<br/>LR · KNN · SVR · DT"]
    J --> K["Regularization<br/>Lasso"]
    K --> L["Hyperparameter Tuning<br/>GridSearchCV, 5-fold"]
    L --> M["Best Model<br/>Tuned KNN — R² 0.953"]
```

---

## 📊 Exploratory Data Analysis

The notebook runs a full univariate and bivariate pass across every numeric feature — **86 charts in total** — before any modeling begins.

<p align="center">
 
  <br/>
  <em>Distribution of the target variable — life expectancy is left-skewed, with most countries clustered between 60–80 years.</em>
</p>

<p align="center">
 
  <br/>
  <em>Developed nations average <b>79.2 years</b> vs. <b>67.1 years</b> for developing nations — a ~12-year gap.</em>
</p>

<p align="center">
  <img src="https://res.cloudinary.com/dm6bzrs6l/image/upload/v1784476845/PHOTO-2026-07-19-21-30-34_dfth6r.jpg" width="800" alt="Life expectancy vs all features"/>
  <br/>
  <em>Life expectancy plotted against all 18 numeric predictors to visually screen for linear and non-linear relationships.</em>
</p>

---

## 🧹 Data Preprocessing

**Missing values** were present in 12 of the 22 columns (up to 22.2% missing for `Population`). Each was handled with a strategy matched to its distribution and missingness pattern:

| Columns | Missing % | Strategy |
|---|---|---|
| Life expectancy, Adult Mortality | 0.34% | Rows dropped (target integrity) |
| Alcohol, BMI, Total expenditure, thinness (both) | 1.2% – 7.7% | Mean imputation |
| Hepatitis B, Polio, Diphtheria | 0.6% – 18.8% | Mode imputation |
| GDP, Population | 15.2% – 22.2% | Linear interpolation |
| Income composition of resources, Schooling | ~5.6% | Country-wise median, with Status-wise median fallback |

**Outlier treatment:** the IQR method (`Q1 − 1.5×IQR`, `Q3 + 1.5×IQR`) was applied across 18 numeric columns, with out-of-range values replaced — before-and-after boxplots confirmed every distribution was brought back within a reasonable range.

**Encoding:**
- `Status` → binary encoded (Developed = 1, Developing = 0)
- `Country` → target (mean) encoded using each country's historical average life expectancy, turning a 193-level categorical variable into a single, highly informative numeric feature

**Final modeling dataset:** 2,928 rows × 20 predictor features (`Year` dropped, `Country` target-encoded) — zero missing values, zero duplicates.

---

## 🔗 Feature Correlation

<p align="center">
  <img src="https://res.cloudinary.com/dm6bzrs6l/image/upload/v1784476717/PHOTO-2026-07-19-21-28-29_ycnjwg.jpg" width="850" alt="Correlation heatmap"/>
  <br/>
  <em>Full correlation matrix across all engineered features, computed after cleaning and encoding.</em>
</p>

Independently verifying against the raw data confirms the strongest relationships with life expectancy:

| Feature | Correlation with Life Expectancy |
|---|:---:|
| Schooling | +0.75 |
| Income composition of resources | +0.72 |
| Adult Mortality | −0.70 |
| HIV/AIDS | −0.56 |
| thinness 1–19 / 5–9 years | −0.48 |
| Diphtheria immunization | +0.48 |

---

## 🤖 Model Building & Results

Four regression algorithms were trained on an 80/20 train-test split with `StandardScaler`-normalized features (`random_state = 42`):

### Baseline performance

| Model | R² Score | RMSE (years) |
|---|:---:|:---:|
| Linear Regression | 0.932 | 2.43 |
| K-Nearest Neighbors (k=5) | 0.919 | 2.65 |
| Support Vector Regressor (RBF) | 0.920 | 2.62 |
| Decision Tree Regressor | 0.938 | 2.32 |

A **Lasso regression** (α = 0.01) was then used to inspect feature-level coefficients for sparsity and interpretability — `Income composition of resources` (+0.83), `Diphtheria` (+0.53), and `HIV/AIDS` (−0.50) emerged as the strongest independent drivers alongside the engineered `Country` feature.

### Hyperparameter tuning — `GridSearchCV`, 5-fold cross-validation

| Model | Search Space | Best Parameters | R² Score | RMSE (years) |
|---|---|---|:---:|:---:|
| Decision Tree | 108 candidates → 540 fits | `max_depth=10`, `min_samples_leaf=4`, `min_samples_split=2` | 0.924 | 2.56 |
| KNN | 24 candidates → 120 fits | `n_neighbors=5`, `weights='distance'`, `metric='manhattan'` | **0.953** | **2.02** |
| SVR | 24 candidates → 120 fits | `C=10`, `epsilon=0.2`, `kernel='rbf'` | 0.951 | 2.07 |

<p align="center">
  <img src="https://res.cloudinary.com/dm6bzrs6l/image/upload/v1784476626/PHOTO-2026-07-19-21-26-29_swjgu4.jpg" width="650" alt="Model comparison"/>
  <br/>
  <em>Final head-to-head comparison across all four algorithms.</em>
</p>

> 🏆 **Best Model: Tuned K-Nearest Neighbors Regressor — R² = 0.953, RMSE ≈ 2.02 years**

---

## 💡 Key Insights

- **Education and income outweigh healthcare spending.** `Schooling` (r = 0.75) and `Income composition of resources` (r = 0.72) correlate more strongly with life expectancy than any direct health-expenditure variable — socioeconomic opportunity is a bigger lever than clinical spend alone.
- **Adult mortality is the single strongest negative signal** (r = −0.70), consistent with it being a direct WHO-defined mortality indicator rather than an indirect proxy.
- **HIV/AIDS mortality matters even after controlling for other factors** — it retained a strong negative Lasso coefficient (−0.50) alongside its raw correlation (−0.56).
- **Development status alone explains a ~12-year gap:** Developed nations average 79.2 years vs. 67.1 years for Developing nations.
- **The dataset spans real-world extremes** — the lowest recorded life expectancy is Haiti in 2010 (36.3 years, the year of the Haiti earthquake), and the highest is Belgium in 2014 (89.0 years).
- **Country identity is a very strong signal** — the target-encoded `Country` feature had the largest Lasso coefficient (+7.90) by a wide margin, which motivated a dedicated feature-selection experiment re-training models without it, to test how much predictive power comes from geography/history versus the underlying health and economic indicators themselves.

---

## 🛠 Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3 |
| Data Handling | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | scikit-learn — Linear Regression, KNN, SVR, Decision Tree, Lasso |
| Model Selection | `train_test_split`, `GridSearchCV`, `StandardScaler`, `SimpleImputer` |
| Environment | Jupyter Notebook |

---

## 📁 Project Structure

```
life-expectancy-prediction/
│
├── README.md
├── requirements.txt
├── LICENSE
├── Life_expectancy.ipynb
│
├── data/
│   └── Life_Expectancy_Data.csv
│
└── assets/
    └── images/
        ├── 01_life_expectancy_distribution.png
        ├── 02_status_comparison.png
        ├── 03_bivariate_feature_analysis.png
        ├── 04_correlation_heatmap.png
        ├── 05_knn_bias_variance_tradeoff.png
        └── 06_model_performance_comparison.png
```

---

## ⚙️ Installation & Usage

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/life-expectancy-prediction.git
cd life-expectancy-prediction

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the notebook
jupyter notebook Life_expectancy.ipynb
```

Run all cells top-to-bottom — the notebook reads `data/Life_Expectancy_Data.csv` and reproduces every chart and metric in this README.

---

## 🚀 Future Enhancements

- [ ] **Leakage-safe target encoding** — compute the `Country` mean-encoding within cross-validation folds only, to guarantee no test-set information leaks into training
- [ ] **Ensemble models** — Random Forest, Gradient Boosting, and XGBoost for potentially stronger accuracy and built-in feature importance
- [ ] **Explainability** — SHAP or permutation importance for a deeper, model-agnostic view beyond Lasso coefficients
- [ ] **Production pipeline** — wrap preprocessing and modeling into a single `sklearn.pipeline.Pipeline` for clean, leakage-free inference (already scoped as the next step in the notebook)
- [ ] **Deployment** — serve the tuned model through a Streamlit or FastAPI app for live, interactive predictions
- [ ] **Time-aware validation** — since the data is a 2000–2015 country-year panel, validate by holding out the most recent years rather than a random split

---

## 👨‍💻 Author

**Vydhyam Vishnusai**
B.Tech CSE (AI & ML) · Mohan Babu University, Tirupati

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/vishnusai-vydhyam/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/vishnusai2005)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:vishnusaivydhyam@gmail.com)



---

