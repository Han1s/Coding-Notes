# VII. Configure and Run

- configure **Telegram**
  - On telegram communicate to **BotFather**
  - need to create a bot with it
  - open then **@get_id_bot** and type **/my_id** to get your id
- Configure **Binance**
- Configure bot

## 32. Dry run

- `python3 ,/freqtrade/main.py -c config.json` 
  - to run the bot
- `python3 ./freqtrade/main.py -c config.json --dynamic-whitelist 100` 
  - looks for pairs based on top 100 pairs.
- to get the testdata
  - `cp freqtrade/tests/testdata/pairs.json user_data/data/binance/`
  - `python scripts/download_backtest_data.py --exchange binance --days 90 -t 1h`
  - or `python3 ./freqtrade/main.py -c config.json -s BBRSI backtesting --refresh-pairs-cached`
  - or `python3 ./freqtrade/main.py -c config.json -s BBRSI backtesting --refresh-pair`
- run `python3 ./freqtrade/main.py -c config.json -s BBRSI --dynamic-whitelist 200`

# VIII. Strategy Implementation

- based on two indicators
  - **Bullinger Bands** (BB)
  - Only buy if RSI is over 30 however
  - **Buy** - We also want the price of the coin to go below 2 Σ of BB
  - **Sell** - The price has to be bigger than middle band

## 37. Backtesting & Plotting results

- to plot a pair:

  ```bash
  python3 ./scripts/plot_dataframe.py -s BBRSI -p LINK/BTC
  ```

- if you define indicators in your strategy you can also call them in the plot

  ```bash
  python3 ./scripts/plot_dataframe.py -s BBRSI -p ADA/BTC --indicators1 bb_lowerband,bb_middleband,bb_upperhand --indicators2 rsi
  ```

## 38. Parameters to optimize

- you wanna check your **sharp ratio**

## 39. Hyperoptimization

- lecture 38 not working, definitely check the example hyperopt.py and the related docs.

# Indicators info

- **standard deviation of 1** is 68%
- **standard deviation of 2** is 95%
- **RSI** - relative strength Index
  - Whether something is overbought or oversold by looking at red / green candles
  - the closer to 100 the more green candles and closer to 0 the closer the red candles
  - Below 30 something is oversold
  - Above 70 means something is overbought
- **Bullinger Bands** track average and two standard deviations
  - if the prices are volatile the bands widen up
- **Sharp ratio**
  - return on your portfolio divided by your standard deviation of your portfolio
  - e.g. 20% / 10% = 2
  - For day trader its (**daily return** divided by your **standard deviation**)  * √365
  - We want something more than 2
  - We never want to trade less than one

