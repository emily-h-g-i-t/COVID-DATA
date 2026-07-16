# COVID-19 Data Dashboard

An interactive dashboard exploring COVID-19 cases, deaths, and demographic/economic factors across ~200 countries, built with vanilla JavaScript and [Chart.js](https://www.chartjs.org/). Includes the companion Jupyter notebook used to clean, merge, and analyze the underlying data.

**[Live demo →](#)** *(replace with your GitHub Pages / Netlify link once deployed)*

![dashboard preview](#) *(optional: add a screenshot here)*

## What it does

- **Compare countries over time** — pick countries by continent and add up to 8 to compare cumulative cases and deaths per million, month by month from 2020–2024
- **GDP vs. deaths scatter** — bubble chart plotting GDP per capita against deaths per million, bubble size scaled by population, colored by k-means cluster
- **Top 15 by deaths per million** — a live-recalculated bar chart across the full country dataset
- **Clustering** — countries are grouped into 4 clusters based on pandemic outcomes, demographics, and economic indicators (see notebook for methodology)

## Data source

Data comes from [Our World in Data's COVID-19 dataset](https://github.com/owid/covid-19-data), combining:
- `total_deaths.csv`, `total_deaths_per_million.csv`, `total_cases_per_million.csv` — daily time series (wide format)
- `owid-covid-data.csv` — country demographic and economic characteristics (population, GDP per capita, median age, hospital beds per capita, HDI, etc.)

## Files in this repo

| File | Description |
|---|---|
| `index.html` | The dashboard itself — a single self-contained HTML/JS/Chart.js file, no build step or server required |
| `covid_analysis.ipynb` | Jupyter notebook: cleans and merges the raw OWID CSVs, runs k-means clustering, and fits a regression model to identify predictors of death rate |

## Running it locally

The dashboard is a static file — no installation needed:

```bash
git clone https://github.com/YOUR_USERNAME/covid-dashboard.git
cd covid-dashboard
open index.html   # or double-click it, or serve with e.g. VS Code's Live Server extension
```

To re-run the analysis notebook, you'll need the four source CSVs (linked above) in the same folder, plus:

```bash
pip install pandas numpy matplotlib scikit-learn statsmodels
jupyter notebook covid_analysis.ipynb
```

## Analysis highlights

- A multiple regression across median age, GDP per capita, population density, hospital beds per capita, and HDI explains about **52% of the variation** in deaths per million across countries (R² = 0.52)
- **Median age** is the strongest, most statistically significant predictor — older populations saw meaningfully higher death rates
- Countries cluster into roughly four groups by pandemic outcome and demographic/economic profile (see notebook Section 7 for full breakdown)

## Built with

- Vanilla JavaScript (no framework) — `.map()`, `.filter()`, `.sort()`, and DOM event listeners for all the interactivity
- [Chart.js](https://www.chartjs.org/) for line, bubble, and bar charts
- Python (pandas, scikit-learn, statsmodels) for the data cleaning, clustering, and regression in the notebook

## About this project

I built this as a hands-on way to learn JavaScript fundamentals — DOM manipulation, event listeners, and working with real datasets in the browser — after first doing the data analysis side in Python/pandas.
