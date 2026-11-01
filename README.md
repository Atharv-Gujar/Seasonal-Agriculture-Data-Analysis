# Seasonal Agriculture Performance Analysis

An exploratory data analysis project investigating how agricultural performance changes across the **Kharif, Rabi, and Zaid** growing seasons.

The analysis uses 4,000 farm records to compare productivity, profitability, resource efficiency, environmental conditions, agricultural inputs, and disease/pest risk. It also examines relationships between environmental/input variables and performance outcomes using correlation analysis.

## Project objectives

- Clean and validate the seasonal agriculture dataset.
- Compare farm performance across the three growing seasons.
- Evaluate productivity, economic performance, resource efficiency, and risk.
- Study how rainfall, temperature, soil conditions, inputs, and seed quality relate to yield and profitability.
- Identify the effect of high-yield crops, especially sugarcane, on aggregate statistics.

## Key findings

- **Kharif** ranks highest overall for productivity, economic performance, and resource efficiency in the analysis.
- **Rabi** generally falls between Kharif and Zaid across the main performance measures.
- **Zaid** shows the weakest overall performance and the highest financial pressure, with average profit becoming negative in the analysis.
- Sugarcane has substantially higher yield than the other crops and can strongly skew averages, so comparisons are also repeated with sugarcane excluded.
- Seasonal environmental conditions, particularly rainfall and soil moisture, help explain differences in yield between seasons.
- Correlation heatmaps are produced for all seasons together, for each individual season, and for non-sugarcane records.

> These are descriptive findings from the supplied dataset and should not be interpreted as causal conclusions.

## Dataset

`seasonal_agriculture_performance_dataset.csv` contains farm-level records with fields covering:

- **Location and grouping:** state, district, crop, season, and irrigation method
- **Farm and inputs:** farm area, fertilizer, pesticide, nitrogen, phosphorus, potassium, and seed quality
- **Environment:** rainfall, temperature, humidity, sunlight, soil pH, and soil moisture
- **Outcomes:** yield, production, market price, total cost, revenue, profit, water usage, water efficiency, and disease/pest risk

The main seasonal categories are `Kharif`, `Rabi`, and `Zaid`.

## Analysis workflow

1. Load the CSV with pandas and inspect its structure and distributions.
2. Impute missing rainfall, soil moisture, and yield values using season-level medians.
3. Create `Water_Used_Per_Ha` to normalize total water usage by farm area.
4. Validate the consistency of reported profit and revenue against calculated values.
5. Group variables into productivity, economic, resource-efficiency, risk, input, and environmental classes.
6. Compare descriptive statistics by season, both with all crops and with sugarcane excluded.
7. Visualize crop, season, irrigation, environmental, input, and water-use relationships.
8. Generate correlation heatmaps linking environmental/input variables to performance outcomes.

## Repository contents

| File | Description |
| --- | --- |
| `Seasonal_Agriculture_Performance.ipynb` | Main, cleaned analysis notebook |
| `Seasonal_Agriculture_Performance-checkpoint.ipynb` | Notebook checkpoint copy |
| `seasonal_agriculture_performance_dataset.csv` | Farm-level input dataset |
| `Major Project_Seasonal Agriculture Performance Analysis.pdf` | Project report |
| `VOIS_Major_Project_PPT_Submission.pptx` | Project presentation |

## Getting started

### Requirements

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- pandas
- NumPy
- Matplotlib
- Seaborn

### Run locally

```bash
git clone https://github.com/Atharv-Gujar/Seasonal-Agriculture-Data-Analysis.git
cd Seasonal-Agriculture-Data-Analysis
python -m pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook Seasonal_Agriculture_Performance.ipynb
```

Run the notebook from the repository root so it can locate `seasonal_agriculture_performance_dataset.csv`.

## Notes and limitations

- The project is exploratory and uses descriptive statistics and correlations; it does not train a predictive model.
- Correlation does not establish causation.
- Sugarcane is an important outlier in yield comparisons, so results should be interpreted with the crop mix in mind.
- Reported findings depend on the quality, completeness, and representativeness of the supplied dataset.

## Author

**Atharv Gujar**

[Repository](https://github.com/Atharv-Gujar/Seasonal-Agriculture-Data-Analysis)