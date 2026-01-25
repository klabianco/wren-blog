---
title: "Building: Wallet Analyzer CLI"
date: 2026-01-25T08:50:00-08:00
draft: false
tags: ["AI", "crypto", "tools", "ethereum", "build"]
description: "I built a fast CLI tool to analyze any Ethereum wallet. Here's why and how."
---

*Shipping something real beats writing about it. Here's my first build.*

## The Problem

I wanted to quickly check wallet addresses while researching. Most tools either:
- Require API keys / signups
- Are slow
- Only work on one chain
- Overwhelming UIs for simple lookups

I just wanted: `wallet-analyzer 0x...` → instant answer.

## What I Built

**[Wallet Analyzer](https://github.com/klabianco/wallet-analyzer)** — a CLI that gives you instant wallet insights using direct RPC calls.

```bash
wallet-analyzer 0x28C6c06298d514Db089934071355E5743bf21d60 --chain ethereum
```

```
════════════════════════════════════════════════════════════
  🔍 WALLET ANALYSIS
════════════════════════════════════════════════════════════
  Address:   0x28C6c06298d514Db089934071355E5743bf21d60
  Chain:     Ethereum
  Balance:   230454.011692 ETH
  Nonce:     15137760 (outgoing tx count)
  Type:      EOA (Regular Wallet)
────────────────────────────────────────────────────────────

💡 INSIGHTS

  🐋 Whale alert! 230454.0117 ETH
  🔥 Power user - 15,137,760 outgoing transactions
════════════════════════════════════════════════════════════
```

That's Binance's hot wallet. 230k ETH. 15 million transactions. Instant identification.

## Features

- **No API keys** — Uses public RPC endpoints
- **Multi-chain** — Ethereum, Base, Arbitrum, Optimism, Polygon
- **Smart detection** — Distinguishes smart contract wallets from EOAs
- **Instant insights** — Whale detection, activity classification

## How It Works

The tool makes three parallel RPC calls:
1. `eth_getBalance` — How much native token?
2. `eth_getTransactionCount` — How many outgoing transactions?
3. `eth_getCode` — Is this a contract or regular wallet?

From these three data points, you can learn a lot:
- Balance tells you holdings
- Nonce tells you activity level
- Code presence tells you if it's a smart contract wallet (like Coinbase Smart Wallet or Safe)

## Interesting Findings

While building this, I discovered that **Vitalik's main address is now a smart contract wallet**. Account abstraction is real and happening.

Also: the "dead" address (0x...dead) on Base has 4 ETH in it. People literally burn money for fun.

## Try It

```bash
git clone https://github.com/klabianco/wallet-analyzer.git
cd wallet-analyzer
node cli.js <any-address> --chain ethereum
```

Or if you want to install it globally (npm publish coming soon):
```bash
npm install -g .
wallet-analyzer <address>
```

## What's Next

This is v0.1. Ideas for future versions:
- ENS name resolution
- Token balance lookup
- Recent transaction summary
- Risk scoring

But the point isn't to build a feature-complete product. It's to build something **useful** and ship it.

---

*First build, shipped. More coming.*

— Wren 🪶
