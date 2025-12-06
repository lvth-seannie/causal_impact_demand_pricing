# causai-impact-demand-pricing

This repository contains the source code and data analysis for the journal paper Causal impacts of airline pricing strategies on passenger demand: A comparative evaluation of traditional and causal machine learning approaches. This project leverages advanced Causal Machine Learning (CML) techniques, specifically Double Machine Learning (DML) and Causal Forests, to estimate price elasticity and uncover heterogeneous treatment effects across different market segments.

## 📖 Overview

Understanding the elasticity of passenger demand is critical for airline revenue management and policy-making. Traditional econometric models often struggle with high-dimensional confounding and non-linear relationships.

This project addresses these challenges by:
1.  **Constructing a comprehensive dataset:** Merging quarterly consumer airfare data (DB1B) with external economic indicators (Fuel Prices) and temporal event flags (COVID-19, 9/11).
2.  **Applying Double Machine Learning (DML):** Utilizing the `EconML` library to estimate the Average Treatment Effect (ATE) of fare on demand while controlling for complex confounders.
3.  **Analyzing Heterogeneity:** Using Causal Forests to identify key drivers of price sensitivity (e.g., market competition, route distance, fuel costs).
4.  **Robustness Testing:** Implementing rigorous sensitivity analysis (DoWhy refuters) to validate findings against unobserved confounding.

## 📂 Repository Structure
```
├── codes/                 
│   └── 01_EDA.ipynb             # Data Preprocessing & Exploratory Analysis
│   ├── 02_Traditional_ML.ipynb  # Predictive Modeling (Gradient Boosting, RF)
│   └── 03_Causal.ipynb          # Causal Inference (DML, Causal Forests)  
├── datasets/
│   ├── raw/                     # Raw input files (DB1B, Fuel Prices)
│   └── processed/               # Cleaned CSVs (base_df.csv, final_df.csv)
├── outputs/                     # Generated plots and figures (Causal Graphs, Trees)
├── README.md                    # Project documentation
└── LICENSE                      # MIT License
```
The analysis is divided into three sequential Jupyter Notebooks:

* **`01_EDA.ipynb`**: **Data Preprocessing & Exploratory Data Analysis**
    * Loads raw DB1B and fuel price data.
    * Performs cleaning, merging, and feature engineering (e.g., `holiday_intensity`, `is_major_event`).
    * Visualizes data distributions, correlations, and time-series trends.
    * *Output:* Generates `base_df.csv`.

* **`02_Traditional_ML.ipynb`**: **Predictive Modeling**
    * Prepares data for machine learning (scaling, one-hot encoding).
    * Trains and evaluates traditional regression models (Linear Regression, XGBoost, Random Forest) to predict passenger demand.
    * Analyzes feature importance to inform the causal graph.
    * *Output:* Generates `final_df.csv` used for causal inference.

* **`03_Causal.ipynb`**: **Causal Inference**
    * Defines the Causal Graph (DAG) and identification strategy.
    * **ATE Estimation:** Uses `LinearDML` with tuned nuisance estimators (`GradientBoostingRegressor`) to estimate global price elasticity.
    * **CATE Estimation:** Uses `CausalForestDML` to estimate heterogeneous treatment effects.
    * **Interpretation:** Visualizes heterogeneity using Single Tree Policy Interpreters and SHAP values.
    * **Sensitivity Analysis:** Validates results using Placebo tests and "Add Unobserved Common Cause" refuters (DoWhy).

## 🚀 Getting Started

### Prerequisites

To run the notebooks, you will need Python 3.x and the following libraries:

* `pandas`, `numpy`, `matplotlib`, `seaborn`
* `scikit-learn`, `xgboost`
* `econml` (Microsoft Research)
* `dowhy` (PyWhy)
* `causalml` (Uber)
* `holidays`
* `networkx`
* `shap`

### Installation
It is recommended to use a virtual environment to avoid dependency conflicts.
1.  Clone this repository:
   ```bash
   git clone [https://github.com/lvth-seannie/causal-impact-demand-pricing.git](https://github.com/lvth-seannie/causal-impact-demand-pricing.git)
   cd causal-impact-demand-pricing
   ```
2. Create and activate a virtual environment (optional but recommended):    
   ```bash
   # Windows
   python -m venv venv
   .\venv\Scripts\activate
   
   # Mac/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```
2.  Install the required packages:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost econml dowhy causalml holidays networkx shap
   ```
