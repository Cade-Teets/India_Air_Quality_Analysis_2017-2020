# India Air Quality Analysis (2017-2020)
Comprehensive analysis of air pollution in India using Python (Pandas/Seaborn). Includes EDA of seasonal &amp; diurnal cycles and a predictive Random Forest pipeline (R²=0.81). Key findings highlight the dominant predictive power of PM10 over VOCs and the potential for "virtual sensors" to bridge historical data gaps in urban monitoring.
India Air Quality Analysis (2017-2020)

# Data Source

The data used in this project is sourced from the Air Quality Data in India (2015 - 2020) dataset available on Kaggle.

* Dataset Link: [Air Quality Data in India (Kaggle)](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india/data?select=stations.csv)

* Instructions: To run the notebooks in this repository, download the CSV files from the link above and place them in a local folder named data/. Due to GitHub's file size limitations, the raw data files are excluded from this repository via .gitignore.

# Repository Structure

* notebooks/: Contains the consolidated Jupyter Notebook with EDA and ML pipelines.

* visualizations/: Exported plots including Correlation Heatmaps and Confusion Matrices.

* requirements.txt: List of dependencies required to reproduce the environment.

# Project Overview

This project provides a comprehensive analysis of air quality across multiple Indian cities between 2017 and 2020. By leveraging Exploratory Data Analysis (EDA) and Machine Learning, the study identifies critical pollution patterns and builds a high-accuracy predictive pipeline for PM2.5 levels.

# Key Objectives:

* Temporal Analysis: Identify diurnal and seasonal cycles in urban pollution.

* Predictive Modeling: Evaluate the relationship between gaseous pollutants and particulate matter.

* Feature Optimization: Determine the most efficient predictors for PM2.5 to minimize model complexity.

# Key Findings

1. **The "Virtual Sensor" Potential**

I developed a Random Forest Regression model (Model V4) that achieved an R-squared of 0.814. This high accuracy suggests the model could function as a "virtual sensor," predicting PM2.5 levels at monitoring stations where physical sensors may have failed, thus preventing critical data gaps.

2. **PM10 vs. VOC Redundancy**

My analysis revealed that while VOCs (Benzene, Toluene, Xylene) help predict PM2.5 in the absence of other data, they become statistically redundant once PM10 is included in the model.

* Without PM10: Adding VOCs to a gas-only model improved R² from 0.51 to 0.64.

* With PM10: Adding VOCs only improved the model from 0.797 to 0.814.
* Conclusion: VOCs and PM10 are largely redundant signals. For an efficient monitoring system, PM10 is the single most dominant and necessary predictor.

3. **Diurnal & Seasonal Trends**

EDA confirmed that pollution levels follow a strict diurnal cycle, peaking during morning and evening rush hours. Furthermore, the analysis proved that the seasonal monsoon cycle has a massive effect on reducing urban pollutants.

4. **The 11:00 AM CO Divergence**

Discovered a secondary Carbon Monoxide peak at 11:00 AM, diverging from $NO_2$ and $PM_{2.5}$ trends. This identifies CO as a critical marker for heavy commercial vehicle traffic following morning restriction lifts.

# Machine Learning & Discussion

The modeling process was iterative, moving from simple gaseous baselines to complex ensemble models to identify the most efficient predictors for PM2.5.

1. **Regression (Predicting PM2.5)**

I utilized a Random Forest Regressor across four iterations to test the impact of different chemical markers:

* Model V1 (Basic Gases Only): Using NO2, CO, SO2, O3, and NH3, I achieved an R² of 0.51. Carbon Monoxide (CO) was identified as the strongest individual gaseous predictor.

* Model V2 (Gases + VOCs): Adding Volatile Organic Compounds (Benzene, Toluene, Xylene) pushed the R² to 0.64. This 25% improvement confirms that VOCs provide a unique predictive signal not captured by standard combustion gases.

* Model V3 (Gases + PM10): Adding PM10 resulted in a massive leap to R² of 0.797. As PM2.5 is physically a subset of PM10, this feature acts as the "missing link" for high-accuracy modeling.

* Model V4 (The "All-In" Model): Including all available features resulted in a final R² of 0.814.

**The Redundancy Insight:** While V4 is technically the most accurate, the marginal gain over V3 (only 0.017) proves that once PM10 is included, the VOC signal becomes redundant. For real-world deployment, Model V3 offers the best balance of simplicity and accuracy.

2. **Classification (AQI Health Buckets)**

I compared a baseline Decision Tree against an ensemble Random Forest to predict health categories.

* **Decision Tree (Interpretability):**  Achieved ~66.7% accuracy. Useful for visualizing the "logic" of a split, though it struggled with precision on category boundaries.

* **Random Forest (Performance):** Achieved an improved ~70.5% accuracy and reduced "neighbor confusion" by 150+ instances in the Moderate/Satisfactory categories and better at classifying Poor catagory.

* **Safety:** Both models made zero "catastrophic errors" (confusing 'Good' with 'Severe'), making them reliable for public health advisories.

# Regression Model Performance Summary (PM2.5)

| Model | Features | R-squared | RMSM ($$\mu g/m^3$$) | Interpretation |
| ----- | -------- | --------- | -------------- | ----- |
| V1    | Basic Gases | 0.51 | 32.27 | Simple yet incomplete model |
| V2    | Basic Gases + VOCs | 0.64 | 27.71 |Strong gas-only baseline. |
| V3    | Basic Gases + PM10 | 0.79 | 20.88 | High efficiency, PM10 is the key predictor |
| V4    | All Pollutants | 0.81 | 19.96 | The model confirms the VOC redundancy |

# Classification Model Performance Summary (AQI Buckets)

| Model | Technique | Accuracy | Interpretation |
| ----- | -------- | --------- | -------------- |
| Baseline | Decision Tree | 66.7% | High interpretability (Visualization) |
| Ensemble | Random Forest | 70.5% | Higher precision in Moderate/Satisfactory, Poor |


# Future Work

The primary limitation identified was the lack of real-time weather data. Further improvements will aim to merge this dataset with historical wind speed, humidity, and temperature data to account for the ~19% of variance currently unexplained by pollutant concentrations alone.

# Technical Stack

* Language: Python 3.8+

* Data Manipulation: Pandas, NumPy

* Visualization: Matplotlib, Seaborn

* Machine Learning: Scikit-Learn (Random Forest, Decision Tree)

* Metrics: R-squared, MSE, RMSE, Confusion Matrix, Skewness Analysis
