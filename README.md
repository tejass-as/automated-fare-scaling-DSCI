# Automated Fare Scaling

This project implements a dynamic pricing strategy for ride-sharing services by analyzing historical ride data. It leverages data exploration, cleaning, visualization, correlation analysis, and machine learning to predict adjusted ride costs based on demand and supply factors.

---

## Table of Contents

- Project Overview  
- Dataset
- Data Exploration & Cleaning  
- Data Visualization 
- Correlation Analysis
- Dynamic Pricing Strategy  
- Model Training 
- Model Evaluation  
- Price Prediction
- Actual vs Predicted Comparison
- Usage
- Requirements  

---

## Project Overview

This project analyzes ride-sharing data to create a dynamic pricing model where the cost of rides is adjusted based on supply and demand conditions. A Random Forest Regressor model predicts ride costs, improving profitability by capturing demand surges and supply shortages.

---

## Dataset

The dataset (`dataset.csv`) contains 1000 records with the following columns:

| Column Name               | Description                     | Type         |
|---------------------------|--------------------------------|--------------|
| Number_of_Riders          | Number of ride requests         | int          |
| Number_of_Drivers         | Number of available drivers     | int          |
| Location_Category         | Urban, Suburban, Rural          | categorical  |
| Customer_Loyalty_Status   | Regular, Silver, Gold           | categorical  |
| Number_of_Past_Rides      | Customer's past ride count      | int          |
| Average_Ratings           | Average rating of rides         | float        |
| Time_of_Booking           | Morning, Afternoon, Evening, Night | categorical  |
| Vehicle_Type              | Economy or Premium              | categorical  |
| Expected_Ride_Duration    | Duration of ride in minutes     | int          |
| Historical_Cost_of_Ride   | Original cost of ride           | float        |

---

## Data Exploration & Cleaning

- Checked for null/missing values — none found.  
- Removed duplicate entries.  
- Verified data types for each column.  
- Statistical summary using `.describe()` for numerical columns.

---

## Data Visualization

Used Plotly to visualize relationships between `Historical_Cost_of_Ride` and other features:

- Scatter plots with trendlines for continuous variables (`Number_of_Riders`, `Number_of_Drivers`, `Number_of_Past_Rides`, `Average_Ratings`, `Expected_Ride_Duration`).  
- Box plots for categorical variables (`Location_Category`, `Customer_Loyalty_Status`, `Time_of_Booking`, `Vehicle_Type`).

---

## Correlation Analysis

- Encoded categorical variables using LabelEncoder.  
- Computed correlation matrix using Pearson correlation.  
- Visualized correlations with Seaborn heatmap.  
- Found strong correlation between `Expected_Ride_Duration` and `Historical_Cost_of_Ride`.

---

## Dynamic Pricing Strategy

- Defined high and low percentile thresholds for demand (`Number_of_Riders`) and supply (`Number_of_Drivers`).  
- Calculated demand and supply multipliers based on percentile thresholds.  
- Computed `adjusted_ride_cost` by applying demand and supply multipliers to `Historical_Cost_of_Ride`.  
- Calculated `profit_percentage` to analyze profitability after applying dynamic pricing.  
- Visualized profitability with a pie chart.

---

## Model Training

- Features selected: `Number_of_Riders`, `Number_of_Drivers`, `Vehicle_Type`, `Expected_Ride_Duration` (vehicle type encoded as Economy=0, Premium=1).  
- Target variable: `adjusted_ride_cost`.  
- Split data into training (80%) and test (20%) sets with fixed random seed for reproducibility.  
- Trained a Random Forest Regressor model.

---

## Model Evaluation

Metrics on test set:

| Metric                  | Value           |
|-------------------------|-----------------|
| Mean Squared Error (MSE)| 25937.83        |
| Root MSE (RMSE)         | 161.05          |
| Mean Absolute Error (MAE)| 112.36         |
| R² Score                | 0.873           |

---

## Price Prediction

- Created a function `predict_price()` that takes user inputs for number of riders, number of drivers, vehicle type, and expected ride duration.  
- Returns predicted adjusted ride cost using the trained model.

Example usage:

```python
predicted_price = predict_price(50, 25, 0, 30)
print(f"Predicted price: {predicted_price.round(3)}")
