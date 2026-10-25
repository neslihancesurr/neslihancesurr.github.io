---
layout: page
title: Housing Price Prediction
description: Predicting apartment prices in Istanbul using real-estate listing data and machine learning
img: assets/img/regression.jpeg
importance: 4
category: work
related_publications: false
---

This machine learning project investigates **apartment price prediction in Istanbul** using real-estate listing data collected from [Hepsiemlak](https://www.hepsiemlak.com/). It explores how property characteristics, including location, floor area, room count, and building age, relate to listing prices and how these features can be used to estimate property values.

The project combines data cleaning, exploratory data analysis, feature analysis, and predictive modeling in a series of Jupyter notebooks.

**[View the Project on GitHub](https://github.com/neslihancesurr/housing-models)**

## Data Collection & Preprocessing

The project uses apartment listing data stored in JSON format. The raw dataset, `novemberdata.json`, contains property information collected from Hepsiemlak, while `cleaned_data_model.json` contains the processed data used for modeling.

The preprocessing pipeline focuses on transforming raw listing attributes into usable numerical features.

1. **Data Inspection:** Examine the structure and quality of the collected property data.
2. **Data Cleaning:** Convert prices, floor areas, room counts, and other attributes into usable formats.
3. **Outlier Handling:** Identify and handle invalid values and outliers that may affect model performance.
4. **Feature Preparation:** Produce a cleaned dataset suitable for exploratory analysis and regression modeling.

## Exploratory Data Analysis

The `emlak-correlations.ipynb` notebook investigates relationships between property attributes and listing prices using statistical analysis and visualizations.

The analysis explores how factors such as apartment size, room count, building age, and location relate to price, helping identify potentially informative features for predictive modeling.

## Machine Learning Models

The project implements and compares two regression approaches using scikit-learn.

### Linear Regression

The `emlak-linear.ipynb` notebook develops a linear regression model to estimate apartment prices from the prepared property features. Cross-validation is used to assess model performance, and an example demonstrates how the trained model can generate price predictions.

### Random Forest Regression

The `emlak-randomforest.ipynb` notebook applies random forest regression to the same prediction task. This tree-based ensemble approach can capture nonlinear relationships and interactions between property attributes that a linear model may not represent adequately.

Both approaches are evaluated using validation metrics, including **Mean Absolute Error (MAE)** and **Normalized Absolute Error (NAE)**.

## Project Workflow

The notebooks are organized into a sequential workflow:

1. `emlak-data-cleaning.ipynb` — data preprocessing and feature preparation.
2. `emlak-correlations.ipynb` — exploratory data analysis and correlation visualizations.
3. `emlak-linear.ipynb` — linear regression and cross-validation.
4. `emlak-randomforest.ipynb` — random forest regression and cross-validation.

## Technologies

**Python · Jupyter Notebook · pandas · NumPy · scikit-learn · Matplotlib · Seaborn · Machine Learning · Regression Analysis**

This project demonstrates an end-to-end workflow for **tabular machine learning**, from preparing real-world data to exploring feature relationships and comparing predictive models. It also provides a foundation for further work on feature engineering, model evaluation, and data-driven analysis of the Istanbul housing market.
