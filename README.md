# India Air Quality Analysis (2017-2020)
Comprehensive analysis of air pollution in India using Python (Pandas/Seaborn). Includes EDA of seasonal &amp; diurnal cycles and a predictive Random Forest pipeline (R²=0.81). Key findings highlight the dominant predictive power of PM10 over VOCs and the potential for "virtual sensors" to bridge historical data gaps in urban monitoring.
India Air Quality Analysis (2017-2020)

# Project Overview

This project provides a comprehensive analysis of air quality across multiple Indian cities between 2017 and 2020. By leveraging Exploratory Data Analysis (EDA) and Machine Learning, the study identifies critical pollution patterns and builds a high-accuracy predictive pipeline for PM2.5 levels.

# Key Objectives:

* Temporal Analysis: Identify diurnal and seasonal cycles in urban pollution.

* Predictive Modeling: Evaluate the relationship between gaseous pollutants and particulate matter.

* Feature Optimization: Determine the most efficient predictors for PM2.5 to minimize model complexity.

# Data Source

The data used in this project is sourced from the Air Quality Data in India (2015 - 2020) dataset available on Kaggle.

* Dataset Link: [Air Quality Data in India (Kaggle)](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india/data?select=stations.csv)

* Instructions: To run the notebooks in this repository, download the CSV files from the link above and place them in a local folder named data/. Due to GitHub's file size limitations, the raw data files are excluded from this repository via .gitignore.

# Key Findings

1. The "Virtual Sensor" Potential

We developed a Random Forest Regression model (Model V4) that achieved an R-squared of 0.814. This high accuracy suggests the model could function as a "virtual sensor," predicting PM2.5 levels at monitoring stations where physical sensors may have failed, thus preventing critical data gaps.

2. PM10 vs. VOC Redundancy

A major insight of this study was the evaluation of Volatile Organic Compounds (VOCs) like Benzene, Toluene, and Xylene.

* Without PM10: Adding VOCs to a gas-only model improved R² from 0.51 to 0.64.

* With PM10: Adding VOCs only improved the model from 0.797 to 0.814.
* Conclusion: VOCs and PM10 are largely redundant signals. For an efficient monitoring system, PM10 is the single most dominant and necessary predictor.

3. Diurnal & Seasonal Trends

EDA confirmed that pollution levels follow a strict diurnal cycle, peaking during morning and evening rush hours. Furthermore, the analysis proved that the seasonal monsoon cycle has a massive, natural "cleansing" effect on urban pollutants.

# Technical Stack

* Language: Python 3.8+

* Data Manipulation: Pandas, NumPy

* Visualization: Matplotlib, Seaborn

* Machine Learning: Scikit-Learn (Random Forest, Decision Tree)

* Metrics: R-squared, MSE, RMSE, Confusion Matrix

# Model Performance Summary

| Model | Features | R-squared / Error % | Interpretation |
| ----- | -------- | --------- | -------------- |
| V1    | Basic Gases + VOCs | 0.64 | Strong gas-only baseline. |
| V2    | Basic Gases + PM10 |  0.79  | High efficiency, PM10 is the key predictor |
| V3    | All Pollutants | 0.81 | The "All-In" model; confirms redundancy|
| Classifier | All Pollutants | 66.7% | High accuracy in identifying AQI Buckets |

# Future Work

The primary limitation identified was the lack of real-time weather data. Future iterations will aim to merge this dataset with historical wind speed, humidity, and temperature data to account for the ~19% of variance currently unexplained by pollutant concentrations alone.

# Repository Structure

* notebooks/: Contains the consolidated Jupyter Notebook with EDA and ML pipelines.

* visualizations/: Exported plots including Correlation Heatmaps and Confusion Matrices.

* requirements.txt: List of dependencies required to reproduce the environment.
