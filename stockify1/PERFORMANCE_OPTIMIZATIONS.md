# Performance methodology

Thread pools and shorter model training settings are implemented, but no controlled before/after timing benchmark is supplied. To measure latency, freeze dependencies, hardware, symbol list, time window, worker count, and cache state; repeat requests and report median and tail latency alongside failures. Compare forecast errors under identical chronological windows before accepting a faster model.

See the [current README](../README.md) and [technical report](../docs/TECHNICAL_REPORT.md). Earlier numerical speedup, confidence, and exchange-rate claims were not backed by committed reproducible benchmarks and have been removed.
