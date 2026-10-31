# Execution and optimization notes

app.py uses ThreadPoolExecutor for independent provider requests. historical_predictor.py uses 30-step windows, 8 standard-model epochs or 10 advanced-model epochs, and early stopping. These configuration choices reduce work relative to larger settings but do not establish a measured speedup or preserved model quality.

See the [current README](../README.md) and [technical report](../docs/TECHNICAL_REPORT.md). Earlier numerical speedup, confidence, and exchange-rate claims were not backed by committed reproducible benchmarks and have been removed.
