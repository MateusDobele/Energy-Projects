# Forecasting Renewable Energy Generation: A Comparative Analysis and Ensemble Approach

## Overview

This repository contains the code and data for my master's thesis: **"A Comparative Analysis and Ensemble Approach of VAR, XGBoost, and LSTM for Forecasting Renewable Energy Generation."** This project aims to compare the performance of three forecasting models (VAR, XGBoost, and LSTM) and an ensemble model integrating VAR, XGBoost and LSTM to predict renewable (solar) energy generation accurately. 

## Table of Contents

- [Abstract](#abstract)
- [Data](#data)
- [Train-Test Split](#train-test-split)
- [Models](#models)
  - [Vector Autoregression (VAR)](#vector-autoregression-var)
  - [Extreme Gradient Boosting (XGBoost)](#extreme-gradient-boosting-xgboost)
  - [Long Short-Term Memory (LSTM)](#long-short-term-memory-lstm)
  - [Ensemble Model (VAR, XGBoost, LSTM)](#ensemble-model-var-xgboost-lstm)
- [Installation](#installation)

## Abstract

Global energy consumption is expected to rise by 34% by 2050, heightening the urgency to transition from fossil fuels to sustainable energy sources. This research addresses the need for accurate renewable energy generation forecasting, crucial for integrating renewable sources into energy systems. The study compares the performance of three forecasting models: Vector Autoregression (VAR), Extreme Gradient Boosting (XGBoost), and Long Short-Term Memory (LSTM) networks, along with an ensemble model combining these methods. Evaluation metrics include Root Mean Square Error (RMSE), Mean Absolute Error (MAE), and quantile loss scores across different forecasting horizons.

XGBoost consistently outperforms VAR and LSTM, showing superior short-term accuracy with lower RMSE and MAE values. VAR performs reasonably well in the short term but struggles with long-term accuracy due to its linear assumptions. LSTM, while capable of capturing complex patterns, exhibits substantial errors, particularly in long-term forecasts, likely due to overfitting and sensitivity to noise. The ensemble model, integrating the strengths of VAR, XGBoost, and LSTM, achieves the best performance, especially in medium and long-term forecasts, with significantly lower error metrics.

Quantile loss scores highlight XGBoost's precision in short-term probabilistic forecasting, while the ensemble model excels in capturing a range of outcomes over longer horizons. Training time analysis indicates XGBoost’s efficiency, making it suitable for frequent updates, whereas VAR and LSTM require more computational resources.

This research underscores the effectiveness of ensemble models in renewable energy forecasting, recommending their use for medium to long-term predictions while leveraging XGBoost for short-term accuracy. Future studies should explore applying these models to diverse geographic regions and other renewable energy sources, extending forecasting horizons, and incorporating causality metrics to enhance model interpretability. The findings support improved energy management and strategic planning, facilitating a more sustainable energy transition.

## Data 

This project utilizes two publicly available datasets from Kaggle, spanning four years of data recorded hourly, from January 2015 to December 2018.

The first dataset focuses on energy and contains 35,064 observations across 29 features. These features include data on energy generated from fossil fuel and renewable sources in Spain, forecasts and actual values for wind and solar energy, total energy load, and forecasted and actual prices for total produced energy. Energy generation data is sourced from ENTSOE, while price-related data is sourced from the Spanish Transmission System Operator - Red Eléctrica de España.

The second dataset includes 178,396 observations across 17 weather-related features, critical for predicting renewable energy generation. Weather-related features include data on air temperature, atmospheric pressure, humidity, wind speed, and precipitation levels. This dataset is limited to Spain’s five largest cities—Barcelona, Bilbao, Madrid, Seville, and Valencia, and is sourced from the Open Weather API.

The data is made available in the GitHub repository, but can also be accessed directly on Kaggle: [Energy Consumption, Generation, Prices, and Weather](https://www.kaggle.com/datasets/nicholasjhana/energy-consumption-generation-prices-and-weather).

## Train-Test Split

The dataset for this study was systematically divided using a time-based split to ensure the integrity of the forecasting process and to prevent data leakage, a common issue in time-series analysis. Following standard practices in time-series model development, the data was divided into training and test sets. Since the data is organized chronologically, splitting it in this order is crucial for preventing data leakage and ensuring the integrity of the model.

The **training set** encompasses data from **3-07-2017 to 1-07-2018**. This period was chosen to include multiple complete cycles of seasonal variations, which are crucial for training models to recognize and adapt to patterns in solar energy generation affected by differing weather conditions. The **test set** includes data from **2-07-2018 to 31-12-2018**, allowing the models to be validated against unseen data. This approach aligns with best practices for evaluating forecasting models by using subsequent dates as a hold-out set.

To handle the skewness of certain features and to ensure comparability across variables, log transformation and standardization were applied. Log transformation was particularly used for the target variable, solar energy generation, and skewed features like rain_1h and lag1_generation_solar. This transformation helps in stabilizing the variance and normalizing the distribution, making the data more suitable for linear models. After log transformation, standardization was applied to scale features to have zero mean and unit variance, which is essential for many machine learning algorithms to perform optimally. Standardization ensures that features with larger scales do not dominate the model training process, thereby improving model performance and convergence speed. These transformations were performed after splitting the data into training and test sets to avoid data leakage and ensure that the model does not gain an unfair advantage by having access to future information during training.

The split of data into training and test sets following these criteria ensures that the forecasting models developed in this study are both robust and capable of generalizing well to new data. This methodology not only adheres to the rigorous standards required for scientific research in the field of energy forecasting but also provides a solid foundation for operational applications where the accurate prediction of solar energy generation is critical.

## Models

### Vector Autoregression (VAR)

VAR is used for capturing linear interdependencies among multiple time series. It is effective for short-term forecasting but struggles with long-term predictions due to its linear nature.

### Extreme Gradient Boosting (XGBoost)

XGBoost is a powerful machine learning algorithm known for handling non-linear relationships efficiently. It consistently outperforms other models in short-term and medium-term forecasts.

### Long Short-Term Memory (LSTM)

LSTM networks are a type of recurrent neural network capable of learning long-term dependencies. While they can capture complex patterns, they may suffer from overfitting and high computational costs.

### Ensemble Model (VAR, XGBoost, LSTM)

The ensemble model integrates VAR, XGBoost, and LSTM to leverage their strengths. It performs well in medium and long-term forecasts, providing robust and reliable predictions.

## Installation

To run the code in this repository, you'll need to install the following dependencies:

```bash
pip install numpy pandas tqdm optuna seaborn matplotlib statsmodels scikit-learn xgboost tensorflow arch
