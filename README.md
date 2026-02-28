# Causal Impact of Pricing on Passenger Demand

## Causal impacts of airline pricing strategies on passenger demand: A comparative evaluation of traditional and causal machine learning approaches

This repository contains the data, analysis notebooks, and high-resolution outputs for a causal inference study on airline ticket pricing. We employ **Double Machine Learning (DML)** and **Causal Forests** to estimate the Average Treatment Effect (ATE) of fare changes on passenger volume while accounting for complex confounding factors.

## 💡 Key Research Findings
* **Estimated ATE:** -4.008 (p < 0.001), indicating a statistically significant inverse relationship between fare and demand.
* **Robustness:** Our findings remain stable across a Leave-One-Out (LOO) sensitivity analysis, with the ATE consistently remaining negative despite the removal of major confounders.
* **Sensitivity:** Causal refutation tests confirm the model is robust to potential unobserved common causes (up to a correlation threshold of 0.3).

## 🛢️ Data Source
The raw airline dataset used in this study is too large to be hosted directly on GitHub. You can access the original source files at the following location:

* **Source Name:** [Domestic Airline Consumer Airfare (DACA) - US Department of Transportation (USDOT)]
(https://www.transportation.gov/policy/aviation-policy/domestic-airline-consumer-airfare-report)
* **Access Note:** For reproducibility, ensure you download the periods corresponding to the 1996-2024 timeframe as specified in the methodology.

If you are using the pre-processed version for replication, please refer to the `datasets/processed/` directory in this repository, which contains the foundational data required to run the notebooks.


## 📂 Project Structure
* `datasets/processed/`: Contains the cleaned `base_df.csv` and `final_df.csv` used for modeling.
* `notebooks/`:
    * `01_EDA.ipynb`: Exploratory data analysis and feature correlation.
    * `02_Traditional_ML.ipynb`: Predictive modeling and baseline performance.
    * `03_Causal.ipynb`: Primary causal estimation using DML, Causal Forests, and refutation tests.
* `outputs/`: High-resolution (500 DPI) PDF visualizations of SHAP values, causal graphs, and sensitivity heatmaps.

## 🛠 Methodology
We utilize a **LinearDML** framework with Gradient Boosting Regressors to handle nuisance models for both treatment (Fare) and outcome (Passengers). 

### Hyperparameter Tuning
To prevent overfitting and ensure the stability of heterogeneous treatment effects, we performed 5-fold cross-validation on the Causal Forest parameters. 
Detailed search spaces for leaf size, tree depth, and pruning are documented in **Table C.2** of the manuscript appendix.

## 🚩 Limitations
As detailed in the manuscript, this study utilizes a pooled estimation approach. While we control for temporal shocks (e.g., Year, Quarter, Major Events), the model does not formally exploit a dynamic panel structure. Future work should explore within-route variations to further validate these causal mechanisms.

## © License
This project is licensed under the MIT License.
