# Kenya GDP Projection & Sector Impact Model

> **Status: In Progress — Data Exploration and Ingestion Phase**<br>
> *Note: This repository represents ongoing empirical research. Data ingestion and exploratory data analysis (EDA) for baseline macroeconomic indicators are actively underway. GDP econometric forecasting models and sector-impact transmissions have not yet been implemented or finalized.*

---

## 1. Project Overview & Motivation

Kenya’s economy is East Africa's economic anchor, yet it experiences macroeconomic shocks driven by climatic variability, terms-of-trade volatility, currency fluctuations, and domestic fiscal debt dynamics. Accurate medium-term economic forecasting is critical for fiscal policy planners, multilateral partners, and private-sector decision-makers.

The **Kenya GDP Projection & Sector Impact Model** is an analytical data science initiative designed to:
1. Forecast Kenya's real Gross Domestic Product (GDP) over a **three-year forward horizon** at **quarterly frequency**.
2. Empirically model how shifts in headline growth propagate into key socio-economic sectors: **Agriculture**, **Health**, and **Employment**.

---

## 2. Project Objectives

- **Macroeconomic Forecasting:** Develop and benchmark univariate and multivariate time-series models (e.g., ARIMA/SARIMAX, Vector Autoregression [VAR], and machine learning regressors) to project quarterly real GDP.
- **Explanatory Transmission Analysis:** Incorporate key transmission variables—headline inflation, Central Bank Rate (CBR), USD/KES exchange rates, and fiscal deficit indicators—to understand macroeconomic drivers.
- **Sector Sensitivity Analysis:** Estimate historical elasticities and impulse-response dynamics between aggregate real GDP growth and key sectors (agricultural output, healthcare budget absorption/allocations, and formal/informal employment indicators).
- **Portfolio Demonstration:** Provide an end-to-end, reproducible, and mathematically rigorous econometrics and machine learning repository suitable for portfolio demonstration in economic analytics.

---

## 3. Project Scope & Roadmap

| Component | Status | Description |
| :--- | :--- | :--- |
| **Data Inventory & Quality Audit** | **Completed** | Initial ingestion, audit, datetime parsing, and deduplication of monthly inflation data (2005–2026). Documented in `notebooks/01_data_inventory.ipynb`. |
| **Inflation Exploratory Analysis** | **Completed** | Statistical distribution, volatility profiling, and visualization of 12-month headline inflation and annual average inflation trends. |
| **GDP Series Ingestion (KNBS)** | *Planned* | Ingestion of official Kenya National Bureau of Statistics (KNBS) quarterly real GDP releases and historical series. |
| **Explanatory Variable Pipeline** | *Planned* | Ingestion and frequency harmonization of Central Bank Rate (CBR), commercial lending rates, USD/KES exchange rates, and revenue/fiscal data. |
| **Time-Series Forecasting Models** | *Planned* | Stationarity testing (ADF, KPSS), seasonal adjustment, train-test splits, walk-forward cross-validation, and benchmarking (ARIMA/SARIMAX, VAR, Ridge/ElasticNet, Gradient Boosting). |
| **Sector Impact Assessment** | *Planned* | Econometric modeling of sector channels: Agriculture (value added), Health, and Employment. |

---

## 4. Data Sources & Explanatory Variables

### Intended Data Sources
- **Kenya National Bureau of Statistics (KNBS):** Quarterly GDP Reports (QGDP), Economic Surveys, Leading Economic Indicators (LEI), and Statistical Abstracts.
- **Central Bank of Kenya (CBK):** Monthly Inflation Series, Central Bank Rate (CBR), USD/KES daily/monthly foreign exchange averages, and commercial bank credit statistics.
- **National Treasury & Economic Planning:** Quarterly Economic and Budgetary Reviews (QEBR) for public debt and revenue/fiscal indicators.
- **World Bank / IMF:** World Development Indicators (WDI) and International Financial Statistics for secondary cross-validation.

### Target & Explanatory Variables
- **Target Variable ($Y_t$):** Kenya Real GDP (Quarterly, constant prices, KNBS).
- **Explanatory Variables ($X_t$):**
  - **Price Stability:** 12-Month Headline Inflation rate (%) & Annual Average Inflation rate (%) *(ingested)*.
  - **Monetary Policy:** Central Bank Rate (CBR, %) and Interbank rates.
  - **External Sector:** USD/KES nominal and real effective exchange rate (REER).
  - **Fiscal Indicators:** Total public debt-to-GDP ratio and fiscal deficit.
  - **Sector Drivers:** Rainfall / weather anomaly proxies (Agriculture) and credit to the private sector.

---

## 5. Current Verified Findings (Notebook 01 Outputs)

The initial exploratory notebook (`notebooks/01_data_inventory.ipynb`) evaluated the raw monthly inflation dataset (`kenya_inflation_raw.xlsx.csv`):

- **Temporal Coverage:** January 2005 through September 2026 (spanning 22 calendar years).
- **Data Quality & Hygiene:**
  - The raw dataset contained 262 entries.
  - Exactly **1 duplicate entry** was detected and isolated (`April 2019`, identical recorded inflation figures).
  - Deduplicating reduced the dataset to **261 contiguous monthly observations** with zero missing calendar months over the entire 2005–2026 horizon.
- **Empirical Distributions (261 Observations):**
  - **12-Month Headline Inflation:** Mean of **7.22%** (Std. Dev: 3.85%), ranging between a minimum of **1.85%** (April 2007) and a maximum of **19.72%** (November 2011). Median: **6.26%**.
  - **Annual Average Inflation:** Mean of **7.38%** (Std. Dev: 3.30%), ranging from **3.55%** to **17.07%**. Median: **6.34%**.
- **Historical Context:** Highlights severe inflationary pressure periods in 2008 (global food/fuel shock and post-election unrest) and late 2011 (exchange rate depreciation and drought), moderating towards the CBK target band (5.0% $\pm$ 2.5%) in recent periods.

> *Note: A naive 3-month flat persistence projection demonstrated in Cell 17 of Notebook 01 serves solely as an illustrative notebook output placeholder and does not constitute a trained forecasting model.*

---

## 6. Repository Structure

```text
kenya_gdp_projection/
├── data/
│   ├── raw/                       # Original, unedited raw datasets (read-only)
│   │   └── kenya_inflation_raw.xlsx.csv  # Monthly inflation history (KNBS/CBK)
│   └── processed/                 # Cleaned, frequency-aligned datasets (git-retained)
├── models/                        # Serialized model artifacts & parameter checkpoints
├── notebooks/                     # Jupyter analysis & prototyping notebooks
│   └── 01_data_inventory.ipynb   # Inflation data cleaning, audit, & EDA
├── outputs/                       # Exported figures, evaluation tables, and forecasts
├── .gitignore                     # Git exclusion rules for Python & Jupyter environments
├── README.md                      # Project documentation and research overview
└── requirements.txt               # Pinned project dependencies
```

---

## 7. Setup & Installation (Windows PowerShell)

### Prerequisites
- Python 3.11 or 3.12 installed on Windows.
- Git installed on your local machine.

### Step 1: Clone the Repository
```powershell
git clone <YOUR_REPOSITORY_URL>
cd "Kenya GDP Projection & Sector Impact Model\kenya_gdp_projection"
```

### Step 2: Create and Activate Virtual Environment
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```
*(If PowerShell restricts script execution, run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` once).*

### Step 3: Upgrade Pip & Install Dependencies
```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Step 4: Launch JupyterLab / Notebooks
```powershell
jupyter lab
```
Navigate to `notebooks/01_data_inventory.ipynb` to view or step through the exploratory audit.

---

## 8. Dependencies

Key dependencies specified in `requirements.txt`:
- **Data Engineering:** `pandas`, `numpy`, `openpyxl`
- **Visualization:** `matplotlib`, `seaborn`
- **Econometrics & ML:** `statsmodels`, `scipy`, `scikit-learn`
- **Environment:** `jupyterlab`, `ipykernel`

---

## 9. Current Limitations & Next Steps

### Limitations & Assumptions
- **Frequency Discrepancy:** High-frequency variables (monthly inflation, exchange rates) must be aggregated (average vs. quarter-end) to align with quarterly GDP releases without lookahead bias.
- **Reporting Lags:** Official KNBS quarterly GDP figures typically publish with a 90-day lag.
- **Structural Shifts:** The series includes major structural breaks (e.g., rebasing of Kenya's national accounts in 2014 and 2021, and the COVID-19 shock in 2020).

### Immediate Next Steps
1. Ingest official quarterly real GDP data from KNBS (2010–present).
2. Codify the quarterly aggregation pipeline in `data/processed/`.
3. Construct the multivariate feature matrix (GDP, Inflation, CBR, USD/KES).
4. Implement baseline stationarity tests and fit benchmark forecasting models (SARIMAX / VAR).
5. Formulate the sectoral transmission equations for agriculture, health, and employment.

---

## 10. License & Author

- **Author:** Computer Science Graduate & Data Science Researcher
- **Focus:** Time Series Econometrics, Macroeconomic Analytics & Applied Machine Learning
- **License:** MIT License (or open for academic/research demonstration)
