# Indian Stocks — RSI + MACD Dashboard

A Streamlit dashboard that highlights "Fully Bullish" and "Weak / Oversold"
NSE stocks and shows a full RSI + MACD breakdown (Daily / Weekly / Monthly)
for your watchlist, using free live data from Yahoo Finance (`yfinance`).

## 1. One-time setup (5 minutes)

You need Python installed on your computer.

1. **Install Python** (skip if you already have it):
   Go to https://www.python.org/downloads/ and install the latest version.
   On Windows, tick **"Add Python to PATH"** during install.

2. **Put these three files in one folder** on your computer:
   - `app.py`
   - `requirements.txt`
   - `README.md` (this file)

3. **Open a terminal in that folder**:
   - Windows: open the folder, click the address bar, type `cmd`, press Enter.
   - Mac: right-click the folder → "New Terminal at Folder" (or open Terminal and `cd` into it).

4. **Install the required packages** (one-time, or whenever you update):
   ```
   pip install -r requirements.txt
   ```
   If `pip` isn't recognized, try `pip3` or `python -m pip install -r requirements.txt`.

## 2. Run the dashboard

In the same terminal:
```
streamlit run app.py
```

This will automatically open the dashboard in your web browser at
`http://localhost:8501`. Every time you want to view it again, just repeat
this command from the folder.

## 3. Using the dashboard

- **Refreshing data**: The page pulls fresh data every 5 minutes automatically,
  or press **"🔄 Force refresh"** in the left sidebar to fetch immediately.
- **Editing your watchlist**: In the sidebar, edit the text box — one line per
  stock, in the format `TICKER.NS : Display Name`. NSE tickers always end in
  `.NS` (e.g. `RELIANCE.NS`, `TCS.NS`, `INFY.NS`). You can find the correct
  ticker for any stock by searching it on https://finance.yahoo.com.
- **Cards**: "Fully Bullish" = RSI > 60 and MACD above its signal line on
  Daily, Weekly, and Monthly all at once. A "Watch" badge means Weekly +
  Monthly are bullish but Daily hasn't caught up yet. "Weak" = Daily RSI < 40
  with MACD below signal.

## Notes & limitations

- **Data delay**: Yahoo Finance's free data for NSE is typically delayed by
  roughly 15 minutes — it is not tick-by-tick real-time. There is no free,
  truly real-time NSE data source; for true real-time data you'd need a paid
  broker API (e.g. Zerodha Kite Connect, Upstox, ICICI Breeze).
- **RSI/MACD math**: RSI uses Wilder's smoothing (14-period), the same method
  most charting platforms use. MACD uses the standard 12/26/9 EMA settings.
  Weekly and Monthly values are computed by resampling daily candles, not by
  fetching separate weekly/monthly data (Yahoo's raw weekly/monthly history is
  shorter and less reliable for indicator warm-up).
- **This is not investment advice.** RSI/MACD are lagging technical
  indicators and can give false signals; always do your own research.

## Troubleshooting

- **"Could not fetch data for: XYZ.NS"** — double check the ticker on Yahoo
  Finance; some ETFs/small-caps use slightly different symbols.
- **Blank/slow first load** — the first fetch for each ticker pulls 3 years of
  daily history; subsequent loads are cached for 5 minutes and much faster.
- **Command not found errors** — make sure Python was added to PATH during
  installation (see step 1), then restart your terminal.
