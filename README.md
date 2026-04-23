# 🚀 IPO Sentinel
### IPO Listing Gain Prediction using Machine Learning & Market Signals

---

## 📌 Overview

**IPO Sentinel** is a machine learning project that predicts whether an IPO will achieve **>10% listing gains** using only **pre-listing, publicly available data** — no Grey Market Premium, no post-listing leakage.

The project transforms raw IPO subscription and market data into an **Apply / Avoid decision system** by leveraging demand signals and market sentiment — trained on Indian mainboard IPOs from **2010 to 2025**.

---

## 🎯 Objective

> Can we predict IPO listing performance before it lists?

- Identify patterns in IPO subscription and demand data
- Build predictive models using structured financial signals
- Evaluate whether pre-listing market behavior provides reliable signals of listing gains

---

## 🧠 Key Insights

- 📈 **Institutional demand (QIB, HNI)** is the strongest predictor of listing performance
- ⚖️ **Demand Gap** captures the imbalance between institutional and retail interest
- 📊 **Market sentiment (Nifty_Return_7d)** adds short-term contextual signal
- 🔍 Consistent ROC-AUC across models indicates **strong underlying signal in the features, not model complexity**

---

## 🏗️ Project Structure

```
ipo-sentinel/
│
├── config.yaml
├── requirements.txt
├── README.md
│
├── src/
│   ├── data_preprocessing.py
│   ├── train_pipeline.py
│   └── models.py
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_Preprocessing_and_Feature_Engineering.ipynb
│   └── 03_Model_1_Baseline.ipynb
│
└── models/
    └── best_model.pkl
```

---

## ⚙️ Features Used

| Feature | Description |
|---|---|
| `Issue_Size(crores)` | Total IPO size in INR crores |
| `QIB` | Qualified Institutional Buyer subscription multiple |
| `HNI` | High Net-worth Individual subscription multiple |
| `RII` | Retail Individual Investor subscription multiple |
| `Total_Subscription` | Overall subscription multiple |
| `Offer_Price` | IPO offer price |
| `Demand_Gap` | Engineered: difference between institutional and retail demand |
| `log_issue_size` | Log-transformed issue size to reduce skew |
| `Month`, `Year` | Temporal features for seasonality |
| `Nifty_Return_7d` | 7-day Nifty return before IPO close (market sentiment) |

---

## 🧪 Models Trained

| Model | Notes |
|---|---|
| Logistic Regression | Baseline |
| Random Forest | Ensemble, handles non-linearity |
| Gradient Boosting | Sequential boosting |
| XGBoost | Regularized boosting |
| LightGBM | Fast gradient boosting |
| **CatBoost** | **Best performer** |
| SVM | Margin-based classifier |

---

## 📊 Results

| Metric | Value |
|---|---|
| Best Model | CatBoost |
| ROC-AUC (best) | **~0.927** |
| ROC-AUC (range across models) | 0.90 – 0.93 |

> Consistent performance across diverse model families confirms **strong, learnable signal in the feature set** — not overfitting to a single algorithm.

---

## 📓 Notebooks (Step-by-Step Walkthrough)

Prefer exploring interactively? The full pipeline is broken into 3 notebooks inside the `notebooks/` folder — you can run them directly on Google Colab, no setup needed.

| # | Notebook | What it covers |
|---|---|---|
| 1 | [`01_EDA.ipynb`](notebooks/01_EDA.ipynb) | Exploratory Data Analysis — distributions, correlations, class balance |
| 2 | [`02_Preprocessing_and_Feature_Engineering.ipynb`](notebooks/02_Preprocessing_and_Feature_Engineering.ipynb) | Cleaning, Demand_Gap, log transforms, Nifty_Return_7d |
| 3 | [`03_Model_1_Baseline.ipynb`](notebooks/03_Model_1_Baseline.ipynb) | Training all 7 models, cross-validation, ROC-AUC comparison |

> 💡 **Recommended order:** Run notebook 2 → 1 → 3 for the full end-to-end flow.

---

## 🔧 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/DeemonDuck/ipo-sentinel.git
cd ipo-sentinel
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Add Dataset

Place your raw dataset at:

```
data/raw/raw_dataset.xlsx
```

### 4. Run Data Preprocessing

```bash
python src/data_preprocessing.py
```

### 5. Train Models

```bash
python src/train_pipeline.py
```

---

## 📦 Output

| Output | Path |
|---|---|
| Processed dataset | `data/processed/ipo_feature_engineered.csv` |
| Best trained model | `models/best_model.pkl` |

---

## 🧠 Methodology

```
1. Data Collection       →  Indian mainboard IPOs (2010–2025) + Nifty via yfinance
2. Feature Engineering   →  Demand_Gap, log_issue_size, Nifty_Return_7d
3. Data Cleaning         →  EDA-driven missing value handling, redundant feature removal
4. Label Creation        →  Binary target: Listing Gain > 10% → 1, else 0
5. Model Training        →  Stratified K-Fold cross-validation across 7 models
6. Model Comparison      →  ROC-AUC as primary metric (handles class imbalance)
7. Best Model Export     →  Saved as best_model.pkl for inference
```

---

## 🚧 Future Improvements

- [ ] Integrate Grey Market Premium (GMP) for post-2018 data
- [ ] Add company fundamentals from RHP (revenue, profitability, D/E ratio)
- [ ] Deploy as a **Streamlit web app** with live prediction
- [ ] Add SME IPO support alongside mainboard
- [ ] Real-time prediction pipeline using SEBI filing data

---

## 💡 Key Learnings

- Financial markets exhibit **predictable patterns** through subscription demand signals
- **Feature engineering matters more than model complexity** — Demand_Gap alone is highly informative
- Using only pre-listing data enforces strict **no-leakage discipline**, making results credible
- Proper target definition (>10% gain as binary label) makes the problem tractable and practically useful

---

## 👨‍💻 Author

**Ridham Taneja**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Ridham%20Taneja-blue?style=flat&logo=linkedin)](https://linkedin.com/in/ridham-taneja)
[![GitHub](https://img.shields.io/badge/GitHub-DeemonDuck-black?style=flat&logo=github)](https://github.com/DeemonDuck)

---

## ⭐ If you found this useful

Consider giving a **star** ⭐ to the repository — it helps others find the project!
