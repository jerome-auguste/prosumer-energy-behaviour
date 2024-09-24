# Enefit - Predict Energy Behavior of Prosumers

Personnal analysis and solution for a [Kaggle Challenge](https://www.kaggle.com/competitions/predict-energy-behavior-of-prosumers/overview) proposed by Enefit to predict energy production and consumption of prosumers.

## [TODO] Repository Structure

## Data sctructure and relationship

After introductory analysis, the data is structured as follows:

```mermaid
erDiagram
    test {
        int county
        int is_business
        int product_type
        int is_consumption
        datetime prediction_datetime
        int row_id
        int prediction_unit_id
    }
    client {
        int product_type
        int county
        int eic_count
        float installed_capacity
        bool is_business
        date date
    }
    historical_weather {
        datetime datetime
        float temperature
        float dewpoint
        float rain
        float snowfall
        float surface_pressure
        int cloud_cover_total
        int xcloud_cover_low
        int xcloud_cover_mid
        int xcloud_cover_high
        float windspeed_10m
        int winddirection_10m
        float shortwave_radiation
        float direct_solar_radiation
        float diffuse_radiation
        float latitude
        float longitude
    }
    forecast_weather {
        float latitude
        float longitude
        datetime origin_datetime
        int hours_ahead
        float temperature
        float dewpoint
        float cloudcover_high
        float cloudcover_low
        float cloudcover_mid
        float cloudcover_total
        float _10_metre_u_wind_component
        float _10_metre_v_wind_component
        datetime forecast_datetime
        float direct_solar_radiation
        float surface_solar_radiation_downwards
        float snowfall
        float total_precipitation
    }
    electricity_price {
        datetime forecast_datetime
        float euros_per_mwh
        datetime origin_datetime
    }
    gas_prices {
        date forecast_date
        float lowest_price_per_mwh
        float highest_price_per_mwh
        float origin_date
    }
    test |{--|| client : "identifies (county x product_type x is_business)"
    historical_weather |{--|| test : "locates (latitude x longitude <-> county)"
    forecast_weather |{--|| test : "locates (latitude x longitude <-> county)"
    electricity_price |{--|| test : "applies (prediction_datetime = forecast_datetime)"
    gas_prices |{--|| test : "applies (prediction_datetime = forecast_datetime)"

```
Notes:
- Compared to test, train has a `target` which is the value to predict either for consumption or production
- The column `prediction_datetime` in test dataframe corresponds to the `datetime` column in train


## TODO

### Simplest baseline

#### EDA
- [ ] Univariate analysis
- [ ] Multivariate analysis
- [ ] Check for missing values
- [ ] Correlation matrix
- [ ] PCA

#### Feature engineering
- [ ] Average weather data to the entire Estonia
- [ ] Reencode product_type to a more relevant way like onehot (cf Kaggle description `{0: "Combined", 1: "Fixed", 2: "General service", 3: "Spot"}`)
- [ ] List and remove useless columns for a first version and list columns that could help improve in further versions
- [ ] Do not use historical weather data
- [ ] Split train data into train and validation sets
- [ ] Normalize data

#### Model selection
- [ ] Baseline model?
- [ ] Learn time-series forecasting techniques (ARIMA, SARIMA...)
- [ ] Implement a simple model

#### Evaluation
- [ ] Test best model on test set using MAE

### Further versions

#### EDA
- [ ] Check historical vs forecast weather data

#### Feature engineering
- [ ] Map county names to latitude and longitude ranges (approximately)
- [ ] Use local forecast weather data instead of average one
- [ ] Include historical weather data


#### Model selection
- [ ] Litterature review on time-series forecasting
- [ ] Test Prophet
- [ ] Test XGBoost
- [ ] Train & evaluate LSTM, GRU, RNN
- [ ] Train & evaluate Transformers?
