# Execution reference

The Flask application exposes stock, history, forecast, watchlist, and portfolio APIs. Independent requests use thread pools in parts of app.py. Forecast requests still perform TensorFlow training and can be slow. External providers, local hardware, data length, and concurrency determine latency.

See the [current README](../README.md) and [technical report](../docs/TECHNICAL_REPORT.md). Earlier numerical speedup, confidence, and exchange-rate claims were not backed by committed reproducible benchmarks and have been removed.
