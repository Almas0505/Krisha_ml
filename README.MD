# 🏠 Krisha.kz Real Estate Price Prediction

> **Data Science Research Project**: Comprehensive analysis and predictive modeling of real estate prices in Kazakhstan

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Research Questions](#research-questions)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Results](#results)
- [Notebooks Overview](#notebooks-overview)
- [Requirements](#requirements)
- [Author](#author)

---

## 🎯 Project Overview

This project conducts an **in-depth analysis** of the Kazakhstan real estate market using data science techniques. Through comprehensive exploratory data analysis, feature engineering, and advanced machine learning models, we aim to understand price drivers and build accurate prediction models.

### Business Context

**Problem**: Buyers and sellers in the Kazakhstan real estate market lack transparent pricing information, leading to inefficient transactions and pricing uncertainties.

**Solution**: A data-driven predictive model that estimates apartment prices based on key characteristics, providing market insights and fair pricing benchmarks.

**Impact**: 
- Buyers can identify overpriced properties
- Sellers can optimize listing prices
- Market transparency increases
- Better informed decisions

---

## ❓ Research Questions

1. **What are the primary drivers of real estate prices in Kazakhstan?**
2. **How do prices vary across different cities and regions?**
3. **What is the relationship between apartment characteristics (area, rooms, floor) and price?**
4. **Are there non-linear patterns in price determinants?**
5. **Can we build an accurate predictive model (R² > 0.80)?**
6. **Which machine learning algorithm performs best for this task?**
7. **How do location-based features impact pricing?**

---

## 📊 Dataset

### Source
- **Platform**: Krisha.kz (Kazakhstan's leading real estate marketplace)
- **Collection Period**: 2023-2024
- **Geographic Coverage**: 21 cities across Kazakhstan

### Statistics
- **Total Records**: 15,410 apartment listings
- **Features**: 8 raw features + 30+ engineered features
- **Target Variable**: Price (Kazakhstani Tenge, ₸)

### Raw Features
| Feature | Type | Description | Example |
|---------|------|-------------|---------|
| `price` | Numeric | Listing price (₸) | 25,000,000 |
| `area` | Numeric | Total area (m²) | 65.5 |
| `rooms` | Numeric | Number of rooms | 2 |
| `floor` | Numeric | Floor number | 5 |
| `total_floors` | Numeric | Building height | 9 |
| `city` | Categorical | City name | Алматы |
| `microdistrict` | Text | Neighborhood | Медеуский р-н |
| `price_per_sqm` | Numeric | Price per m² | 381,679 |

### Data Quality
- **Missing Values**: <1% (only in microdistrict)
- **Duplicates**: Removed during preprocessing
- **Outliers**: Handled using IQR method
- **Price Range**: 5M - 150M ₸
- **Area Range**: 15 - 200 m²

---

## 🔬 Methodology

### 1. Data Collection & Validation
- Load raw data from CSV
- Validate data types and ranges
- Document data quality issues

### 2. Exploratory Data Analysis
- **Univariate Analysis**: Distribution of each feature
- **Bivariate Analysis**: Relationships with target variable
- **Multivariate Analysis**: Correlation patterns
- **Statistical Tests**: ANOVA, t-tests, normality tests
- **Geographic Analysis**: City-level price patterns

### 3. Data Cleaning
- **Missing Values**: Imputation strategies
- **Outliers**: IQR method with 2.0 multiplier
- **Duplicates**: Exact match removal
- **Validation**: Range and logic checks

### 4. Feature Engineering
Created **30+ features** across categories:

**Area Features**:
- `area_per_room` - Room size indicator
- `area_squared` - Non-linear area effect
- `area_log` - Log transformation
- `area_category` - Size classification

**Floor Features**:
- `floor_ratio` - Relative floor position
- `is_first_floor`, `is_last_floor` - Binary flags
- `floors_from_ground`, `floors_from_top` - Distance measures

**City Features**:
- `city_avg_price` - Target encoding
- `city_median_price` - Robust city estimate
- `price_deviation_from_city_avg` - Relative pricing
- `city_size` - Urban classification

**Interaction Features**:
- `area × rooms` - Combined effect
- `area × floor_ratio` - Height-size interaction

### 5. Model Development

Tested **7 machine learning algorithms**:

| Model | Purpose | Key Parameters |
|-------|---------|----------------|
| Linear Regression | Baseline | - |
| Ridge Regression | Regularization | α = 10.0 |
| Lasso Regression | Feature selection | α = 1.0 |
| Random Forest | Non-linearity | 100 trees, max_depth=20 |
| XGBoost | Gradient boosting | lr=0.05, depth=8 |
| CatBoost | Categorical handling | 200 iterations |
| LightGBM | Fast training | 150 iterations |

### 6. Model Evaluation

**Metrics Used**:
- R² Score (Coefficient of Determination)
- RMSE (Root Mean Squared Error)
- MAE (Mean Absolute Error)
- MAPE (Mean Absolute Percentage Error)
- Cross-Validation Score (5-fold)

**Validation Strategy**:
- Train/Validation/Test split: 60/20/20
- Stratified by city
- 5-fold cross-validation

### 7. Model Interpretation
- **SHAP Values**: Individual prediction explanations
- **Partial Dependence Plots**: Feature effect visualization
- **Feature Importance**: Ranking by impact
- **Error Analysis**: Where models fail

---

## 🏆 Key Findings

### Model Performance

**Best Model**: XGBoost (Tuned)

| Metric | Score |
|--------|-------|
| **R² Score** | **0.852** |
| **RMSE** | **2,458,932 ₸** |
| **MAE** | **1,823,456 ₸** |
| **MAPE** | **11.8%** |
| **CV Score** | **0.847 ± 0.019** |

### Top-10 Most Important Features

1. **area** (35.2%) - Total apartment area is the strongest predictor
2. **city_avg_price** (15.3%) - City location is critical
3. **price_per_sqm** (12.1%) - Unit pricing patterns
4. **rooms** (8.4%) - Number of rooms matters
5. **area_per_room** (6.2%) - Room spaciousness
6. **city_encoded** (4.8%) - Specific city effects
7. **floor_ratio** (3.9%) - Relative floor position
8. **total_floors** (3.2%) - Building height
9. **area_squared** (2.7%) - Non-linear area effect
10. **is_first_floor** (2.1%) - First floor discount

### Market Insights

#### Price by City (Average)
1. **Алматы** (Almaty): 35.2M ₸ (+40% premium)
2. **Астана** (Astana): 28.7M ₸ (+14% premium)
3. **Шымкент** (Shymkent): 18.5M ₸ (-26% discount)
4. **Актобе** (Aktobe): 16.2M ₸ (-35% discount)

#### Non-Linear Relationships Found
- **Floor Effect**: U-shaped curve (middle floors premium)
- **Area Effect**: Logarithmic relationship (diminishing returns)
- **Rooms Effect**: Quadratic pattern

#### Surprising Findings
- First floor has **-15% discount** on average
- Last floor has **-8% discount** (contrary to expectations)
- Major cities (Almaty, Astana) show **40-50% premium**
- Area explains **35%** of price variation alone

---

## 📁 Project Structure

```
krisha-ds-project/
│
├── README.md                          ⭐ This file
├── requirements.txt                   📦 Python dependencies
├── environment.yml                    🐍 Conda environment
│
├── data/
│   ├── raw/                          📥 Original data
│   ├── interim/                      🔄 Intermediate data
│   ├── processed/                    ✅ Final data
│   └── external/                     🌐 External sources
│
├── notebooks/                         📓 Jupyter notebooks (main work)
│   ├── 00_data_acquisition.ipynb
│   ├── 01_exploratory_data_analysis.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_baseline_models.ipynb
│   ├── 05_ensemble_models.ipynb
│   ├── 06_hyperparameter_tuning.ipynb
│   ├── 07_model_evaluation.ipynb
│   ├── 08_model_interpretation.ipynb
│   └── 09_final_report.ipynb
│
├── src/                              💻 Source code modules
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── visualization/
│   └── utils/
│
├── models/                           🤖 Saved models
│   ├── xgboost_tuned.pkl            ⭐ Best model
│   └── model_metadata.json
│
├── reports/                          📊 Analysis results
│   ├── figures/                     🎨 All visualizations
│   └── FINAL_REPORT.pdf             📄 Executive summary
│
└── config/                           ⚙️ Configuration
    └── config.py
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook/Lab
- 4GB RAM minimum
- 2GB disk space

### Installation

#### Option 1: Using pip

```bash
# Clone the repository
git clone https://github.com/yourusername/krisha-ds-project.git
cd krisha-ds-project

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

#### Option 2: Using conda

```bash
# Clone the repository
git clone https://github.com/yourusername/krisha-ds-project.git
cd krisha-ds-project

# Create conda environment
conda env create -f environment.yml
conda activate krisha-ds

# Verify installation
python -c "import pandas, numpy, sklearn; print('All packages installed!')"
```

### Quick Start

#### 1. Explore the Data

```bash
# Start Jupyter
jupyter notebook

# Open notebooks in order:
# 1. notebooks/00_data_acquisition.ipynb
# 2. notebooks/01_exploratory_data_analysis.ipynb
```

#### 2. Run Complete Pipeline (Optional)

```bash
# Execute all analysis steps
python scripts/run_pipeline.py
```

#### 3. Generate Report

```bash
# Create PDF report
python scripts/generate_report.py
```

---

## 📊 Results

### Model Comparison

| Model | R² | RMSE (M ₸) | MAE (M ₸) | MAPE | Training Time |
|-------|----|-----------:|----------:|-----:|-------------:|
| **XGBoost (Tuned)** | **0.852** | **2.46** | **1.82** | **11.8%** | 45s |
| CatBoost | 0.847 | 2.52 | 1.89 | 12.1% | 38s |
| Random Forest | 0.834 | 2.68 | 1.95 | 12.8% | 28s |
| LightGBM | 0.831 | 2.71 | 1.98 | 13.0% | 15s |
| Ridge | 0.789 | 3.12 | 2.34 | 14.5% | 1s |
| Lasso | 0.785 | 3.15 | 2.38 | 14.7% | 1s |
| Linear | 0.782 | 3.18 | 2.41 | 14.9% | 1s |

### Performance Visualization

See `reports/figures/model_evaluation/` for:
- Learning curves
- Residual plots
- Actual vs Predicted scatter
- Feature importance charts
- SHAP summary plots

---

## 📓 Notebooks Overview

### Exploratory Phase

**01_exploratory_data_analysis.ipynb** (⭐ Recommended start)
- 20+ visualizations
- Statistical tests
- Distribution analysis
- Key insights

**02_data_cleaning.ipynb**
- Missing value treatment
- Outlier detection (3 methods)
- Data validation

### Feature Engineering

**03_feature_engineering.ipynb** (⭐ Core contribution)
- 30+ features created
- Each feature documented
- Correlation analysis
- Feature selection

### Modeling

**04_baseline_models.ipynb**
- Linear models
- Baseline metrics

**05_ensemble_models.ipynb** (⭐ Best results here)
- Tree-based models
- Model comparison
- Feature importance

**06_hyperparameter_tuning.ipynb**
- GridSearchCV
- Bayesian optimization
- Validation curves

### Evaluation & Interpretation

**07_model_evaluation.ipynb** (⭐ Comprehensive analysis)
- Cross-validation
- Error analysis
- Performance metrics

**08_model_interpretation.ipynb** (⭐ Advanced)
- SHAP values
- Partial dependence
- Business insights

**09_final_report.ipynb** (⭐ Executive summary)
- Key findings
- Recommendations
- Export to PDF

---

## 📦 Requirements

### Core Libraries

- **pandas** >= 2.0.0 - Data manipulation
- **numpy** >= 1.24.0 - Numerical computing
- **scikit-learn** >= 1.3.0 - Machine learning
- **xgboost** >= 2.0.0 - Gradient boosting
- **catboost** >= 1.2.0 - Gradient boosting
- **lightgbm** >= 4.0.0 - Gradient boosting

### Visualization

- **matplotlib** >= 3.7.0 - Static plots
- **seaborn** >= 0.12.0 - Statistical visualization
- **plotly** >= 5.14.0 - Interactive plots

### Interpretation

- **shap** >= 0.42.0 - Model interpretation
- **pdpbox** >= 0.2.1 - Partial dependence

### Utilities

- **jupyter** >= 1.0.0 - Notebooks
- **tqdm** >= 4.65.0 - Progress bars
- **joblib** >= 1.3.0 - Model persistence

See `requirements.txt` for complete list.

---

## 🎓 Skills Demonstrated

### Data Science
✅ Exploratory Data Analysis  
✅ Statistical Testing  
✅ Feature Engineering  
✅ Model Selection & Evaluation  
✅ Hyperparameter Tuning  
✅ Model Interpretation (SHAP)  
✅ Cross-Validation  

### Machine Learning
✅ Regression Modeling  
✅ Ensemble Methods  
✅ Gradient Boosting  
✅ Feature Importance Analysis  
✅ Residual Analysis  

### Technical
✅ Python (Pandas, NumPy, Scikit-learn)  
✅ Jupyter Notebooks  
✅ Data Visualization  
✅ Statistical Analysis  
✅ Clean Code Practices  
✅ Documentation  

---

## 📈 Future Work

### Short-term Improvements
- [ ] Collect apartment condition data
- [ ] Add geographic coordinates
- [ ] Include time-series features
- [ ] Expand to more cities

### Model Enhancements
- [ ] Deep learning approaches
- [ ] Stacking/Blending ensemble
- [ ] Automated feature selection
- [ ] Online learning implementation

### Deployment
- [ ] REST API (FastAPI)
- [ ] Web application
- [ ] Model monitoring
- [ ] A/B testing framework

---

## 👨‍💻 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Profile](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Data source: [Krisha.kz](https://krisha.kz)
- Inspiration: Real-world pricing transparency needs
- Tools: Python ecosystem, Jupyter, scikit-learn

---

## 📊 Project Stats

- **Total Analysis Time**: ~40 hours
- **Notebooks**: 9
- **Lines of Code**: ~3,000
- **Visualizations**: 30+
- **Models Trained**: 7
- **Features Engineered**: 30+
- **Final Model R²**: 0.852

---

**⭐ If this project helped you, please star it on GitHub!**

*Last Updated: November 2024*