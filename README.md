# Stockify

A Flask application for exploring stock histories, watchlists, portfolios, and experimental price forecasts. The original application files are in [`stockify1/`](stockify1/). This is a software and modeling demonstration; predictive usefulness has not been established.

## Problem and implemented features

The project brings price exploration and multiple forecast approaches into one interface:

- JSON-backed registration/login, watchlist management, and portfolio entries.
- Historical prices and company data fetched through Yahoo Finance using `yfinance`.
- Standard and bidirectional LSTM options with technical price/volume features.
- TextBlob news sentiment with scraping and market-performance fallbacks.
- A heuristic hybrid forecast combining historical and sentiment outputs.
- USD/INR conversion with external rate sources and fallback values.

This is **Flask**, not Streamlit. Data depends on provider responses and is not guaranteed to be real time. Sentiment and portfolio features are already present; they are not future-only features.

## Architecture and models

`app.py` defines browser routes and JSON APIs. Jinja templates render the interface. `models/historical_predictor.py` creates technical features, 30-step input windows, an 80/20 chronological sequence split, and on-request TensorFlow training. `sentiment_analyzer.py` retrieves news and applies TextBlob polarity. `hybrid_predictor.py` weights outputs using heuristic error/confidence quantities. `currency_utils.py` handles currency conversion.

The historical model requests two years of data and uses close, volume, moving averages, RSI, MACD, signal line, volume ratio, momentum, and volatility. There is no versioned training dataset or saved benchmark in this repository.

## Local setup

Use Python 3.11 for the supplied TensorFlow/NumPy pins. From PowerShell:

```powershell
git clone https://github.com/adityahaa/Stockify.git
cd Stockify
py -3.11 -m venv .venv
.venv\Scripts\python.exe -m pip install -r stockify1/requirements.txt
$env:STOCKIFY_SECRET_KEY = (py -3.11 -c "import secrets; print(secrets.token_hex(32))")
cd stockify1
..\.venv\Scripts\python.exe app.py
```

Open http://127.0.0.1:5000. Run from `stockify1` because runtime JSON paths are relative to the working directory. No public deployment is verified. Network access is required for stock/news/currency requests; forecast requests train models and can take time.

## Evaluation and limitations

Read the [technical report](docs/TECHNICAL_REPORT.md) before interpreting model outputs. Existing MAE/RMSE are calculated on scaled targets and then passed through currency conversion; they are not valid price-unit error measurements. The scaler is fit before the train/test split. The displayed confidence and risk scores are heuristics, not calibrated probabilities. No measured accuracy, trading profit, latency improvement, or superiority over a persistence baseline is claimed.

Accounts store plaintext passwords in a local JSON file; the development server enables debugging. Use synthetic credentials and data locally. Public hosting requires authentication/storage hardening, CSRF protection, concurrency review, and a deployment configuration. Forecast dates include calendar days and recursively hold other features fixed.

## Attribution

The original README credits **Kaustubh J.** and links [kaustubhj18/Stockify](https://github.com/kaustubhj18/Stockify). That attribution is retained here; repository ownership does not establish sole authorship. Aditya Hambire maintains this copy. Existing Git history is preserved. No additional rights or third-party data redistribution license is asserted.

Current checks and unresolved prerequisites: [verification record](docs/VERIFICATION.md).
