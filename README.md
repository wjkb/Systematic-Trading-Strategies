# Trading Strategy 1: Combining Bollinger Bands, RSI, and ATR for MAANG Stocks

This repository contains a Python-based trading strategy that integrates **Bollinger Bands**, **Relative Strength Index (RSI)**, and **Average True Range (ATR)** to generate buy and sell signals. The strategy is designed for backtesting on MAANG stocks (Meta, Apple, Amazon, Netflix, and Google) over a specified period, comparing its performance against a simple buy-and-hold approach.

---

## Key Features

### 1. **Technical Indicators Used**
- **Bollinger Bands (BB)**: Identifies overbought and oversold market conditions by measuring price volatility.
- **Relative Strength Index (RSI)**: A momentum oscillator that highlights overbought or oversold conditions based on price momentum.
- **Average True Range (ATR)**: A volatility measure used to filter trades during periods of excessive market noise.

### 2. **Signal Generation**
- **Buy Signal**: Triggered when the stock price drops below the lower Bollinger Band and the RSI is below 30 (oversold condition).
- **Sell Signal**: Triggered when the stock price rises above the upper Bollinger Band, RSI is above 70 (overbought condition), and ATR exceeds the 75th percentile.

### 3. **Position Management**
- The strategy maintains alternating long and short positions and avoids exiting the market completely. If no valid signal is generated, the previous position is retained.

---

## Strategy Performance

The strategy has been backtested on **MAANG stocks** from **1st January 2015 to 31st December 2019**. The following performance metrics are calculated and visualized:

1. **Annualized Returns**
2. **Alpha & Beta**
3. **Standard Deviation**
4. **Sharpe Ratio**
5. **Maximum Drawdown**
6. **Sortino Ratio**
7. **Calmar Ratio**
8. **Treynor Ratio**
9. **Information Ratio**

---

## Plots and Visualizations

- **Price and Signals Plot:** Shows buy and sell signals on the stock price chart.
- **Bollinger Bands Plot:** Illustrates the stock price with the upper and lower Bollinger Bands.
- **RSI Plot:** Displays the RSI value over time, marking overbought (70) and oversold (30) levels.
- **ATR Plot:** Plots the stock’s volatility using the ATR indicator.
- **Histograms:** Shows the distribution of log returns for both the strategy and the stock.
- **Drawdown Plot:** Visualizes the drawdowns for both the strategy and the buy-and-hold approach.
- **Cumulative Returns Plot:** Compares the cumulative returns of the strategy vs. buy-and-hold.

## Optimization

The parameters for Bollinger Bands, RSI, and ATR have been optimized based on Sharpe Ratio, with the following values yielding the best performance:
   - **Bollinger Bands Window**: 20
   - **Bollinger Bands Standard Deviation**: 2
   - **RSI Window**: 21
   - **ATR Window**: 14

These parameters provided a **Sharpe Ratio of 1.79** during the optimization process.

---

## Performance Comparison

The strategy’s performance is compared to a simple buy-and-hold strategy. Metrics such as Sharpe Ratio, Alpha, Beta, and Maximum Drawdown are calculated and visualized for both strategies. Cumulative returns are also plotted to provide a direct comparison.

---

## Key Performance Metrics

The following metrics are used to evaluate the strategy's performance and compare it with a simple **buy-and-hold** strategy.

### Metrics:

| **Metric**            | **Buy-and-Hold** | **Strategy**      |
|-----------------------|------------------|-------------------|
| **Annual Returns**     | 0.311563         | 0.326523          |
| **Alpha**              | 0.157792         | 0.234580          |
| **Beta**               | 1.294180         | 0.773816          |
| **Standard Deviation** | 0.228389         | 0.182173          |
| **Sharpe Ratio**       | 1.364180         | 1.792383          |
| **Max Drawdown**       | 1.182958         | 0.430533          |
| **Sortino Ratio**      | 1.995577         | 2.721313          |
| **Calmar Ratio**       | 0.263376         | 0.758415          |
| **Treynor Ratio**      | 0.240742         | 0.421965          |
| **Information Ratio**  | 1.256211         | 1.360234          |

---

### Explanation of Metrics

1. **Annual Returns**: The total return generated annually by the strategy and buy-and-hold approach.
2. **Alpha**: Measures the strategy’s excess returns relative to a benchmark, after adjusting for market risk.
3. **Beta**: A measure of the volatility of the strategy or stock in comparison to the market as a whole.
4. **Standard Deviation**: The statistical measure of the dispersion of returns, representing risk.
5. **Sharpe Ratio**: A risk-adjusted measure of return, calculated by dividing excess returns by the standard deviation.
6. **Max Drawdown**: The maximum observed loss from a peak to a trough before a new peak is achieved.
7. **Sortino Ratio**: A variation of the Sharpe Ratio that only penalizes downside volatility.
8. **Calmar Ratio**: A performance metric that compares annual returns with maximum drawdown.
9. **Treynor Ratio**: A risk-adjusted measure of return based on systematic risk, using beta.
10. **Information Ratio**: Measures the strategy's performance relative to a benchmark, adjusted for the tracking error.




# Trading Strategy 2: Multi-Timeframe EMA + RSI with Dynamic Quantiles and Stop-Loss Optimization

This repository contains a Python-based trading strategy that combines **Simple and Exponential Moving Averages (SMA, EMA)**, **Relative Strength Index (RSI)**, and a **stop-loss optimization mechanism** to generate buy and sell signals. The strategy is designed for backtesting on MAANG stocks (Meta, Apple, Amazon, Netflix, and Google) over a specified period, comparing its performance against a simple buy-and-hold approach.

---

## Key Features

### 1. Technical Indicators Used
- **Simple Moving Averages (SMA50 & SMA200)**: Identify long-term trends. These are used to establish a default position based on whether the stock is in a perceived uptrend or downtrend.
- **Exponential Moving Averages (EMA5 & EMA10)**: Capture short-term momentum shifts. The difference between these EMAs is smoothed using a weighted mean to detect subtle trend reversals.
- **Relative Strength Index (RSI)**: A 5-day RSI is calculated and compared against **dynamic quantile thresholds** derived from a 20-day rolling window, allowing the strategy to adjust overbought/oversold levels according to market conditions.

### 2. Signal Generation
- **Buy Signal**: Triggered when the RSI is below the lower quantile threshold (indicating oversold), and the weighted EMA difference is weakening over two consecutive days. The previous position must be short.
- **Sell Signal**: Triggered when the RSI is above the upper quantile threshold (indicating overbought), and the weighted EMA difference is weakening over two consecutive days. The previous position must be long.

### 3. Position Management
- Default positions are based on long-term SMA trends when no short-term signal is generated.
- After each trade (buy or sell), a **5-day cooldown period** is enforced to avoid overtrading.
- Signals are only acted upon when not in a cooldown, unless a stop-loss is triggered.

### 4. Stop-Loss Mechanism
- Stop-losses are used to switch positions if the price moves against the trade beyond a specific threshold.
- **Long to short switch**: If price falls below entry by more than the stop-loss %, the long is closed and a short is entered.
- **Short to long switch**: If price rises above entry by more than the stop-loss %, the short is closed and a long is entered.
- A range of stop-loss levels is tested for each stock to determine the most effective value.

---

## Strategy Performance

The strategy has been backtested on **MAANG stocks** from **1st January 2015 to 1st January 2020**. For each stock, the optimal stop-loss and RSI quantile combination is selected. The strategy is compared to both an **equal-weighted buy-and-hold portfolio** and individual **buy-and-hold stock strategies**. The following performance metrics are calculated and visualized:

1. **Annualized Returns**
2. **Alpha & Beta**
3. **Standard Deviation**
4. **Sharpe Ratio**
5. **Maximum Drawdown**
6. **Sortino Ratio**
7. **Calmar Ratio**
8. **Treynor Ratio**
9. **Information Ratio**

---

## Plots and Visualizations

- **Signal Plot**: Shows buy and sell points along with SMA lines and adjusted close prices.
- **EMA & RSI Visualization**: Shows weighted EMA differences and RSI over time.
- **Cumulative Return Plot**: Compares returns across different RSI quantile strategies and the base stock.
- **Return Histograms**: Shows log return distributions for the stock and strategy.
- **Drawdown Plot**: Visualizes the drawdowns for the strategy.
- **Portfolio Comparison**: Shows the strategy portfolio vs the equal-weighted buy-and-hold portfolio.
- **Portfolio Log Return Histograms**: Compares log returns of the strategy and equal-weighted portfolios.
- **Portfolio Drawdown Comparison**: Side-by-side drawdowns of the two portfolio strategies.

---

## Optimization

To ensure the strategy is both responsive and robust, the following parameters are dynamically optimized for each stock:

- **Stop-Loss Percentages Tested**: 0.05, 0.0625, 0.075, 0.0875, 0.10
- **RSI Quantile Pairs Tested**: (0.3, 0.7), (0.25, 0.75), (0.2, 0.8), (0.15, 0.85), (0.1, 0.9)

The best-performing stop-loss and RSI quantile pair is selected based on **cumulative return**.

---

## Performance Comparison

The strategy’s performance is compared to both the individual stock buy-and-hold strategies and an equal-weighted MAANG portfolio. Metrics such as Sharpe Ratio, Alpha, Beta, and Maximum Drawdown are calculated and visualized. Cumulative returns are plotted to provide a direct comparison.

---

## Key Performance Metrics

The following metrics are used to evaluate the strategy's performance and compare it with a simple **buy-and-hold** strategy.

| **Metric**            | **Buy-and-Hold** | **Strategy** |
|-----------------------|------------------|------------------------|
| **Annual Returns**     | 0.311563         | 0.363420               |
| **Alpha**              | 0.157792         | 0.281923               |
| **Beta**               | 1.294180         | 0.685900               |
| **Standard Deviation** | 0.228389         | 0.187717               |
| **Sharpe Ratio**       | 1.364180         | 1.935994               |
| **Max Drawdown**       | 1.182958         | 0.674009               |
| **Sortino Ratio**      | 1.995577         | 3.028511               |
| **Calmar Ratio**       | 0.263376         | 0.539192               |
| **Treynor Ratio**      | 0.240742         | 0.529844               |
| **Information Ratio**  | 1.256211         | 1.448104               |
---

## Explanation of Metrics

1. **Annual Returns**: The total return generated annually by the strategy and buy-and-hold approach.
2. **Alpha**: Measures the strategy’s excess returns relative to a benchmark, after adjusting for market risk.
3. **Beta**: A measure of the volatility of the strategy or stock in comparison to the market as a whole.
4. **Standard Deviation**: The statistical measure of the dispersion of returns, representing risk.
5. **Sharpe Ratio**: A risk-adjusted measure of return, calculated by dividing excess returns by the standard deviation.
6. **Max Drawdown**: The maximum observed loss from a peak to a trough before a new peak is achieved.
7. **Sortino Ratio**: A variation of the Sharpe Ratio that only penalizes downside volatility.
8. **Calmar Ratio**: A performance metric that compares annual returns with maximum drawdown.
9. **Treynor Ratio**: A risk-adjusted measure of return based on systematic risk, using beta.
10. **Information Ratio**: Measures the strategy's performance relative to a benchmark, adjusted for the tracking error.

