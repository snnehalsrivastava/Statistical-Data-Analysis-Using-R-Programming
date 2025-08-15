# Statistical Data Analysis using R: Property Sales Prediction

## Overview

This project involves a **statistical data analysis** using **R** on a historical dataset of property sales. The primary aim is to identify key characteristics of the data, develop predictive models for property sale prices, and classify properties based on the presence of a fireplace.

## Project Objectives

The project addresses three main objectives:

*   **1. Exploratory Data Analysis (EDA)**: Conduct a thorough investigation of the property sales dataset by generating plots and summary statistics. The goal is to identify key data characteristics and interpret these statistical observations within the business context of property sales, providing insights into variables like `MSZoning`, `LotArea`, `BldgType`, `HouseStyle`, `OverallQual`, `OverallCond`, `YearBuilt`, `CentralAir`, `GrLivArea`, `FullBath`, `HalfBath`, `BedroomAbvGr`, `KitchenAbvGr`, `KitchenQual`, `Fireplace`, `GarageArea`, `SaleCondition`, and the target variable `SalePrice`.
*   **2. Regression Model Development**: Build a regression model to **predict `SalePrice`** using one or more variables from the dataset. This involves discussing the methodology, including variable selection (e.g., identifying and eliminating confounding variables like `GarageArea`, `BldgType`, `HouseStyle`, `KitchenQual`, and `SaleCondition`), assessing goodness of fit (e.g., Multiple R-squared values), and evaluating model performance. Both linear and potentially nonlinear models are considered.
*   **3. Classification Model Development**: Create a classification model to **predict whether a property has a fireplace** (`Fireplace=Y,N`). This task involves exploring various subsets of predictors (such as `OverallQual`, `BedroomAbvGr`, `GrLivArea`, and `SalePrice`) and evaluating the model's performance (e.g., test error).

## Dataset

The dataset, `property-sales.csv`, contains historical data on property sales, originally sourced from Kaggle and slightly modified for this assessment. It comprises **1460 observations** and **18 variables**. Detailed descriptions of variables are available in `description.txt`.

Key variables include:
*   **`SalePrice`**: The sale price of the property in US$ (target for regression).
*   **`Fireplace`**: Indicates if the property has a fireplace (Y/N) (target for classification).
*   Other variables cover various property attributes such as zoning (`MSZoning`), lot size (`LotArea`), dwelling type (`BldgType`), style (`HouseStyle`), quality and condition ratings (`OverallQual`, `OverallCond`), construction date (`YearBuilt`), living area (`GrLivArea`), number of bathrooms and bedrooms (`FullBath`, `HalfBath`, `BedroomAbvGr`), kitchen quality (`KitchenQual`), garage size (`GarageArea`), and sale condition (`SaleCondition`).

## Methodology

All analyses were performed using **R**.

### 1. Exploratory Data Analysis (EDA)

*   Data was imported, cleaned, and processed.
*   Summary statistics revealed an average sale price of US$180,921 for 1460 houses sold between 1872 and 2010.
*   Visualizations (e.g., using `ggplot`) were used to identify key characteristics:
    *   **MSZoning Distribution**: Maximum sales occurred in Residential Low Density (RL) zones.
    *   **Sale Price vs. MSZoning**: Properties in Floating Village (FV) zones generally commanded higher prices, and outliers in RL indicated high value.
    *   **Sale Price vs. Overall Quality (`OverallQual`)**: A clear **positive trend** was observed, with higher quality leading to higher prices and increased price variability.
    *   **Sale Price vs. Garage Area (`GarageArea`)**: Customers showed little value for garage areas up to approximately 675 sq ft, but variability increased exponentially beyond this range.
    *   **Sale Price vs. Above Ground Living Area (`GrLivArea`)**: Concentration of observations up to 1800 sq ft, with more variability at larger living areas, indicating `GrLivArea` influences price significantly for larger properties.
    *   **Sale Price vs. Sale Condition (`SaleCondition`)**: Partial sale conditions were preferred, showing more variability, and normal sale conditions had many outliers indicating higher willingness to pay.
    *   **Sale Price vs. Lot Area (`LotArea`)**: Customers generally did not prioritize `LotArea` as much as other attributes, with concentration of points towards the y-axis, indicating other attributes drive higher prices regardless of lot size.
    *   **Sale Price vs. Fireplace**: Properties with fireplaces commanded a **higher median price** and showed greater variability in sale price, indicating a preference for fireplaces.

### 2. Regression Model for `SalePrice` Prediction

*   An initial multiple linear regression model including all 17 explanatory variables achieved a **Multiple R-squared of 0.8185**.
*   **Variable selection** involved identifying and eliminating confounding variables through further regression analyses:
    *   `GarageArea` was found to be confounded by `GrLivArea` and `LotArea`.
    *   `BldgType`, `HouseStyle`, and `KitchenQual` were also identified as confounding.
    *   `SaleCondition` was eliminated due to lack of statistical significance with `LotArea` and `GrLivArea`.
*   The **final regression model** for `SalePrice` prediction consisted of **6 explanatory variables**: `LotArea`, `GrLivArea`, `OverallQual`, `OverallCond`, `YearBuilt`, and `BedroomAbvGr`.
*   This optimized model yielded a **Multiple R-squared of 0.7635**, with all included variables being highly statistically significant.
*   The dataset was split into a **60% training set** and a **40% test set** for model training and prediction.

### 3. Classification Model for Fireplace Prediction

*   The goal was to predict the presence of a fireplace (`Fireplace=Y,N`).
*   Character variables like `OverallQual`, `MSZoning`, `BldgType`, `HouseStyle`, `CentralAir`, `KitchenQual`, `Fireplace`, and `SaleCondition` were converted to factor variables for analysis.
*   Initial investigation identified `OverallQual`, `BedroomAbvGr`, `GrLivArea`, and `SalePrice` as potentially highly correlated predictors.
*   Different subsets of predictors were explored to optimize model performance using **LDA (Linear Discriminant Analysis)** and **logistic regression** models.
*   The dataset was split into a **70% training set** and a **30% test set**.
*   An initial LDA model with `OverallQual`, `BedroomAbvGr`, `GrLivArea`, and `SalePrice` had a test error of 28.31%.
*   **Optimization** involved removing `OverallQual` as a predictor, as its P-value was too high, indicating it was not suitable for predicting fireplace presence.
*   The **final classification model** using **`BedroomAbvGr`, `GrLivArea`, and `SalePrice`** as predictors achieved a **test error rate of 26.02%**.

## Key Findings

*   Property characteristics like overall quality, above-ground living area, and the presence of a fireplace significantly influence sale price.
*   Confounding variables were successfully identified and removed to create a more robust regression model for `SalePrice` prediction.
*   A classification model effectively predicts the presence of a fireplace based on relevant property attributes.


## Contributors

*   SNEHAL SRIVASTAVA
*   MUHAMMAD ZAIN HASHMI
*   WEIDONG LIANG
