# 📈 Demand Forecasting with Iterative Future Prediction

This repository contains a comprehensive demand forecasting pipeline using iterative future prediction logic, inspired by the M5 Walmart dataset.

## 🎯 Project Objective
To accurately forecast item-level daily demand for a 28-day future horizon by using an iterative approach that simulates real-world business forecasting. Each day’s forecast influences subsequent day features, creating a realistic chain of dependencies.

## 📄 Dataset Overview
- **Sales data:** Historical daily sales for each item-store combination.
- **Calendar data:** Contains dates, events, SNAP days, week and year markers.
- **Sell prices data:** Weekly price information per item and store.

## 💾 Data Source
The dataset used in this project is inspired by the [M5 Forecasting — Accuracy competition dataset on Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data).

> 📥 **Link to Kaggle competition dataset:** https://www.kaggle.com/competitions/m5-forecasting-accuracy/data

## 🛠️ Feature Engineering
### 🔥 Lag Features
- `lag_7`: Sales value 7 days ago.
- `lag_28`: Sales value 28 days ago.

### 📈 Rolling Means
- `Rolling_7`: Mean of sales over past 7 days.
- `Rolling_28`: Mean of sales over past 28 days.

### 💰 Price Features
- `sell_price`: Current price of the item on given week.
- `price_lag_7`: Price 7 days ago.
- `price_change_flag`: Binary flag if the price changed compared to 7 days ago.

### 📅 Calendar Features
- `day_of_month`, `week_number`, `quarter`, `year`, `is_weekend`.

## ⚡ Model Approach
### Model Choice
- **LightGBM Regressor**: Selected for its speed and ability to handle large, tabular data efficiently.

### Hyperparameter Tuning
- Initial baseline parameters were tuned using manual grid search to improve RMSE and MAE.

## 🔄 Iterative Forecasting Logic
### Why Iterative?
In real-world retail, future sales forecasts depend on actual outcomes of previous days. Thus, each predicted day updates the "history" used to create features for the next day.

### Step-by-Step Iterative Prediction
1️⃣ **Copy last day’s data (`base_df`).**  
2️⃣ **Update date to first future day.**  
3️⃣ **Create features:** Calendar, Lag, Rolling, Price.  
4️⃣ **Predict sales using LightGBM.**  
5️⃣ **Append predicted day to historical data.**  
6️⃣ **Repeat steps 3–5 for each future day.**

### 📅 Forecast Period
- Start: **2016-04-25**
- End: **2016-05-22** (28 days total)

