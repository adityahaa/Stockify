# Currency conversion implementation

app.py and models/currency_utils.py contain conversion logic. Indian symbol suffixes are handled separately from foreign symbols; foreign price arrays are converted to INR. External rate responses and fallback values are application inputs, not guaranteed executable market quotes. The two implementations should be reconciled before relying on consistent rates across views.

See the [current README](../README.md) and [technical report](../docs/TECHNICAL_REPORT.md). Earlier numerical speedup, confidence, and exchange-rate claims were not backed by committed reproducible benchmarks and have been removed.
