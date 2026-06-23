<!--
README for the course folder. Fill every ‹TODO› before committing.
Privacy: this is a PUBLIC repo. Teammates' names and student IDs are intentionally omitted.
All figures/metrics below come from the author's own submitted RMIT coursework.
-->

# NYC Taxi & Limousine Commission (TLC) Project - `ISYS3466` Data-Driven Decision Making: Machine Learning for Business Professionals

A journey across the full applied-ML lifecycle: first applying supervised and unsupervised models in **Microsoft Azure ML** to comprehend ML models, then **designing** a data-science solution proposal for NYC TLC (Read case study **[here](Asset/case-study.md)**), and finally **implementing and presenting** a production-grade fare-prediction model to the Microsoft team.

🏆 **[Top Course Grade](Asset/top-course-grade.png)** The team's NYC TLC solution was selected and pitched to **[Microsoft Team](Asset/top-6-selected-team.png)**.

**[Certification](Asset/CoA.png)**: Certification of Archievement - Exceptional efforts and insightful presentation showcasing your expertise in designing and implementing effective data science solutions for business scenarios

**Team:** Gradient Minds / Team 4 - Section 2

**My role:** Business Intelligence Analyst/ Machine Learning Specialist

---

## Table of Contents
| Assessment | Focus | Format | Folder |
|---|---|:---:|:---:|
| **1. Azure AI Exercise** | Supervised classification + unsupervised clustering in Azure ML *(Individual)* | Report | [Assessment1](./Assessment-1-Azure-AI-Exercise) |
| **2. Business opportunity identification and solution design** | Identify a data-science opportunity for NYC TLC and propose a solution design *(Team)* | Slide deck | [Assessment2](./Assessment-2-Solution-Design) |
| **3. Project Implementation and Executive Presentation** | Build, evaluate and pitch a GBDT fare-prediction model integrated into NYC TLC's dispatcher system and driver app *(Team)* | Slide deck & Report | [Assessment3](./Assessment-3-Implementation) |


## Tools <a id="tools"></a>

![Azure ML](https://img.shields.io/badge/Azure_Machine_Learning-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)
![Tableau Prep](https://img.shields.io/badge/TableauPrep-538A9C?style=flat&logo=tableauprep&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-FFFFFF?style=flat&logo=tableau&logoColor=black)

**Models:** Multiclass Logistic Regression · Multiclass Decision Forest · K-Means · Gradient Boosted Decision Tree (Boosted Decision Tree Regression)

**Techniques:** EDA · Median/Mode imputation · Z-score normalisation · Tukey IQR capping · Stratified sampling · Hyperparameter tuning · Permutation feature importance

---

# Assessment 1 — Azure AI Exercise

**Summary.** An individual exercise applying machine learning end-to-end in Azure ML across two business scenarios: a **supervised** cell-phone price-category classifier and an **unsupervised** wine-segmentation clustering model.

### 1. Data used
| Dataset | Source | Shape | Download | In repo |
|---|---|---|---|---|
| Cell Phone Price | Kaggle | 2,000 train / 1,000 test · 20 predictors + `price_range` (4 balanced classes) | [Kaggle](https://www.kaggle.com/datasets/atefehmirnaseri/cell-phone-price) | ‹TODO: `./Assessment-1-Azure-AI-Exercise/data/…`› |
| Wine | UCI ML Repository | 178 obs · 14 variables (13 chemical + class) | [UCI](https://archive.ics.uci.edu/dataset/109/wine) | ‹TODO: `…/data/…`› |

### 2. Method / Techniques
- **Preparation (Azure ML):** median imputation, Z-score normalisation (target excluded), 80/20 holdout split with fixed seed (123); for the test set, transformations learned on training data were re-applied to prevent leakage.
- **Cell phone (classification):** Multiclass Logistic Regression (MLR) vs Multiclass Decision Forest (MDF), with hyperparameter tuning (L2 = 1.0; MDF: 100 trees, depth 10, min leaf 5).
- **Wine (clustering):** K-Means (K-Means++ init, Euclidean distance, normalised features), compared at **K=3** and **K=4**.

### 3. Key findings
- **Cell phone:** **MLR outperformed MDF** — accuracy **0.90 vs 0.8375** — with higher micro/macro precision and recall; relationships were largely linear, with RAM the dominant predictor (≈0.92 correlation).
- **Wine:** **K=3 is optimal** — strongest cluster separation with comparable cohesion, aligning with the dataset's three natural classes; K=4 over-segments and reduces stability.

### 4. Output
- 📄 [Azure AI Exercise Report (PDF)](./Assessment-1-Azure-AI-Exercise/report/ASM1_Azure_AI_Exercise_Report.pdf) — 2,200 words, RMIT Harvard.
- 🖼️ Azure ML pipeline screenshots → ‹TODO: add to `./Assessment-1-Azure-AI-Exercise/azure-pipeline/`›

---

# Assessment 2 — Business Opportunity Identification & Solution Design

**Summary.** A team slide deck identifying a data-science opportunity in the **NYC Taxi & Limousine Commission (TLC)** industry — losing share to ride-hailing — and proposing an end-to-end analytics solution, from data engineering to predictive modelling and business impact.

### 1. Data used
| Dataset | Source | Notes | Download | In repo |
|---|---|---|---|---|
| NYC Yellow Taxi trips (2019) | NYC TLC | ~90M+ rows → ~84M after cleaning | [Azure Open Datasets](https://learn.microsoft.com/en-gb/azure/open-datasets/dataset-taxi-yellow) · [Kaggle](https://www.kaggle.com/datasets/microize/newyork-yellow-taxi-trip-data-2020-2019) | ‹TODO: `…/data/…`› |
| Taxi Zone Lookup | NYC TLC | 263 zones across 5 boroughs | (joined to trip data) | ‹TODO: `…/data/…`› |

### 2. Method / Techniques
- **Approach:** Data Engineering & Geospatial Integration → EDA Visualisation (Tableau) → Predictive Modelling (Azure ML) → Business Impact & ROI.
- **Preprocessing:** capping imputation for the 10–15% null/outlier values; column selection to remove noise; median/mode imputation; outlier filtering; SQL feature transforms (`HourOfDay`, `DayOfWeek`).
- **Proposed model:** Gradient Boosted Decision Tree (justified by NYC demand's non-linear, spiky behaviour), evaluated via MAE and R².

### 3. Key findings
- **Demand** concentrates in **Midtown & Upper East Side** (short, frequent trips).
- **Revenue** concentrates at **airports** despite lower volume (JFK ≈ $55.93, LaGuardia ≈ $43.35 avg revenue/trip).
- Clear **weekday peaks** (7–10 AM, 4–8 PM); fares rise slightly at peak while tips stay flat → flat pricing leaves revenue on the table.

### 4. Output
- 📄 [Solution-Design Deck (PDF)](./Assessment-2-Solution-Design/deck/ASM2_NYC_Taxi_Solution_Design.pdf) — 10 pages.
- 📊 Tableau EDA workbooks → ‹TODO: `./Assessment-2-Solution-Design/tableau/`› · deck visuals → ‹TODO: `…/assets/`›

---

# Assessment 3 — Project Implementation & Executive Presentation

**Summary.** The team implemented the proposed solution as a working **GBDT fare-prediction model** on Azure ML — *"From Proposal to Production: Implementing GBDT for Dynamic Pricing & Fleet Optimisation"* — and presented it to an executive audience. 🏆 Top grade; pitched to Microsoft.

### 1. Data used
| Dataset | Source | Notes | Download | In repo |
|---|---|---|---|---|
| NYC Yellow Taxi trips (2019, 12 monthly files) | NYC TLC | ~84M rows / 12.42 GB after cleaning | [Azure Open Datasets](https://learn.microsoft.com/en-gb/azure/open-datasets/dataset-taxi-yellow) · [Kaggle](https://www.kaggle.com/datasets/microize/newyork-yellow-taxi-trip-data-2020-2019) | ‹TODO: `…/data/…`› |
| Stratified sample | derived | ~5.05M rows · 242/263 zones · 1.5M held-out for validation | (generated by notebook) | ‹TODO: `…/data/…`› |
| Taxi Zone Lookup | NYC TLC | borough/zone enrichment | (joined) | ‹TODO: `…/data/…`› |

### 2. Method / Techniques
Seven-stage Azure ML pipeline: **Tableau Prep** cleaning with Tukey IQR capping (~90M → ~84M rows) → **Python/Jupyter** chunked stratified sampling → **Join + feature selection** (10 features; leakage columns `total_amount`, `tip_amount` dropped) → 70/30 split → **Tune Model Hyperparameters** (random sweep, 20 runs vs RMSE) → **Permutation Feature Importance** → **Score & Evaluate**. Model: Gradient Boosted Decision Tree Regression.

### 3. Key findings
- **Accuracy:** R² = **0.947**, MAE = **$0.54**, RMSE = 2.74 (validated on 1.5M unseen trips).
- **Drivers:** `trip_distance` (~46%) + `trip_duration` (~39%) explain **~85%** of predictions; `RatecodeID` isolates the airport premium (e.g. ~$52 JFK flat rate).
- **Business value:** enables controlled dynamic pricing (~1.2× peak), proactive fleet pre-positioning toward high-value zones (est. 15–20% idle-time reduction), and a 2–3 min target wait time.
- **Ethics:** flags an algorithmic feedback-loop risk (≈95% Manhattan concentration); GBDT chosen partly for auditable feature importance; uses anonymised trip records only.

### 4. Output
- 📄 [Implementation Report (PDF)](./Assessment-3-Implementation/report/ASM3_NYCTLC_Fare_Prediction_Implementation.pdf) — 2,750 words, RMIT Harvard.
- 🎤 Executive pitch deck → ‹TODO: `./Assessment-3-Implementation/deck/`›
- 🖥️ UI mockups (Fleet Command Center dashboard + Driver App) → ‹TODO: `…/dashboards/`›
- 🔧 Tableau Prep flow → ‹TODO: `…/tableau-prep/`› · Python sampling notebook → ‹TODO: `…/python/`› · Azure pipeline + evaluation screenshots → ‹TODO: `…/azure-pipeline/`›

---

<sub>All datasets are public/simulated; no confidential data is included. Figures and metrics are taken from the author's own submitted RMIT coursework.</sub>
