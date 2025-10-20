# Linear Regression for Weather Data

This repository contains a Jupyter Notebook that implements various linear regression models to predict **Mean Temperature (`MeanTemp`)** using historical weather summary data.

The core analysis is performed in the following file:
* `Linear Regression.ipynb`

## Project Overview

The main objective of this project is to apply and evaluate the performance of three different regression models on a weather dataset:
1.  **Simple Linear Regression**
2.  **Lasso Regression**
3.  **Ridge Regression**

## Dataset and Preprocessing Highlights

The project utilizes the `Summary of Weather.csv` dataset, which required extensive cleaning due to mixed data types and significant missing values. The following preprocessing steps were critical:

* **Initial Data Cleaning:** Columns consisting entirely of `NaN` values were removed.
* **Data Type Handling:** Non-numeric markers like `'T'` (Trace precipitation) in `Precip` and `PRCP`, and `'#VALUE!'` in `Snowfall`, were replaced with `NaN`.
* **Type Conversion:** The `Date` column was converted to `datetime`, and the relevant weather columns (`Precip`, `Snowfall`, `SNF`, `PRCP`) were converted to the `float` type.
* **Missing Value Imputation:**
    * `Precip`'s missing values were filled with the column's mean.
    * `PRCP`'s missing values were filled with the column's minimum value.
    * Rows with remaining `NaN` values in `MAX`, `MIN`, and `MEA` were dropped to ensure a complete dataset for the final model training.
* **Feature Selection:** Several columns, including highly correlated temperature data and redundant date/measurement fields (`MAX`, `MIN`, `MEA`, `YR`, `MO`, `DA`, `PRCP`, `SNF`), were dropped after correlation analysis.

## Model Performance

The cleaned data was split into training (75%) and testing (25%) sets, and independent features were scaled using `StandardScaler`. The models were evaluated using **Mean Absolute Error (MAE)**, **Mean Squared Error (MSE)**, and the **R-squared ($R^2$) Score**.

| Model | MAE | MSE | $R^2$ Score |
| :--- | :--- | :--- | :--- |
| **Linear Regression** | $0.14927$ | $0.06410$ | $0.99885$ |
| **Lasso Regression** | $0.73853$ | $1.08566$ | $0.98065$ |
| **Ridge Regression** | $0.14927$ | $0.06410$ | $0.99885$ |

**Conclusion:** Both the standard Linear Regression and the penalized Ridge Regression achieved an exceptionally high $R^2$ score ($> 0.998$), indicating a near-perfect fit for predicting the mean temperature based on the selected features.

## Technologies and Libraries

* **Python 3**
* **pandas** (Data manipulation and cleaning)
* **numpy** (Numerical operations)
* **seaborn** & **matplotlib** (Data visualization, including correlation heatmap)
* **scikit-learn (`sklearn`)**:
    * `LinearRegression`, `Lasso`, `Ridge` (Model implementation)
    * `StandardScaler` (Feature scaling)
    * `train_test_split` (Data splitting)
    * `mean_absolute_error`, `mean_squared_error`, `r2_score` (Model evaluation)
