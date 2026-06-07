# Agentic AI-Based Dynamic Tariff Optimization for EV Charging Networks

## Overview

The rapid adoption of Electric Vehicles (EVs) has increased pressure on charging infrastructure worldwide. Traditional fixed-rate charging tariffs fail to adapt to changing demand conditions, resulting in charger congestion during peak periods and underutilization during off-peak hours.

This project develops an **Agentic AI-based Dynamic Tariff Optimization Framework** that forecasts charging demand, recommends utilization-aware dynamic tariffs, and continuously evaluates pricing effectiveness using a monitoring and simulation layer.

The system combines large-scale EV charging datasets, machine learning forecasting models, and pricing optimization strategies to improve charging network efficiency while maintaining revenue performance.

---

## Objectives

The proposed framework aims to:

* Forecast EV charging demand and charger utilization.
* Predict congestion and charging load patterns.
* Generate dynamic tariff recommendations.
* Identify overloaded and underutilized charging stations.
* Simulate operational outcomes of pricing decisions.
* Monitor pricing effectiveness through feedback-driven evaluation.
* Improve:

  * Revenue Gain %
  * Charger Utilization Rate
  * Off-Peak Uplift
  * Pricing Efficiency
  * Congestion Reduction

---

## Datasets

### 1. ACN-Data (Caltech)

Session-level charging dataset containing approximately 15,000 EV charging sessions.

Features include:

* Connection Time
* Disconnect Time
* Charging Duration
* Energy Delivered (kWh)
* Station ID
* User Charging Requests

Used for:

* Session behavior analysis
* Charging duration estimation
* Utilization analysis
* Congestion proxy development

---

### 2. UrbanEV (Shenzhen)

Large-scale public charging infrastructure dataset.

Characteristics:

* 247 charging grids
* 8640 timestamps
* 5-minute resolution
* Demand
* Occupancy
* Duration
* Pricing information

Used for:

* Demand forecasting
* Utilization forecasting
* Dynamic pricing simulation
* Revenue optimization

---

## Project Pipeline

```text
Raw EV Charging Data
        │
        ▼
Data Preprocessing
        │
        ▼
Feature Engineering
        │
        ▼
Demand Prediction Agent
        │
        ▼
Tariff Pricing Agent
        │
        ▼
Simulation Layer
        │
        ▼
Monitoring & Learning Agent
        │
        ▼
Performance Evaluation
```

---

## Methodology

### 1. Data Preprocessing

* Cleaned ACN session records.
* Converted timestamps to unified datetime format.
* Aggregated charging sessions to station-hour level.
* Processed UrbanEV 5-minute records into hourly observations.
* Generated a unified analytical dataset.

### 2. Feature Engineering

Created:

#### Temporal Features

* Hour of Day
* Day of Week
* Weekend Indicator
* Month
* Peak Hour Flag

#### Demand Features

* Demand Lag 1 Hour
* Demand Lag 24 Hours
* Rolling Mean (3 Hours)
* Rolling Mean (24 Hours)
* Rolling Standard Deviation

#### Utilization Features

* Utilization Lag 24 Hours
* Utilization Rolling Mean

#### Pricing Features

* Price Ratio
* Price Change
* Historical Pricing Indicators

#### Infrastructure Features

* Charger Count
* Fast Charger Count
* Slow Charger Count
* CBD Indicator
* Dynamic Pricing Indicator

---

## Demand Prediction Agent

### Model

LightGBM Regressor

### Target

Hourly Charging Demand (kWh)

### Evaluation Strategy

Time-based train-validation-test split.

### Performance

| Metric | Value |
| ------ | ----- |
| RMSE   | 54.29 |
| MAE    | 16.65 |
| R²     | 0.998 |

### Baseline Comparison

| Model                 | RMSE   | R²    |
| --------------------- | ------ | ----- |
| Naive Lag-24 Baseline | 270.29 | 0.954 |
| LightGBM              | 59.12  | 0.979 |

### Most Important Features

* Utilization Lag 24h
* Utilization Rolling Mean
* Demand Lag 1h
* Hour of Day
* Demand Lag 24h

---

## Dynamic Tariff Pricing Agent

A utilization-aware pricing strategy was developed.

### Pricing Rules

| Utilization Level | Pricing Action |
| ----------------- | -------------- |
| < 30%             | Discount       |
| 30% – 60%         | Base Tariff    |
| > 60%             | Surge Pricing  |

### Baseline Tariff

```text
₹15 / kWh
```

### Demand Elasticity Assumption

```text
Elasticity = -0.5
```

Meaning:

```text
10% Price Increase → 5% Demand Reduction
```

---

## Monitoring & Simulation Agent

Since real deployment data was unavailable, a simulation framework was developed.

Evaluated metrics include:

* Revenue Gain %
* Off-Peak Uplift
* Customer Response Rate
* Congestion Reduction
* Pricing Efficiency Gain
* Waiting Time Proxy

---

## Results

### Dynamic Pricing Impact

| Metric                    | Result  |
| ------------------------- | ------- |
| Revenue Gain %            | +0.44%  |
| Off-Peak Uplift %         | +2.17%  |
| Customer Response Rate %  | -0.52%  |
| Congestion Reduction %    | +85.14% |
| Pricing Efficiency Gain % | +0.96%  |

### Key Finding

The proposed framework significantly reduced network congestion while maintaining positive revenue gains and improving charging network efficiency.

---

## Repository Structure

```text
├── data/
│   ├── raw/
│   ├── processed/
│
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_demand_prediction_agent.ipynb
│   ├── 05_tariff_pricing_agent.ipynb
│   ├── 06_monitoring_simulation_agent.ipynb
│
├── models/
│   └── demand_forecast_model.pkl
│
├── outputs/
│   ├── demand_predictions.csv
│   ├── tariffs.csv
│   ├── pricing_report.csv
│   ├── metrics.csv
│
├── figures/
│
└── README.md
```

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-Learn
* LightGBM
* Matplotlib
* Seaborn
* SHAP

---

## Limitations

* Waiting time was estimated using utilization-based proxies.
* Demand elasticity was assumed rather than observed.
* No real-world deployment data was available for validation.
* Dynamic pricing outcomes were evaluated through simulation.

---

## Future Work

* Real-time deployment using live charging network data.
* Reinforcement Learning based tariff optimization.
* Improved queue and waiting-time modeling.
* Integration with grid electricity pricing signals.
* Multi-objective optimization considering revenue, congestion, and customer satisfaction simultaneously.

---

## Authors

Developed as part of an academic project on EV Charging Network Optimization and Agentic AI-based Dynamic Pricing.
