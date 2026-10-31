# Stockify application source

This folder contains the Flask application, Jinja templates, and historical, sentiment, hybrid, and currency modules. See the [repository README](../README.md) for correct setup, attribution, and feature coverage, and the [technical report](../docs/TECHNICAL_REPORT.md) for evaluation limitations.

Run `python app.py` from this directory after installing `requirements.txt` and setting `STOCKIFY_SECRET_KEY`. The server listens on http://127.0.0.1:5000. No verified public deployment or benchmark is supplied. The other optimization/currency notes are historical implementation notes; their speed and accuracy claims have not been remeasured.
