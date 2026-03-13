# Bitcoin Market Analysis & Deep Learning Price Prediction


### Author: Leo Suzuki | Tampere University of Applied Sciences | 2026

## 📖 Project Overview
This project is a fully automated, end-to-end pipeline for cryptocurrency analysis and forecasting. It eliminates the need for static CSV files by dynamically fetching the most recent 5 years of live market and search trend data. 

The project is divided into two main phases:
1. **Market & Trend Retrospective:** Analyzing Bitcoin's price history against global Google Search interest.
2. **Deep Learning Forecasting:** A head-to-head battle between Long Short-Term Memory (LSTM) and 1D Convolutional Neural Network (CNN) models to predict the next 30 days of price action.

---

## 🚀 How to Run This Project
This notebook is designed to run automatically without manual data downloads or Google Drive mounting.

1. **Install Required APIs:** Ensure the first cell in your notebook includes and runs this command to install the live data fetchers: `!pip install yfinance pytrends`
2. **Execute the Code:** Run all remaining cells from top to bottom.
   - **Dynamic Timeframe:** The script automatically calculates a rolling 5-year window backwards from the current date (e.g., 2021–2026).
   - **Live APIs:** Connects seamlessly to yfinance (financial data) and pytrends (search volume).

---

## 🛠 Libraries & Technologies
- **Data Gathering:** yfinance, pytrends
- **Data Manipulation:** pandas, numpy, datetime
- **Machine Learning:** tensorflow, keras, scikit-learn
- **Interactive Visualization:** plotly, matplotlib

---

## Part 1: Market Value vs. Global Search Trends

### Automated Data Pipeline
- **Bitcoin Stock Data:** Fetched daily opening/closing prices dynamically using the yfinance API.
- **Google Trends Data:** Queried worldwide "Bitcoin" search volumes matching the exact 5-year timeframe using the pytrends API.

### Visualizations & Analysis
- **Dynamic 5-Year Overlays:** Yearly average prices displayed using Plotly's qualitative color scales.
- **Auto-Scaling Annotations:** The charts automatically calculate maximum prices to draw perfectly scaled indicators for major macro events (e.g., Bitcoin Halvings).
- **Search Trend Correlation:** Dual-axis line charts map Google search volumes directly against Bitcoin’s price to observe public interest shifts during bull and bear cycles.

---

## Part 2: AI Price Prediction (LSTM vs. CNN)

The second half of the project applies advanced neural networks to the dynamic 5-year dataset to forecast the asset's trajectory for the upcoming 30 days.

### Model Architectures
1. **Long Short-Term Memory (LSTM)**
   - **Strategy:** Designed for sequential time-series data. It uses internal memory gates to capture long-term price momentum.
   - **Structure:** Sequential LSTM layers paired with Dropout for regularization, feeding into Dense output layers. Optimized with Adam using a 60-day sliding window.

2. **1D Convolutional Neural Network (CNN)**
   - **Strategy:** Designed to recognize geometric "shapes" in the data (like short-term peaks, valleys, and consolidation flags).
   - **Structure:** Conv1D layers for feature extraction paired with MaxPooling1D, standardized with tanh activations and a tuned learning rate to prevent exploding gradients on highly volatile data.

### Evaluation & Results
The models were evaluated against unseen test data using standard regression metrics. The results highlighted a massive performance divergence based on how the two architectures process 1D time-series data:

| Metric | LSTM Model | CNN Model |
| :--- | :--- | :--- |
| **RMSE (Error)** | **$3,660.30** | $27,655.08 |
| **R² Score** | **0.90** | -4.71 |

### Forecasting Visualizations
- **Interactive Divergence Plot:** A zoomed-in look at the last 60 days of real data splitting into the two separate 30-day forecast paths.
- **The Macro View:** A complete 1-year historical chart paired with the 30-day future forecasts from both models, featuring interactive Plotly range sliders.

---

## 🏆 Project Conclusion & Model Comparison

### 1. The Numbers
- **LSTM Model:** Achieved a solid R-squared of **0.90** with an RMSE of **$3,660.30**. It successfully followed the overall price trend during the test period.
- **CNN Model:** Struggled significantly with this dataset, resulting in an R-squared of **-4.71** and a high RMSE of **$27,655.08**. This indicates the model failed to capture the sequential nature of the price action.

### 2. Summary
The LSTM is the clear winner for this univariate price forecasting task. While the CNN found some spatial features, it lacked the long-term dependency memory required to handle Bitcoin's high volatility over time. This confirms that Recurrent Neural Networks (RNNs) like LSTM remain superior to standard 1D-CNNs for direct financial time-series prediction.

### 3. Future Potential for CNNs
Although the standalone CNN performed poorly, CNNs are highly valuable in quantitative finance when used as **Feature Extractors**. In a hybrid **CNN-LSTM** architecture, the CNN layer would first identify complex local patterns (like 'head and shoulders' or specific breakout shapes), and then pass those high-level features to the LSTM to handle the time-series forecasting. This combination often outperforms either model used in isolation.