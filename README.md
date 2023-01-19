# Data602-FinalProject
Forecasting the next hour's precipitation in mm in Tacoma/McChord, WA

This is my final project for DATA602 Principles of Data Science at the University of Maryland. The objective of this project is to forecast the next hour's precipitation in mm in Tacoma/McChord, WA using time-series data. This objective is uniquely challenging due to the presence of a large quantity of 0's in our target variable, next hour's precipitation. My group and I used the Meteostat Python library (https://github.com/meteostat/meteostat-python) to access open weather data from sources like the National Oceanic and Atmospheric Administration (NOAA). The features selected to forecast the next hour's precipitation are previous hour's precipitation (in mm), dewpoint, temperature, wind speed, and weather code. Each feature is lagged by order = 12 (hours). The models are trained on historical data from November 11, 2021 to 48 hours prior to the current day.  

My contributions to this project are the functions to import, process and prepare the data for forecasting, the multiple linear regression model, the random forest regression model with zero-inflated regressor, and the regression model with an added artificial neural network. Plotly is used to compare the predicted precipitation with the actual precipitation from Meteostat.

The multiple linear regression model uses the linear_model from sklearn to forecast the next hour's precipitation using our selected features that are each lagged by order = 12.  
![newplot (10)](https://user-images.githubusercontent.com/109245460/213548264-1133a46a-d2e0-4dd1-b396-477d0dcd07b2.png)

The random forest regression model with zero-inflated regressor is a two part classification + regression model. This model aims to first classify whether the target variable is 0 using XGBoost Classifier. The random forest regression model is trained on all non-zero targets identified by the classifier.
![newplot (11)](https://user-images.githubusercontent.com/109245460/213548802-29a7ac41-8661-4af5-b272-18b57e528126.png)

The regression model with an added artificial neural network uses the keras sequential model from tensorflow. This model performed the worst due to the excess 0's in the target variable. Like the multiple linear regression model, this model cannot really predict when the target variable is exactly 0mm. In the future, I would take steps to account for the presence of excess 0's in the target before training an ANN model.
![newplot (12)](https://user-images.githubusercontent.com/109245460/213549623-eeedfef7-7164-4e5f-8edf-852f579e786e.png)

This is a table comparing the performance of my three models on current forecasting data (new unseen data).
<img width="922" alt="Screenshot 2023-01-19 at 3 14 46 PM" src="https://user-images.githubusercontent.com/109245460/213550192-77b15ed3-47c1-4e67-9774-5713295bcd6d.png">
