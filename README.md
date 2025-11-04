

# 🏢 Alpha Company — Customer Churn Prediction (Group Alpha)

**👨‍💻 Authors:** [Alfriando C Vean](https://github.com/alfcvean), [Ardinata Jeremy Kingstone Tambun](https://github.com/ardinatatambun), [Bonifasius Sinurat](https://github.com/bonifasiusx)

📅 *Purwadhika Final Project — ***JCDS-3004***

---

## 🎯 1. Business Objective

Reduce customer churn by:

* 🔍 Identifying **high-risk customers** before they churn
* 🎯 Implementing **targeted, cost-efficient retention** interventions
* 💰 Delivering **positive financial impact** while maintaining healthy unit economics

---

## 📊 2. Data Overview

* **Source:** `E Commerce Dataset.xlsx`
* **Target:** `Churn` *(binary)*
* **Key Features:** `Tenure`, `Complain`, `DaySinceLastOrder`, `PreferredPaymentMode`, `PreferredLoginDevice`, etc.
* **Note:** Data is anonymized for analytics and modeling.

---

## ⚙️ 3. Methodology

* **Preprocessing:** Imputation (Simple/Iterative), optional scaling (RobustScaler), One-Hot Encoding
* **Modeling:** `XGBoost` with **class weighting** for imbalance handling
* **Validation:** Hyperparameter tuning — primary metric: **F2-Score**
* **Explainability:** SHAP (summary, dependence, waterfall)
* **Business Impact:** Savings/Cost/Loss/Net Impact and ROI calculations

**🧠 Pipeline Overview**

---

## 📈 4. Model Performance

| **Metric**              | **Cross-Validation** | **Test Set** |
| ----------------------------- | -------------------------: | -----------------: |
| 🧮**F2 Score**          |                     0.8894 |   **0.9759** |
| 🎯**Recall (Churn)**    |                      0.986 |    **0.989** |
| 🎯**Precision (Churn)** |                      0.963 |    **0.964** |
| 📊**AUC-PR**            |                      0.993 |    **0.993** |

**Confusion Matrix (test)** — TN=929, FP=7, FN=4, TP=186

---

## 🧩 5. Explainability (SHAP & Feature Importances)

**Top Drivers of Churn:**

1. 🕒 **Tenure** — shorter tenure increases churn risk
2. 😠 **Complain** — history of complaints correlates with 2–3× higher churn likelihood
3. 📆 **DaySinceLastOrder** — longer inactivity raises churn risk
4. 💳 **PreferredPaymentMode** — COD users churn more than e-wallet users
5. 📱 **PreferredLoginDevice** — app users are more loyal

![SHAP Summary](images/shap_summary.png)

![Feature Importance](images/feature_importance_bar.png)

![SHAP Waterfall](images/shap_waterfall.png)

---

## 💵 6. Business Impact and ROI

**Assumptions**

| Parameter                     | Value ($) | Notes                          |
| ----------------------------- | --------: | ------------------------------ |
| **CAC**                 |        80 | Cost to acquire a new customer |
| **CRC**                 |        20 | Cost to retain a customer      |
| **Net Retention Value** |        60 | CAC − CRC                     |

**Impact Summary**

| Component                     |        Value ($) | Notes                        |
| ----------------------------- | ---------------: | ---------------------------- |
| 💰**Savings (TP)**      |           11,160 | 186 × (80 − 20)            |
| 💸**Cost (FP)**         |              140 | 7 × 20                      |
| 😓**Loss (FN)**         |              320 | 4 × 80                      |
| 🧾**Net Impact**        | **10,700** | 11,160 − (140 + 320)        |
| 📈**ROI (baseline)**    | **78.7×** | (11,160 − 140) / 140        |
| 🔁**ROI (churn ↓5pp)** | **55.6×** | Simulation: churn 17% → 12% |

✅ Enables **precision retention** — focusing spend on *truly at-risk* customers while minimizing waste.

---

## 🚀 7. Deployment and Operations

**Deployment Options:**

* 🧭 **Streamlit App:** Interactive scoring dashboard
* ⚙️ **REST API:** For batch or event-based scoring

![Streamlit](images/streamlit_screenshot.png)

---

## 📊 8. Tableau Story — *The 90-Day Churn Reduction Playbook*

📍 [View on Tableau Public](https://public.tableau.com/views/alpha_churn_dashboards/The90-DayChurnReductionPlaybook?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

![Tableau](images/tableau_story.png)

---

## 🧱 9. Repository Structure

```
Final Project/
├─ Streamlit/                      # Streamlit app (UI & serving)
│  ├─ app.py
│  ├─ pages/                       # multipage Streamlit
│  ├─ utils/                       # helpers: io, metrics, plotting, loaders
│  ├─ assets/                      # css, icons, small UI images
│  ├─ artifacts/                   # churn_xgb_cw.sav
│  └─ .streamlit/                  # config.toml, secrets.toml
├─ Dataset/
│  ├─ Raw Dataset/                 # original files (read-only)
│  ├─ interim/                     # cleaned after EDA
│  └─ processed/                   # final train (csv)
├─ Tableau/
│  └─ alpha_churn_dashboards.twbx  # Tableau dashboard   
├─ alpha_churn_notebook.ipynb
├─ images/                         # PNGs for README (confmat, SHAP, etc.)
└─ README.md
```

---

## 🧪 10. Reproducibility and Run

**Environment:**

Python ≥ 3.10

Install dependencies:

```bash
pip install -r requirements.txt
```

**Core Packages:**

`xgboost`, `lightgbm`, `scikit-learn`, `imbalanced-learn`, `shap`, `pandas`, `numpy`, `matplotlib`, `streamlit`

**Run the Notebook:**

```bash
jupyter notebook alpha_churn_notebook.ipynb
```

**Run the Streamlit App:**

```bash
streamlit run Streamlit/app.py
```

> ⚠️ Make sure model and encoder paths in `app.py` are correct.

---

## 🔍 11. Monitoring and Risks

* 📊 **Data drift:** Monitor key feature distributions (`Tenure`, `DaySinceLastOrder`)
* ⚖️ **Class imbalance:** Reassess threshold if churn prevalence shifts
* 🧱 **Feature availability:** Production schema must match training
* 🧑‍⚖️ **Ethics:** Ensure fairness and avoid disparate impact

---

## 🪪 12. License and Credits

**License:** MIT License © 2025 Group Alpha

**Contributors:**

👤 **Alfriando C Vean**

👤 **Ardinata Jeremy Kingstone Tambun**

👤 **Bonifasius Sinurat**

---

💡 *“Data-driven retention — empowering businesses to act before customers leave.”*
