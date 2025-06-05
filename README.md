# Trading Strategy: Combining Bollinger Bands, RSI, and ATR for MAANG Stocks

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
