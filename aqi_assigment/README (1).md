# Air Quality Historical Data Analysis and AQI Calculation

## Project Overview

This project analyzes historical air quality data using Python,Pandas and numpy. The project performs data preprocessing, missing-value handling, pollutant analysis, AQI calculation for different pollutants, and AQI category classification.

## Dataset Description

The dataset used in this project is `air_quality_historical.csv`.

It contains **1,298 records and 12 columns**.

### Dataset Columns

| Column                  | Description                         |
| ----------------------- | ----------------------------------- |
| `date`                  | Date of the air quality observation |
| `pm10`                  | PM10 pollutant concentration        |
| `pm2_5`                 | PM2.5 pollutant concentration       |
| `carbon_monoxide`       | Carbon monoxide concentration       |
| `nitrogen_dioxide`      | Nitrogen dioxide concentration      |
| `sulphur_dioxide`       | Sulphur dioxide concentration       |
| `ozone`                 | Ozone concentration                 |
| `aerosol_optical_depth` | Aerosol optical depth               |
| `dust`                  | Dust measurement                    |
| `uv_index`              | UV index                            |
| `us_aqi`                | US Air Quality Index                |
| `european_aqi`          | European Air Quality Index          |

## Technologies Used

* Python
* Pandas
* NumPy

## Project Workflow

### 1. Loading the Dataset

The dataset is loaded using Pandas:

```python
import pandas as pd
df = pd.read_csv("air_quality_historical.csv")
```

### 2. Dataset Exploration

The notebook examines:

* Dataset shape
* Column names
* Data types
* Missing values
* Duplicate rows
* Initial records

### 3. Date Conversion

The `date` column is converted into Pandas datetime format for proper date handling.

```python
df['date'] = pd.to_datetime(df['date'])
```

### 4. Missing Value Handling

The project checks missing values in the pollutant columns.

The main pollutant columns are:

* PM10
* PM2.5
* Carbon Monoxide
* Nitrogen Dioxide
* Sulphur Dioxide
* Ozone

Missing pollutant values are handled using **interpolation**, followed by forward-fill and backward-fill where required.

```python
df[pollutant_columns] = df[pollutant_columns].interpolate()
df[pollutant_columns] = df[pollutant_columns].ffill().bfill()
```

### 5. Negative Value Check

The notebook checks whether any pollutant contains negative values.

### 6. AQI Calculation

The project calculates AQI values for:

* PM2.5
* PM10
* Carbon Monoxide
* Nitrogen Dioxide
* Sulphur Dioxide
* Ozone

AQI breakpoint ranges are defined for each pollutant, and a common `calculate_aqi()` function is used to calculate the AQI value based on the corresponding concentration.

### 7. Unit Conversion

For Nitrogen Dioxide, Sulphur Dioxide, and Ozone, concentration values are converted to ppb before calculating their AQI.

Carbon monoxide is converted to ppm before its AQI calculation.

### 8. Overall AQI

The calculated AQI values of the different pollutants are compared, and the maximum pollutant AQI is used as the `calculated_aqi`.

```python
df['calculated_aqi'] = df[aqi_columns].max(axis=1)
```

### 9. AQI Classification

The calculated AQI is classified into categories:

| AQI Range | Category    |
| --------: | ----------- |
|      0–50 | Good        |
|    51–100 | Moderate    |
|   101–150 | Poor        |
|   151–200 | Severe      |
| Above 200 | Very Severe |

## Project Files

```text
├── air_quality_historical.csv
├── Ai Assigment1.ipynb
└── README.md
```

### air_quality_historical.csv

Contains the historical air quality measurements used for the analysis.

### Ai Assigment1.ipynb

Contains the complete Python implementation for data loading, preprocessing, pollutant analysis, AQI calculation, and AQI classification.

### README.md

Contains the documentation and description of the project.

## Conclusion

This project demonstrates the use of Python,Pandas and numpy  for processing historical air quality data. It handles missing values, checks data quality, calculates AQI values for major pollutants, determines the overall calculated AQI, and classifies air quality into different categories.
