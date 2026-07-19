# Alpaca API — Basic Usage Reference

## Overview

A reference notebook covering the fundamental operations of the Alpaca brokerage API — live market data retrieval, account management, and order placement. Built during my time as a Python Developer at a remote trading platform startup (2020–2021).

This notebook serves as the foundational API layer. The production trading system built on top of these foundations is available in the [AlpacaTradingBot](https://github.com/tanjilh136/AlpacaTradingBot) repository.

---

## What This Notebook Covers

### Account & Asset Information
- Retrieve full account details (buying power, equity, balance change)
- Look up any ticker symbol to get company name and shortability status

### Live Market Data
- Fetch real-time bar data (OHLCV) for any ticker
- Retrieve last 30 minutes of live trade data via custom pagination
- Calculate recommended order quantity using a 30-minute weighted price formula:
  - Splits 30-minute window into three 10-minute segments
  - Applies weighted average (3x first segment, 2x second, 1x third)
  - Floors result to a safe integer quantity

### Order Placement
Three order types supported for both buy and sell:

| Order Type | Description |
|------------|-------------|
| Market | Immediate execution at current market price |
| Limit | Execute only at specified price or better |
| Stop-Limit | Trigger price + limit price combination |

### Order Management
- List all open orders
- Fetch order details by order ID or client order ID
- Cancel a specific order by ID
- Cancel all open orders simultaneously
- Retrieve activity history (filled orders, trade log)

---

## Setup

```python
API_KEY = 'your_api_key_here'
SECRET_KEY = 'your_secret_key_here'
BASE_URL = 'https://paper-api.alpaca.markets'  # paper trading
# BASE_URL = 'https://api.alpaca.markets'       # live trading
```

> Always use the paper trading URL for testing. Switch to live only when intentionally trading with real funds.

---

## Installation

```bash
pip install alpaca-trade-api pandas numpy
```

---

## Important Notes

**Credentials:** Never commit API keys to version control. Use environment variables or a `.env` file with `.gitignore`. All credentials in this notebook are placeholders.

**Paper Trading:** All development and testing was done against Alpaca's paper trading environment — no real money involved.

**Deprecation:** `fit_generator` and some older Alpaca API patterns used here may differ from current Alpaca API versions. Refer to the [official Alpaca docs](https://docs.alpaca.markets) for the latest SDK usage.

---

## Relationship to Production Systems

This notebook was the starting point. The structured production systems built from this foundation:

- **[AlpacaTradingBot](https://github.com/tanjilh136/AlpacaTradingBot)** — automated trading bot with WebSocket data feed, strategy engine, and order execution layer
- **[PolygonSMSBot](https://github.com/tanjilh136/PolygonSMSBot)** — real-time price alert system via Telegram and SMS

---

## Tech Stack

- **Language:** Python
- **Brokerage:** Alpaca Trade API
- **Data:** pandas · NumPy
- **Environment:** Google Colab

---

## Author

**Tanjil Hasan**
github.com/tanjilh136 · linkedin.com/in/tanjil-hasan-650246169
