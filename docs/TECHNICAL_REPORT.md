# Stockify technical report

## Problem and architecture

Stockify integrates market exploration and experimental forecast pipelines in a Flask/Jinja application. app.py owns authenticated routes, provider calls, and JSON user/watchlist/portfolio persistence. The historical, sentiment, hybrid, and currency modules separate modeling and data access. No Streamlit entry point exists.

## Dataset and models

HistoricalPredictor requests two years of Yahoo Finance history per symbol, engineers rolling price/volume features, drops incomplete rows, min-max scales features, and builds 30-observation sequences. It splits sequences chronologically at 80%, trains a standard LSTM for up to 8 epochs or an advanced bidirectional stack for up to 10, and uses early stopping on training loss. A 5% internal validation split is requested. No fixed data snapshot, seed, or saved trained model is supplied.

TextBlob polarity and scraped news feed a heuristic sentiment path; fallback summaries/signals are not independently verified journalism. The hybrid normalizes inverse historical MAE and sentiment confidence as weights. Such quantities have incompatible statistical meanings and have not been calibrated.

## Evaluation findings

The implementation fits its scaler on the full dataset before splitting, leaking test distribution information. It computes MAE/RMSE on scaled close values, then currency-converts those errors without inverse-scaling them. Consequently displayed price-unit errors and derived confidence/weighting should not be treated as valid predictive evidence. R-squared alone does not demonstrate useful out-of-sample price forecasts. Recursive forecasts reuse non-close features and generate calendar-day dates.

No frozen price dataset or genuine measured baseline result is committed. A defensible future comparison should freeze ticker/date/adjustment conventions, fit preprocessing on training data only, use a separate chronological validation window, inverse-transform targets before computing MAE/RMSE, and compare next-step forecasts against the previous observed close on identical test timestamps. Compare the hybrid and each component on the same frozen windows; do not tune on the final test. That experiment has not been run in this review.

## Functional reproduction and limitations

Follow the root README with Python 3.11 and run from stockify1. Manually verify synthetic signup/login, watchlist add/remove, portfolio add/remove, and a provider-backed stock request before forecasting. No complete dependency install, provider run, training benchmark, or public deployment is claimed here. Plaintext local passwords, debug serving, provider changes, and JSON concurrency limit deployment suitability. Earlier optimization notes are historical claims, not current measured results. See [verification record](VERIFICATION.md) for executed checks. Original README attribution to Kaustubh J. is preserved in the root README.
