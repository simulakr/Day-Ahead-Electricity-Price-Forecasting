# Day-Ahead Electricity Price Forecasting & Trading Strategy

## 📊 Project Overview
This project develops a machine learning model to forecast day-ahead electricity prices in the Turkish energy market (EPIAS) and implements a simple trading strategy based on predictions. The model achieves **87.8% R² score** with a **54% improvement** over baseline methods.

## 🎯 Objectives
- Predict hourly day-ahead electricity prices (PTF - Market Clearing Price)
- Analyze the impact of renewable energy, demand, and supply dynamics on pricing
- Develop an automated trading strategy based on price forecasts
- Demonstrate quantitative analysis skills for energy sector applications

## 📁 Data Source
- **Platform:** EPIAS Transparency Platform (Turkish Electricity Market)
- **Time Period:** October 30, 2023 - October 30, 2025 (2 years)
- **Granularity:** Hourly data (~17,500 observations)
- **Variables:** 
  - Market Clearing Price (PTF) in TL/MWh
  - Hourly consumption (MWh)
  - Generation by source (Natural Gas, Wind, Solar, Hydro, Coal, etc.)

## 🔧 Methodology

### 1. Exploratory Data Analysis (EDA)
- Analyzed price patterns across hours, days, and months
- Identified peak pricing periods (17:00-22:00)
- Examined correlations between renewable generation and prices
- Discovered strong seasonality and demand-supply dynamics

### 2. Feature Engineering
**Lag Features:**
- `PTF_lag1`, `PTF_lag24`, `PTF_lag168` (1 hour, 1 day, 1 week)

**Rolling Statistics:**
- 24-hour and weekly rolling means/standard deviations

**Cyclic Encoding:**
- Sin/cos transformations for Hour, Day, Month (to capture periodicity)

**Domain-Specific Features:**
- Renewable Share: `(Wind + Solar + Hydro) / Total Generation`
- Fossil Share: `(Natural Gas + Coal) / Total Generation`
- Supply-Demand Ratio: `Total Generation / Consumption`
- Binary flags: `IsWeekend`, `IsPeakHour`

### 3. Model Selection
Compared multiple algorithms:
- **Baseline:** Naive forecast (previous day same hour)
- **Random Forest**
- **XGBoost**
- **LightGBM** ← Best performer

### 4. Trading Strategy
- **Logic:** If predicted price > current price → LONG (expect increase)
- **Execution:** Open position at hour t, close at hour t+1
- **Evaluation:** PnL, win rate, Sharpe ratio, maximum drawdown

## 📈 Results

### Model Performance
| Model | MAE (TL/MWh) | RMSE (TL/MWh) | R² Score |
|-------|--------------|---------------|----------|
| Baseline | 394.35 | 696.04 | 0.176 |
| Random Forest | 202.55 | 297.20 | 0.850 |
| XGBoost | 201.88 | 282.82 | 0.864 |
| **LightGBM** | **180.57** | **268.30** | **0.878** |

**Key Achievements:**
- **87.8% R²** - Model explains 87.8% of price variance
- **~7% MAPE** - Mean absolute percentage error
- **54% improvement** over baseline (MAE: 394 → 180)

### Feature Importance
![Feature Importance](feature_importances.PNG)

Top predictors: Lag features (PTF_lag1, PTF_lag24), consumption, natural gas generation, and renewable share.

### Predictions vs Actual
![Predictions](predictions.PNG)

The model accurately captures price volatility and patterns across different time periods.

### Trading Strategy Results
![Trading Strategy](trading_strategy.PNG)

The momentum-based strategy demonstrates the practical application of price forecasting in energy trading.

## 🛠️ Technologies Used
- **Python 3.x**
- **Libraries:** 
  - Data: pandas, numpy
  - Visualization: matplotlib, seaborn
  - Modeling: scikit-learn, LightGBM, XGBoost
  - Statistics: scipy, statsmodels

## 💡 Key Insights
1. **Lag features are critical:** Previous hour and previous day prices are the strongest predictors
2. **Renewable impact:** Higher renewable share correlates with lower prices
3. **Peak hours:** 17:00-22:00 consistently show higher prices due to demand
4. **Weekend effect:** Prices are significantly lower on weekends (industrial demand drops)
5. **Natural gas dependency:** Natural gas generation strongly influences pricing

## 📊 Business Applications
- **Energy Trading:** Optimize buy/sell decisions in day-ahead markets
- **Risk Management:** Forecast price volatility for hedging strategies
- **Portfolio Optimization:** Balance renewable vs. conventional generation
- **Load Scheduling:** Plan industrial operations during low-price periods

## 🚀 Future Improvements
- Incorporate weather forecasts (temperature, wind speed, solar radiation)
- Add macroeconomic indicators (natural gas prices, exchange rates)
- Implement deep learning models (LSTM, Transformer architectures)
- Develop multi-horizon forecasting (predict 24 hours ahead)
- Test advanced trading strategies (mean reversion, arbitrage)

## 📧 Contact
Yunus BİLGİÇ | in/yunus_bilgic | Data/Quant Analyst Portfolio

---

**Note:** This project demonstrates quantitative analysis skills for energy trading roles, combining domain knowledge with machine learning expertise.
