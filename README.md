# 🚕 NYC Yellow Taxi — Fare & Trip Distance Prediction

**Capstone project (Group 9) · Post-Graduate Diploma in Data Analytics for Business, St. Clair College**

End-to-end analysis of **383,102 NYC Yellow Taxi trips from 2023** (a 10% monthly sample of NYC TLC trip records): data cleaning, exploratory analysis, feature engineering, and predictive models for **fare amount** and **trip distance**, plus an interactive Tableau dashboard.

**Highlights**
- Cleaned 383K raw trips down to ~321K valid records (invalid trips, negative fares and outliers removed)
- Compared Linear Regression, Random Forest, Gradient Boosting (tuned) and an Artificial Neural Network (Keras/TensorFlow)
- **Fare amount:** ANN and tuned Gradient Boosting both reach **R² ≈ 0.99** (test RMSE ≈ $1.45)
- **Trip distance:** ANN reaches **R² = 0.953** (test RMSE 0.82 miles) vs 0.878 for tuned Gradient Boosting

---

## 🔍 Business Questions

- What drives taxi fares, and how accurately can a fare be estimated?
- How far will a trip go, based on where and how it starts?
- When and where is demand highest, and how do payment type and tipping behave?

---

## 🧠 Approach

1. **Data cleaning** — fixed encodings and datetimes, removed 11,541 invalid trips and negative fares, imputed missing values, removed outliers
2. **Exploratory analysis** — distributions, univariate/bivariate/multivariate analysis, weekday × hour demand heatmap, tip % by payment type, top pickup/drop-off zones
3. **Feature engineering** — trip duration, time-of-day and weekday features, borough and zone mapping, same-borough flag, demand by time slot
4. **Modelling** — Linear Regression (baseline), Random Forest, Gradient Boosting, ANN, for two targets
5. **Tuning & evaluation** — `RandomizedSearchCV` for Gradient Boosting; RMSE and R² on a held-out test set; feature importance and residual analysis

---

## 💡 Key Findings

**Demand & behaviour**
- Most trips are short (under 5 miles) with fares under $30
- Demand peaks on weekday evenings (5–8 PM), especially Thursdays and Fridays
- Credit card is the dominant payment method and is associated with higher tip percentages
- Pickups and drop-offs concentrate in Manhattan and at JFK and LaGuardia airports

**Model results (test set)**

| Target | Model | RMSE | R² |
|---|---|---|---|
| Fare amount | **ANN** | **1.451** | **0.9899** |
| Fare amount | Tuned Gradient Boosting | 1.463 | 0.9897 |
| Fare amount | Linear Regression | 2.298 | 0.9746 |
| Fare amount | Random Forest | 3.951 | 0.9251 |
| Trip distance | **ANN** | **0.818** | **0.9531** |
| Trip distance | Tuned Gradient Boosting | 1.317 | 0.8783 |
| Trip distance | Linear Regression | 1.535 | 0.8345 |
| Trip distance | Random Forest | 1.920 | 0.7417 |

**What drives the predictions**
- **Fare:** trip distance (85% of importance) and trip duration (14%) — the fare is close to a metered function of these two
- **Trip distance:** rate code, pickup borough (Queens) and airport pickups (JFK, LaGuardia) — where a trip starts strongly signals how far it goes

**Recommendation:** for fare, tuned Gradient Boosting matches the ANN almost exactly while being faster and explainable through feature importances. For trip distance, the ANN is clearly more accurate and worth its extra training cost.

---

## ⚠️ Limitations

- Fare models use trip distance and duration, which are only known once a trip ends, so they estimate the final fare rather than quote a price upfront. A pre-trip model would rely on pickup/drop-off zones and time only.
- Data covers a 10% sample of 2023 trips.

---

## 🛠️ Tools

Python (Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Keras/TensorFlow) · Tableau · Excel

---

## 📁 Repository Contents

```
├── NYC_EDA_GRP9_FINAL.ipynb   # Final notebook: cleaning, EDA, modelling, ANN, evaluation
├── Dashboard_NYC.twbx         # Tableau dashboard (open with Tableau Desktop or Tableau Reader)
└── archive/                   # Earlier working drafts of the notebook
```

## ⚙️ How to Run

Download 2023 Yellow Taxi trip records from the [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) page, create a 10% monthly sample saved as `sampled_10_percent_by_month.csv`, place it next to the notebook and run `NYC_EDA_GRP9_FINAL.ipynb` in Jupyter.

---

## 👩‍💻 Author

**Gowri S Nair** — Data Analyst · [LinkedIn](https://www.linkedin.com/in/gowri-s-nair-9ba795354) · [GitHub](https://github.com/GowriSNair)

Group project completed with Group 9 teammates at St. Clair College.

**My role:** I led the data cleaning and preprocessing (383K raw trips down to ~321K valid records), checked and validated the analysis and model results, and contributed to most other stages of the project.
