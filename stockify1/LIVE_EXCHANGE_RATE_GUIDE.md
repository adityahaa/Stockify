# Exchange-rate verification procedure

Set STOCKIFY_SECRET_KEY and start Flask from this directory using the root README. Inspect /api/exchange-rate and compare its response with the source used by the implementation. Test network failures in a controlled local environment and verify the displayed fallback. This manual procedure has not been executed in the current review; provider availability and rate freshness remain unverified.

See the [current README](../README.md) and [technical report](../docs/TECHNICAL_REPORT.md). Earlier numerical speedup, confidence, and exchange-rate claims were not backed by committed reproducible benchmarks and have been removed.
