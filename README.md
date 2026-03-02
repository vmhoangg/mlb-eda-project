![GitHub repo size](https://img.shields.io/github/repo-size/vmhoangg/mlb-eda-project)
![GitHub stars](https://img.shields.io/github/stars/vmhoangg/mlb-eda-project?style=social)

# MLB Exploratory Data Analysis (EDA)

## Business Objective
This project explores the determinants of player salary and on-field performance using a dataset of Major League Baseball (MLB) player statistics.

The analysis aims to:
- Identify performance metrics associated with higher salaries
- Examine whether player position and race are statistically associated
- Compare mean salaries across meaningful player subsets
- Build and interpret a regression model to explain variation in a selected performance outcome (career triples)

## Dataset
- **Observations:** 352 players  
- **Features:** 21 variables  
- **Key variables:** salary, player_position, race, team_payroll, years_played, games_played, and multiple career performance metrics  
- **Missing values:** City demographic percentages had missing values and were handled via mean imputation.

## Technical Workflow
1. **Data loading & inspection** (shape, dtypes, summary statistics)
2. **Missing data handling** (identify missingness and apply mean imputation)
3. **Exploratory analysis**
   - Univariate distributions (histograms/KDE)
   - Bivariate relationships (scatter + trend line)
   - Categorical vs continuous comparisons (boxplots)
   - Multivariate visualization (semantic mapping with hue)
4. **Statistical testing**
   - Chi-square test of independence (player position × race)
   - Independent t-test (salary differences between defined subsets)
5. **Modeling**
   - OLS regression (statsmodels)
   - Backward elimination to refine predictors
   - Interpretation of coefficients, significance, and overall fit

## Key Findings
- Many performance variables show **right-skewed distributions**, reflecting a small number of elite, high-performing players.
- There is a **strong positive linear relationship** between **career at-bats** and **career hits**, indicating that greater playing opportunity is strongly associated with cumulative hits.
- **Player salaries differ by position**: positions such as first base, outfield, and third base tend to have higher salary distributions than catcher and second base.
- The **Chi-square test indicates a statistically significant association** between **player position and race** (p < 0.05).
- The **t-test comparison** between selected subsets (e.g., first base vs outfield with >100 home runs) did **not** find a statistically significant salary difference (p > 0.05).

## Model Interpretation (OLS Regression)
A refined OLS model was fitted to predict **career triples** using selected performance predictors.

- **Adjusted R² ≈ 0.74**, meaning the model explains ~74% of the variance in career triples.
- Significant predictors (p < 0.001):
  - **career_hits**
  - **career_runs**
- A non-significant predictor (e.g., **years_played**) was removed during backward elimination to improve parsimony.

## Statistical Assumptions
The regression analysis relies on standard OLS assumptions:
- **Linearity** between predictors and target
- **Independence** of residuals (Durbin–Watson ≈ 2 suggests no strong autocorrelation)
- **Homoscedasticity** (constant variance of errors)
- **Normality** of residuals (may be imperfect due to skewed variables)
- **Low multicollinearity** (a high condition number suggests potential collinearity risk)

## Limitations
- The dataset is **cross-sectional** and limited in size (**n = 352**).
- Some demographic variables required **mean imputation**, which can reduce variance and bias relationships.
- Many career performance metrics are **highly correlated**, which may introduce multicollinearity in regression.
- Salary may be influenced by **external factors not captured** here (contracts, injuries, marketability, team strategy).

## How to Run
### 1) Install dependencies
```bash
pip install -r requirements.txt
