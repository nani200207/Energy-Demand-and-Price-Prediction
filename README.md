LSTM-Based Forecasting of Power Demand and Dynamic Pricing in Norway
Overview

This project implements LSTM (Long Short-Term Memory) neural networks to forecast:

Hourly electricity demand

Hourly dynamic pricing

The models use smart meter data from Norwegian households and incorporate temporal and environmental features such as:

Hour of day, day of week, weekend indicator

Temperature

Lagged demand and rolling statistics

The goal is to support energy providers with accurate short-term forecasts for better grid stability and pricing strategies


Dataset

The dataset is sourced from the iFlex Dynamic Pricing Experiment in Norway and contains:

Hourly electricity consumption

Dynamic pricing

Temperature

User IDs from three regions: Oslo, Bergen, Stavanger

You can download it from Zenodo: https://zenodo.org/records/8248802
 


Features

Time-based features: hour, day, weekend, sine/cosine transformations

Lag features: 1h, 3h, 24h, 168h

Rolling statistics: mean and standard deviation over multiple windows

Interaction features: temperature × hour

Normalization and sequence creation for LSTM input

Model

Architecture: Multiple LSTM layers with dropout and dense layers

Training: 80/20 temporal train-test split

Loss: Mean Squared Error (MSE)

Optimizer: Adam

Forecasting: Recursive 24-hour ahead predictions

Results

Power Demand Model: R² = 0.7985, MAE = 0.4781 kWh

Dynamic Pricing Model: R² = 0.8865, MAE = 0.0330 NOK/kWh

The models capture daily and weekly cycles and regional variations in electricity demand, with subtle predictions for dynamic pricing


Installation

Clone this repository:

git clone <REPO_URL>
cd <REPO_FOLDER>


Install dependencies:

pip install -r requirements.txt


Download the dataset and place CSV files in a data/ folder.

Usage

Preprocess the dataset:

from preprocess import preprocess_data
df = preprocess_data('data/hourly_data.csv', 'data/participants.csv')


Train the LSTM models:

from lstm_model import train_power_demand, train_dynamic_price
train_power_demand(df)
train_dynamic_price(df)


Make forecasts:

from forecast import forecast_next_24h
forecast_next_24h(model, df)


Evaluate performance:

from evaluation import evaluate_model
evaluate_model(model, X_test, y_test)
