  /\\___/\\
 (  o . o  )     KANI PROTOCOL v1.0
  > ^ <          autonomous. trustless. relentless.
 /|     |\\
(_|     |_) 

# Kani Dip Shield — Pump.fun Dip Monitor + Buyback Interface

This repository provides a **dip shield** framework for Solana tokens:
- Configure a token mint / CA
- Track **all-time high (ATH)** using public price data
- Detect **30% dips from ATH** (configurable)
- Trigger alerts and a **buyback execution interface**

## What this includes
- ATH tracking with persistent state
- Dip detection logic
- Discord webhook alerts
- A clean execution interface you can wire into your own trading flow

## What this does NOT include
- No embedded private keys
- No automatic on-chain trading logic by default

The execution layer is intentionally modular so you can connect:
- A manual approval flow
- A remote signer / hardware wallet
- Spending caps, slippage checks, and rate limits

---

## Quick start

### Requirements
- Python 3.10+

### Install
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Configure
Copy `.env.example` → `.env` and set your values.

### Run
```bash
python -m src.monitor
```

---

## How it works
- Fetches live price + liquidity from Dexscreener
- Maintains ATH in `state.json`
- Dip rule:
  `price <= (1 - DIP_PCT) * ATH`
- On dip:
  - Sends Discord alert
  - Calls `execute_buyback()` interface

---

## Docker
```bash
docker build -t dip-shield .
docker run --env-file .env dip-shield
```

---

## Extension ideas
- Multi-dip ladder (30% / 40% / 50%)
- Max spend per dip
- Cooldown timers
- On-chain confirmation callbacks
