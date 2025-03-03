# Energy Efficiency Analysis with XGBoost - CUSP 2025

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains three Jupyter notebooks that leverage XGBoost and Linear regression models to analyze factors affecting energy efficiency in households, which is a project for London CUSP 2025. The analysis focuses on heating systems, ownership types, and a comprehensive evaluation including advanced modeling and visualization techniques. The goal is to identify key drivers of energy efficiency and provide insights that could inform strategies to improve energy efficency using related policies.

## Notebooks
### Linear Regression Models

### 1. Energy Efficiency vs. Total Median Annual Household Income

- **Description**: This analysis examines the linear relationship between energy efficiency ratings and total median annual household income.
- **Dataset**: `all_final_data_2011.csv`
- **Results**:
  - **Intercept**: 68.303
  - **Coefficient**: -0.000152
  - **Pearson Correlation Coefficient (r)**: -0.342
  - **R² (Coefficient of Determination)**: 0.117
  - **Mean Squared Error (MSE)**: 22.923
- **Visualization**: Scatter plot with regression line.

### 2. Energy Efficiency vs. Fuel Poverty (2017 Data)

- **Description**: This analysis explores the linear relationship between energy efficiency and fuel poverty levels in 2017.
- **Dataset**: `all_final_data_2011.csv`
- **Results**:
  - **Intercept**: 66.0
  - **Coefficient**: -0.261
  - **Pearson Correlation Coefficient (r)**: -0.208
  - **R² (Coefficient of Determination)**: 0.043
  - **Mean Squared Error (MSE)**: 24.849
- **Visualization**: Scatter plot with regression line.

### 3. Building Age vs. Total Median Annual Household Income

- **Description**: This analysis investigates the linear relationship between building age and total median annual household income.
- **Dataset**: `all_final_data_2011.csv`
- **Results**:
  - **Intercept**: 202,054.03
  - **Coefficient**: -85.878
  - **Pearson Correlation Coefficient (r)**: -0.251
  - **R² (Coefficient of Determination)**: 0.063
  - **Mean Squared Error (MSE)**: 123,008,798.90
- **Visualization**: Scatter plot with regression line.
- **Note that because of the data is discrete and not continous, it would be hard to visualise it using linear regression for this type of correlation**

### XGB Models

#### 1. Heating Data Analysis (`Heating_Data_Analysis.ipynb`)

- **Description**: This notebook analyzes the impact of various heating systems (e.g., gas, electric, oil) on energy efficiency. It includes:
  - Data loading from `all_final_data_2011.csv`.
  - Feature selection focusing on heating-related columns.
  - Training an XGBoost regression model.
  - Visualization of feature importance as a bar chart.
  - Calculation of a weighted "Heating Score" for each Lower Super Output Area (LSOA).

#### 2. Ownership Data Analysis (`Ownership_Data_Analysis.ipynb`)

- **Description**: This notebook examines how different ownership types (e.g., owned outright, rented) influence energy efficiency. It involves:
  - Data loading from `all_final_data_2011.csv`.
  - Feature selection targeting ownership-related columns.
  - Training an XGBoost regression model.
  - Visualization of feature importance as a bar chart.
  - Calculation of a weighted "Ownership Score" for each LSOA.

#### 3. Comprehensive XGBoost Analysis (`Comprehensive_XGBoost_Analysis.ipynb`)

- **Description**: This notebook provides an in-depth analysis pipeline with advanced features:
  - Data loading from `all_final_data_2011.csv`.
  - Optimal model selection through cross-validation to determine the best number of boosting rounds.
  - Training an XGBoost model with a broader set of features (e.g., income, fuel poverty, year built, heating, and ownership scores).
  - Advanced visualizations including decision trees (rendered as high-resolution PNGs) and feature importance bar charts.
  - A commented-out section for grid search to find the best hyperparameters (can be uncommented and customized).
  - Evaluation across multiple test sizes and random states to identify the best-performing model configuration.

## Installation

To run these notebooks, install the required Python packages using pip:

```bash
pip install xgboost polars numpy scikit-learn matplotlib graphviz shap jupyter
```

## Usage

### Clone the Repository:
```bash
git clone https://github.com/yourusername/energy-efficiency-xgboost.git
cd energy-efficiency-xgboost
```

### Prepare the Data:
Place the dataset all_final_data_2011.csv in the repository's root directory. This file is not included in the repository and must be sourced separately.

### Run the Notebook
- Open the desired notebook (Heating_Data_Analysis.ipynb, Ownership_Data_Analysis.ipynb, or Comprehensive_XGBoost_Analysis.ipynb).
- Execute the cells in sequence. Note: The feature columns used in each notebook are specified within the code. Ensure the dataset contains these columns or adjust the code accordingly.

## Data
The analysis relies on a dataset (all_final_data_2011.csv) containing household data with the following columns:
- **LSOA**: Lower Super Output Area identifier.
- **Mean_Household_Income**: Average household income.
- **Energy Efficiency: Energy efficiency rating (target variable)**.
- **Fuel Poverty**: Fuel poverty indicator.
- **Heating-related features**: No central heating, Gas, Electric, Oil, Solid fuel, Other including communal and renewable, Two or more types.
- **Ownership-related features**: Owned outright, Owned with a mortgage or loan, Shared ownership, Rented from Local Authority, Other social rented, Private landlord or letting agency, Other private rented, Rent free.
- **Additional features**: 1 bedroom, 2 bedrooms, 3 bedrooms, 4 or more bedrooms, Year_built.

## Results
The notebooks produce the following outputs:

- **Feature Importance Plots**: Bar charts showing the relative importance of each feature (heating or ownership) in predicting energy efficiency, with normalized percentages.
- **Decision Tree Visualizations** (Comprehensive notebook only): High-resolution PNG images of XGBoost decision trees, illustrating the model's decision-making process.
- **Weighted Scores**: CSV output (output_with_scores.csv) from the Heating and Ownership notebooks, including calculated "Heating Score" and "Ownership Score" for each LSOA.
- **Performance Metrics**: RMSE, MSE, and R² scores for model evaluation, with the Comprehensive notebook identifying the best configuration (e.g., test size **0.1**, random state **36**, achieving an R² of **0.6366**).