# 🌾 Seasonal Agriculture Performance Analysis

An exploratory data analytics project that investigates **how agricultural performance changes across the three Indian growing seasons — Kharif, Rabi and Zaid** — using 4,000 farm records. The analysis covers data cleaning, feature engineering, season-wise comparison of productivity, economics, resource efficiency and risk, and correlation analysis linking environmental conditions to outcomes.

> Major Project · Data Analytics

---

## 📑 Table of Contents

1. [Problem Statement](#-problem-statement)
2. [Objectives](#-objectives)
3. [Dataset](#-dataset)
4. [Project Workflow](#-project-workflow)
5. [Key Findings](#-key-findings)
6. [Insights & Recommendations](#-insights--recommendations)
7. [Tech Stack](#-tech-stack)
8. [Repository Structure](#-repository-structure)
9. [Getting Started](#-getting-started)
10. [Limitations](#-limitations)
11. [Future Scope](#-future-scope)
12. [Who Can Use This?](#-who-can-use-this)

---

## 🎯 Problem Statement

Agricultural activity is shaped by seasonal changes in weather, farming practices, resource availability and market conditions, so performance naturally differs from one season to another. Raw agricultural data, however, does not explain *how* performance shifts or *what* patterns exist in each season.

This project analyzes the dataset to uncover meaningful patterns, trends, relationships and variations in seasonal agricultural performance, and turns them into evidence-based conclusions.

## ✅ Objectives

- Explore, understand and clean the dataset
- Compare performance across seasons on four dimensions: **productivity, economics, resource efficiency and risk**
- Identify seasonal patterns, unusual observations and outliers
- Investigate relationships between environmental/input variables and performance outcomes
- Draw data-driven conclusions and recommendations for seasonal planning

---

## 📊 Dataset

| Property | Detail |
|---|---|
| File | `seasonal_agriculture_performance_dataset.csv` |
| Records | 4,000 farms |
| Columns | 28 (plus engineered columns during analysis) |
| Seasons | Kharif (1,779), Rabi (1,627), Zaid (594) |
| Crops (8) | Wheat, Maize, Pulses, Rice, Cotton, Chilli, Groundnut, Sugarcane |
| States (8) | Andhra Pradesh, Maharashtra, Telangana, Karnataka, Gujarat, Tamil Nadu, Punjab, Madhya Pradesh |
| Irrigation methods | Drip, Flood, Rainfed, Sprinkler |

### Variable classification used in the analysis

| Category | Columns |
|---|---|
| **Grouping variables** | `Farm_ID`, `State`, `District`, `Crop`, `Season`, `Irrigation_Method` |
| **Environmental factors** | `Rainfall_mm`, `Avg_Temperature_C`, `Humidity_pct`, `Sunlight_Hours_Day`, `Soil_pH`, `Soil_Moisture_pct` |
| **Inputs** | `Nitrogen_kg_ha`, `Phosphorus_kg_ha`, `Potassium_kg_ha`, `Seed_Quality_Score` |
| **Productivity metrics** | `Yield_Tonnes_Ha`, `Production_Tonnes` |
| **Economic metrics** | `Market_Price_INR_Tonne`, `Total_Cost_INR`, `Revenue_INR`, `Profit_INR` |
| **Resource-efficiency metrics** | `Fertilizer_kg_ha`, `Pesticide_Litre_ha`, `Water_Used_m3`, `Water_Efficiency_t_per_1000m3`, `Farm_Area_Hectares` |
| **Risk metric** | `Disease_Pest_Risk_pct` |

---

## 🔬 Project Workflow

### 1. Data understanding
Inspected structure with `info()` and `describe()`, then classified all 28 columns into the categories above, with **`Season` as the central variable** of the analysis.

### 2. Data cleaning
- **Missing values found:** `Rainfall_mm` (48), `Soil_Moisture_pct` (40), `Yield_Tonnes_Ha` (32)
- Plotted histograms to check distributions before choosing an imputation strategy
- **Imputed with the season-wise median** (`groupby('Season').transform('median')`), because the variables differ strongly by season and are skewed (rainfall and yield are right-skewed), which makes the mean misleading

### 3. Feature engineering
- Created `Water_Used_Per_Ha = Water_Used_m3 / Farm_Area_Hectares` so water use is comparable across farms of different sizes

### 4. Data validation
| Check | Result |
|---|---|
| `Revenue − Total_Cost` vs `Profit_INR` | Matches **exactly** for all 4,000 rows |
| `Production × Market_Price` vs `Revenue_INR` | Differences within **±0.5 INR** (rounding only) |

### 5. Outlier handling — the Sugarcane effect
Sugarcane yields roughly 30–100+ t/ha, while all other crops stay under about 6 t/ha. This inflates means and widens the mean–median gap, so every season-wise statistic was computed **both with and without Sugarcane**, and the **median** was preferred as the summary statistic.

### 6. Season-wise statistical comparison
`groupby('Season').describe()` for each metric class (productivity, economic, resource efficiency, risk, inputs, environment), with and without Sugarcane.

### 7. Visualization & correlation analysis
Box plots, violin plots, scatter plots, bar plots, and correlation heatmaps (inputs/environment vs outcomes) for all seasons combined, for each season separately, and with Sugarcane excluded.

---

## 📈 Key Findings

### Season ranking summary

| Metric | Kharif | Rabi | Zaid |
|---|---|---|---|
| Median yield, excl. Sugarcane (t/ha) | **1.81** | 1.54 | 1.33 |
| Average profit, all crops (INR) | **+1,78,915** | +87,689 | **−24,805** |
| Median profit, all crops (INR) | **+38,808** | −3,187 | −62,144 |
| Share of farms making a loss (all crops) | 42.2% | 51.1% | **64.5%** |
| Avg. disease/pest risk (%) | **54.5** | 40.5 | 38.2 |
| Avg. rainfall (mm) | **852** | 436 | 299 |
| Avg. temperature (°C) | 28.5 | 23.5 | **31.0** |
| Avg. humidity (%) | **71.8** | 57.9 | 52.0 |
| Avg. sunlight (hrs/day) | 6.8 | 7.6 | **8.2** |
| Water efficiency, mean excl. Sugarcane (t / 1000 m³) | **3.62** | 3.23 | 2.63 |

### Detailed observations

1. **Crop type drives raw yield more than season does.** Sugarcane dwarfs every other crop; among the rest, Maize (~2.85 t/ha median) and Rice (~2.46) lead, and Pulses (~0.94) trail. Sugarcane must be analyzed separately for fair seasonal comparisons.
2. **Productivity ranks Kharif > Rabi > Zaid**, both with and without Sugarcane. Distributions are heavily right-skewed, so medians are more trustworthy than means.
3. **Economics follow the same ranking.** Kharif is the most profitable season, Rabi is moderate, and **Zaid is the only season with a negative average profit**. Zaid also has the highest average total cost (≈ ₹5.44 lakh vs ≈ ₹5.32 lakh in Kharif), so farmers spend the most in the season that returns the least.
4. **Market prices are essentially flat across seasons** (≈ ₹44–45k per tonne on average), so profit differences come from **yield and cost, not price**.
5. **Zaid is the least water-efficient season** and uses the most water on average, while Kharif is the most efficient.
6. **Kharif carries the highest disease/pest risk**, while Zaid carries the lowest.
7. **Disease/pest risk is driven by environment.** Correlation with risk: Rainfall (**+0.63**), Humidity (**+0.55**), Soil Moisture (**+0.38**), Temperature (+0.25), Sunlight (**−0.25**).
8. **Inputs show near-zero correlation with outcomes.** Nitrogen, phosphorus, potassium, fertilizer and seed quality barely relate to yield or profit, and their averages are almost identical across seasons. Inputs appear to be applied uniformly rather than adapted to season or crop.
9. **Rainfall matters once Sugarcane is excluded.** With Sugarcane included the rainfall–yield link is hidden; without it, rainfall, soil moisture and humidity show a modest positive relationship with yield (r ≈ 0.12–0.16).

---

## 💡 Insights & Recommendations

- **Plan by season, not just by crop.** Kharif is the most reliable season; Zaid needs the most careful planning.
- **Reduce Zaid exposure** by favouring higher-yielding crops (Maize, Rice) or cutting costs, since about 65% of Zaid farms are loss-making.
- **Improve Zaid water efficiency** through better irrigation methods and scheduling (e.g. drip/sprinkler), because Zaid has low rainfall and high temperature.
- **Increase disease/pest monitoring in Kharif**, when humidity and rainfall push risk highest; use season-specific alerts.
- **Adapt inputs to conditions.** Uniform fertilizer application does not translate into yield gains, so input optimization is an opportunity to cut cost without losing output.
- **Treat Sugarcane as a separate category** in policy and benchmarking.

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **Python** | Core language |
| **Pandas** | Data loading, cleaning, grouping |
| **NumPy** | Numerical operations |
| **Matplotlib** | Plotting |
| **Seaborn** | Statistical visualizations and heatmaps |
| **Jupyter Notebook** | Documenting the complete analysis |

---

## 📁 Repository Structure

```
Seasonal-Agriculture-Performance-Analysis/
│
├── Seasonal_Agriculture_Performance.ipynb              # Full analysis notebook
├── seasonal_agriculture_performance_dataset.csv        # Dataset (4,000 rows × 28 columns)
├── Major_Project_Seasonal_Agriculture_Performance_Analysis.pdf   # Problem statement / project brief
├── Project_Presentation.pptx                           # Presentation of results
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab

### Installation

```bash
# 1. Clone the repository
git clone <repository-url>
cd <repository-folder>

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install numpy pandas matplotlib seaborn jupyter

# 4. Launch the notebook
jupyter notebook Seasonal_Agriculture_Performance.ipynb
```

Keep the CSV in the **same folder** as the notebook, since it is loaded with a relative path:

```python
agri_df = pd.read_csv("seasonal_agriculture_performance_dataset.csv")
```

Then run all cells from top to bottom (`Kernel → Restart & Run All`).

---

## ⚠️ Limitations

- The dataset appears to be **synthetic or simulated**: some State–District pairings are not geographically consistent (e.g. Rajkot listed under Andhra Pradesh), and input variables show almost no relationship with yield. Findings describe this dataset and should not be generalized to real-world farms without validation.
- Correlation does not imply causation.
- Zaid has fewer records (594) than Kharif or Rabi, so its estimates are less certain; Zaid's profit confidence interval crosses zero.
- Median imputation of missing values (about 3% or fewer per column) may slightly understate natural variability.
- Season-wise results are dominated by crop mix; crop-level and region-level comparisons within each season are a natural next step.

---

## 🔭 Future Scope

- **Crop recommendation system** based on location, season, soil and rainfall forecast
- **Predictive models** (regression / tree-based) for yield and profit from weather forecasts and planned inputs
- **Irrigation advisory** to close Zaid's water-efficiency gap
- **Season-specific disease/pest alerts** delivered to farmers
- Statistical significance testing (ANOVA / Kruskal–Wallis) for the seasonal differences
- Interactive dashboard (Power BI / Streamlit) for stakeholders

---

## 👥 Who Can Use This?

1. Farmers
2. Agricultural policymakers
3. Agri-finance and insurance providers
4. Agri-tech companies
5. Researchers and agronomists
6. Water and resource boards
