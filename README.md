# Sales Forecasting Using Facebook Prophet

## Project Overview
Sales forecasting helps businesses estimate future demand using historical sales patterns. In this project, historical sales data from **1,115 stores** is analyzed to build a time-series forecasting solution using **Facebook Prophet**.

The main objective is to forecast future daily sales for individual stores by learning patterns from historical sales data, including time-based trends, weekly/yearly seasonality, and holiday effects.

## Business Problem

Retail businesses need reliable sales forecasts for planning inventory, staffing, promotions, and other operational activities.

This project addresses the following business question:

> **Based on historical sales data, how can we forecast future daily sales for a store?**

The project uses the Rossmann Store Sales dataset, where daily sales information is available for 1,115 stores.

## Dataset

The project uses the **Rossmann Store Sales** dataset.

### Sales Dataset

The training dataset contains **1,017,209 records** with the following key fields:

| Column | Description |
|---|---|
| `Store` | Unique store ID |
| `DayOfWeek` | Day of the week |
| `Date` | Sales date |
| `Sales` | Daily sales — target variable |
| `Customers` | Number of customers |
| `Open` | Whether the store was open |
| `Promo` | Whether a promotion was running |
| `StateHoliday` | State/public holiday indicator |
| `SchoolHoliday` | School holiday indicator |

### Store Dataset

Additional store-level information is available for **1,115 stores**, including:

- Store type
- Assortment level
- Competition distance
- Competition opening information
- Promo2 participation
- Promo2 start week/year
- Promo2 interval

## Project Workflow

The project follows these major steps:

1. Load the sales and store datasets.
2. Perform exploratory data analysis.
3. Check data types and missing values.
4. Remove records for stores that were closed.
5. Handle missing values in store information.
6. Merge sales data with store-level information.
7. Analyze correlations between numerical variables.
8. Extract year, month, and day from the date.
9. Analyze sales patterns by:
   - Month
   - Day of month
   - Day of week
   - Store type
   - Promotion
10. Build a time-series forecasting model using Facebook Prophet.
11. Add school and state holiday dates to the forecasting model.
12. Generate future sales forecasts for a selected store.

## Data Preparation

The notebook identifies **844,392 open-store observations** and **172,817 closed-store observations**.

Since sales forecasting is focused on operating stores, closed-store records are removed from the modeling dataset.

Missing values in the store information are handled as follows:

- Missing competition opening month/year and Promo2-related fields are filled with `0`.
- Missing `CompetitionDistance` values are replaced with the mean competition distance.

The cleaned sales data is then merged with store information using the `Store` column.

## Exploratory Data Analysis

The analysis examines several important sales patterns.

### Time-Based Analysis

Sales and customer trends are analyzed across:

- Months
- Days of the month
- Days of the week
- Store types

The project also examines the relationship between sales and customer counts.

### Promotion Analysis

Sales and customer distributions are compared for days with and without promotions using bar plots and violin plots.

### Correlation Analysis

A correlation matrix is created to understand relationships between numerical variables and the target variable `Sales`.

The notebook notes a positive relationship between **Customers**, **Promo**, and **Sales**.

## Facebook Prophet

**Facebook Prophet** is used as the primary forecasting model.

Prophet is a time-series forecasting procedure based on an additive model that can capture:

- Trend
- Yearly seasonality
- Weekly seasonality
- Holiday effects

The project first creates a basic Prophet model and then extends the model by incorporating holiday information.

### Forecasting Process

For a selected store:

1. Filter the dataset for the required store.
2. Keep `Date` and `Sales`.
3. Rename the columns to Prophet's required format:
   - `Date` → `ds`
   - `Sales` → `y`
4. Sort the data by date.
5. Train the Prophet model.
6. Create future dates using `make_future_dataframe()`.
7. Generate predictions using `model.predict()`.
8. Visualize the forecast and its components.

A reusable `sales_pred()` function is created to generate forecasts for a selected store and forecast period.

## Holiday Effects

The project prepares holiday information from:

- School holidays
- State holidays

These dates are combined and provided to Prophet so that holiday effects can be considered during forecasting.

The notebook demonstrates forecasting for a selected store using a **90-day forecast period** with holiday information.

## Technologies Used

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Facebook Prophet**
- **Jupyter Notebook**

## Repository Structure

```text
Sales_Department/
│
├── Sales_Department.ipynb
├── sales_slides.pptx
├── README.md
├── train.csv
|── store.csv
