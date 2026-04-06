# The Rent is Too High: A Big Data Analysis of Interstate Migration

## 1. Executive Summary
Does the cost of housing drive people to leave their states? Using a massive dataset of **25.2 million records** from the 2010 American Community Survey (IPUMS USA), this project quantifies the "push factor" of housing costs. 

Through **Weighted Least Squares (WLS)** regression, I found that higher housing costs are a statistically significant driver of interstate migration ($p < 0.001$), even when controlling for income, age, and tenure (renting vs. owning).

## 2. The Dataset
* **Source:** IPUMS USA (ACS 2010 1-Year Sample).
* **Scope:** 25,250,913 individual observations.
* **Key Variables:**
    * `moved_states`: (Dependent Variable) 1 if moved to a different state in the last year.
    * `total_housing_cost`: Combined rent/mortgage and monthly utility costs.
    * `perwt`: Person-level weights to ensure national representativeness.

## 3. Methodology
To prepare the data for econometric analysis, several high-level data engineering steps were taken:
* **Feature Engineering:** Unified disparate variables (Rent, House Value, Utilities) into a single monthly housing cost metric.
* **Log-Transformation:** Applied $ln(x+1)$ to Income and Rent to normalize skewed distributions and interpret results as elasticities.
* **Handling Survey Weights:** Employed **Weighted Least Squares (WLS)** to ensure the model reflects the actual U.S. population rather than just the raw sample.
* **Data Cleaning:** Removed observations for individuals under 18 and handled top-coded financial values.



## 4. Key Findings & Regression Results

### The Regression Model
The model predicts the probability of moving states ($Y$) based on housing costs ($X_1$) and demographic controls ($X_i$):

$$P(\text{Move}) = \beta_0 + \beta_1\ln(\text{Rent}) + \beta_2\ln(\text{Income}) + \beta_3(\text{Age}) + \dots + \epsilon$$

### Interpretations:
| Predictor | Coefficient | Impact on Migration |
| :--- | :--- | :--- |
| **Housing Cost (ln_rent)** | **+0.0035** | **Push Factor:** Higher costs significantly increase the probability of leaving the state. |
| **Renter Status** | **+0.0294** | **Mobility:** Renters are ~3% more likely to move than owners (the strongest predictor). |
| **Age** | **-0.0004** | **Inertia:** Each year of age decreases the likelihood of interstate moving. |
| **Income (ln_income)** | **+0.0004** | **Resource:** Higher income provides the "liquidity" needed to fund a long-distance move. |

## 5. Technical Stack
* **Stata:** Initial data cleaning, variable construction, and `.dta` file management.
* **Python (Pandas/NumPy):** Data type optimization and memory-efficient processing of 25M+ rows.
* **Statsmodels:** Weighted Least Squares (WLS) regression and statistical inference.
* **Matplotlib/Seaborn:** Data visualization and binned scatter plots.



## 6. How to Run
1. Ensure you have the `migration_data.csv` (or the cleaned `.dta` file).
2. Install dependencies: `pip install pandas statsmodels matplotlib numpy`.
3. Run the Jupyter Notebook `migration_analysis.ipynb` to replicate the regression and charts.

---
**Project Author:** Dang Vu Tuyet Ngan  
**Field:** Data Science / Applied Economics
