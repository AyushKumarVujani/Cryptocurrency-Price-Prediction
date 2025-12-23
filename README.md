# Predicting Short-Term Cryptocurrency Price Movements

This repository contains an exploratory machine learning project focused on **short-term cryptocurrency price forecasting** using time-series models. The primary goal of the project is to **compare a classical statistical baseline (ARIMA)** with a **deep learning approach (LSTM)** in a highly volatile and non-stationary market setting.

The project uses historical Bitcoin price data as a case study and is intended for **learning and experimentation**, not production trading.

---

## Project Objectives

- Understand time-series forecasting fundamentals in volatile markets  
- Establish a statistical baseline using ARIMA  
- Evaluate whether an LSTM model can capture non-linear temporal patterns more effectively  
- Apply correct time-based data splitting and sequence modeling  
- Assess model performance using appropriate regression metrics  

---

## Dataset

- **Source:** Yahoo Finance (`BTC-USD`)
- **Frequency:** Daily

### Available Columns

- Date  
- Open  
- High  
- Low  
- Close  
- Adjusted Close  
- Volume  

### Columns Used

- **Adjusted Close** → ARIMA baseline model  
- **Close Price** → LSTM model  

Other features were intentionally excluded to keep the modeling focused and interpretable.

---

## Modeling Approach

### ARIMA (Baseline Model)

- ARIMA is used as a **statistical benchmark**
- Captures linear temporal dependencies and short-term autocorrelation
- Configuration: `ARIMA(5,1,0)` (not exhaustively tuned)
- Used only for baseline comparison

> ARIMA is **not combined** with the LSTM model and is not part of a hybrid architecture.

---

### LSTM (Proposed Model)

- A stacked LSTM network is used as the primary predictive model
- Formulated as a **sequence-to-one forecasting problem**
- Input: Previous **100 days** of closing prices  
- Output: Next-day price prediction  

#### Key Design Choices

- MinMax scaling for stable neural network training  
- Chronological train–test split (no shuffling)  
- Rolling window sequence generation  
- Dropout regularization to reduce overfitting  

---

## Training & Evaluation

### Evaluation Metrics

The models are evaluated using:

- **Mean Squared Error (MSE)**  
- **Root Mean Squared Error (RMSE)**  
- **Visual comparison of predicted vs actual prices**

Metrics are initially computed in **normalized space**, followed by inverse scaling for interpretability.

> Accuracy-based metrics are intentionally avoided since this is a regression problem.

---

## Results Summary

- The LSTM model achieves **lower RMSE on unseen data** compared to the ARIMA baseline  
- LSTM predictions capture overall trends more effectively but show smoothing and lag during sharp price movements  
- ARIMA performs reasonably in stable regimes but struggles during periods of high volatility  

These observations are consistent with the strengths and limitations of each modeling approach.

---

## Limitations

This project has several known limitations:

- Predicts **price levels**, not returns  
- Uses only historical prices (no exogenous variables)  
- ARIMA parameters are not fully optimized  
- Evaluation uses a single train–test split instead of walk-forward validation  
- Model persistence approach can be improved for production robustness  

These limitations are acknowledged intentionally and represent opportunities for improvement.

---

## Future Improvements

Potential extensions include:

- Predicting log-returns instead of prices  
- Adding technical indicators or volume-based features  
- Implementing walk-forward or rolling-window validation  
- Incorporating exogenous variables (e.g., macroeconomic or sentiment data)  
- Exploring GRU or Transformer-based architectures  

---

## Usage

```bash
git clone https://github.com/AyushKumarVujani/Crypto-Returns.git
cd Crypto-Returns
pip install -r requirements.txt
python main.py
