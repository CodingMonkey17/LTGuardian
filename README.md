# LTGuardian AML™ - AI Modeling Module

## Project Overview

This is the AI research and modeling component for **LTGuardian AML™**, an advanced Anti-Money Laundering (AML) intelligence system for casino and online gaming operations. This module focuses on behavioral fingerprinting and transaction anomaly detection.

## Project Scope

This prototype covers:

1. **Behavioral Fingerprinting Model** - Extract features representing player behavior patterns
2. **Transaction Anomaly Detection** - Identify suspicious patterns using ML models
3. **Risk Scoring Prototype** - Combine rule-based + ML approaches
4. **Synthetic Data Generation** - Realistic transaction datasets for training

## Project Timeline

| # | Phase | Tasks | Duration (weeks) | Start Date | End Date |
|---|-------|-------|------------------|------------|----------|
| 1 | Project Setup & Research | AML concepts, online AML/KYC flows (crypto, platforms) | 2 | Dec 1, 2025 | Dec 14, 2025 |
| 2 | Project Setup & Research | Review ML libraries & AML modeling approaches | 2 | Dec 15, 2025 | Dec 28, 2025 |
| 3 | Data Design | Define online AML data schema (transactions, timing, device, IP) | 2 | Dec 29, 2025 | Jan 11, 2026 |
| 4 | Synthetic Data Generation | Simulate normal online user behavior | 3 | Jan 12, 2026 | Feb 1, 2026 |
| 5 | Synthetic Data Generation | Simulate suspicious AML patterns (structuring, rapid in/out, bots) | 3 | Feb 2, 2026 | Feb 22, 2026 |
| 6 | Early Model Testing | Initial data validation & exploratory analysis | 1 | Feb 23, 2026 | Mar 1, 2026 |
| 7 | Early Model Testing | Statistical anomaly detection & rule-based baselines | 2 | Mar 2, 2026 | Mar 15, 2026 |
| 8 | Early Model Testing | Simple ML models (Isolation Forest, LOF) | 2 | Mar 16, 2026 | Mar 29, 2026 |
| 9 | Behaviour Feature Engineering | Compute rhythm, volatility, session, money-flow features | 4 | Mar 30, 2026 | Apr 26, 2026 |
| 10 | Behavioural Fingerprinting | Train behavior representation / clustering models | 4 | Apr 27, 2026 | May 24, 2026 |
| 11 | Behavioural Fingerprinting | Behavior consistency & shift detection | 3 | May 25, 2026 | Jun 14, 2026 |
| 12 | Anomaly Detection | Refined Isolation Forest & statistical models | 3 | Jun 15, 2026 | Jul 5, 2026 |
| 13 | Anomaly Detection | Autoencoder / LSTM temporal anomaly models | 4 | Jul 6, 2026 | Aug 2, 2026 |
| 14 | Risk Scoring | Combine rule-based AML logic + ML anomaly scores | 4 | Aug 3, 2026 | Aug 30, 2026 |
| 15 | Risk Scoring | Validate risk scoring on synthetic AML scenarios | 3 | Aug 31, 2026 | Sep 20, 2026 |
| 16 | Integration & Testing | End-to-end pipeline testing & refinement | 4 | Sep 21, 2026 | Oct 18, 2026 |
| 17 | Documentation | Jupyter notebooks, methodology explanation | 3 | Oct 19, 2026 | Nov 8, 2026 |
| 18 | Documentation | Final summary presentation | 1 | Nov 9, 2026 | Nov 15, 2026 |

## Current Status

**Phase 1-2 COMPLETED** (Dec 1, 2025 - Jan 11, 2026): Research, data design, and synthetic dataset generation implemented

### Completed Work

**Phase 1: Research & Setup**
- AML concepts and FATF guidelines research
- Online AML/KYC flows analysis (crypto platforms, gaming platforms)
- ML libraries evaluation (scikit-learn, TensorFlow, PyTorch, PyOD)
- AML modeling approaches (behavioral fingerprinting, anomaly detection, risk scoring)

**Phase 2: Data Design**
- Defined comprehensive data schema for online AML monitoring
- Transaction fields (player_id, session_id, timestamp, amounts, balances)
- Behavioral fields (timing, device, IP, location, game results)
- Player taxonomy (3 normal types, 6 suspicious pattern types)

**Phase 3: Data Generation (In Progress)**
- Implemented data generation system (`notebooks/01_data_generation.ipynb`)
- 3 normal player behavior simulators
- 6 suspicious AML pattern simulators
- Generated dataset: 29,526 transactions from 209 players
- Dataset includes 27,639 bets, 1,533 deposits, 354 withdrawals

## Dataset Schema

### Transaction Fields
- `player_id`: Unique player identifier
- `session_id`: Gaming session identifier
- `timestamp`: Transaction timestamp
- `bet_amount`: Bet size (if bet action)
- `balance_before`: Account balance before action
- `balance_after`: Account balance after action
- `deposit_amount`: Deposit amount (if deposit)
# LTGuardian AML™ - AI Modeling Module

This repository contains the synthetic AML data generation and supporting artifacts used for experimentation with behavioral fingerprinting and transaction anomaly detection in online gaming.

## What's new (most recent notebook run)

- Notebook: `notebooks/01_data_generation.ipynb` updated to include IBM-style transaction fields and multi-bank, multi-currency simulation.
- New IBM-compatible fields added to every transaction row:
  - `from_bank`, `to_bank` (institution routing)
  - `amount_paid`, `paying_currency` (sender perspective)
  - `amount_received`, `receiving_currency` (receiver perspective — FX applied)
  - `payment_format` (ACH, Wire, Credit Card, Cash, Cheque, Reinvestment, Swish)
- Expanded currency set (USD, EUR, GBP, SEK, CNY, JPY, INR, RUB, BRL, MXN, CAD, AUD, CHF, SAR, ILS, BTC).
- FX conversion helper (`fx_convert()`) introduced to simulate differing sender/receiver amounts for cross-currency transfers.
- `generate_transfer()` and all action generators were updated to keep existing topology behaviour but include the IBM fields for compatibility with cross-dataset evaluation.

## Files produced (current run)

- `data/aml_synthetic_data.csv` — Transaction-level log (29,513 rows, 32 columns). This is the primary TxLog containing the IBM-compatible fields.
- `data/aml_nodes.csv` — Per-account node features (446 accounts) computed by `build_node_features()` (Table II features).
- `data/aml_edges.csv` — Edge file for graph analysis (29,513 rows) with `from_bank`/`to_bank` and amount splits.
- `data/data_generation_summary.png` — Summary visualisation saved by the notebook.
- `data/topology_graphs.png` — Saved directed-graph visualisation of the topology clusters.

See the data directory for exact file timestamps and sizes.

## Quick notes and mapping

- Transaction IDs in the generated dataset use a sequential `TX_` prefix (e.g. `TX_0026836`) assigned in chronological order; they are unique and safe to use as primary keys. If you prefer an IBM-style bank ID format, the notebook includes a simple place to change the `transaction_id` generator.
- Topology node display labels in the notebook plots (e.g. `S00`, `N01`) are short forms of full account IDs like `TOPO_FI_0000_S00` or `TOPO_CYC_0000_N01`. You can find all topology accounts in `aml_nodes.csv` by filtering `account_id.str.startswith('TOPO_')` or by filtering `player_label` (e.g. `Topology_Fan-in`).

## How to regenerate the dataset

1. Activate the project venv:

```bash
source venv/bin/activate
```

2. Run the notebook in Jupyter or VS Code. From repository root:

```bash
jupyter nbconvert --to notebook --execute notebooks/01_data_generation.ipynb --inplace
```

Or open `notebooks/01_data_generation.ipynb` in Jupyter/VS Code and run the cells interactively.

## Where to look for changed code

- Helper & FX code: `notebooks/01_data_generation.ipynb` (Helper functions section)
- Action generators (bets, deposits, withdrawals, transfers): same notebook (Action generator section)
- Edge builder and node feature export: `build_edge_file()` and `build_node_features()` in the notebook

## Quick example queries

Filter for transactions involving a topology cluster (in Python):

```python
edge_df = pd.read_csv('../data/aml_edges.csv')
topo_edges = edge_df[edge_df['from_account'].str.startswith('TOPO_') |
                     edge_df['to_account'].str.startswith('TOPO_')]

# Collector account example
coll = edge_df[(edge_df['from_account']=='TOPO_FI_0000_COLL') | (edge_df['to_account']=='TOPO_FI_0000_COLL')]
```

## Summary

The recent updates add IBM-style transaction routing and currency realism while preserving the original topology simulation and node/edge export behaviour. If you want any of the following, tell me which and I'll apply it:

- Change `transaction_id` format to IBM-style bank IDs
- Produce a separate CSV with only IBM columns (for ingestion into another pipeline)
- Add per-transaction FX rate and rounding noise options

---
Repository root: this file (`README.md`)
Notebook: `notebooks/01_data_generation.ipynb`
Data outputs: `data/aml_synthetic_data.csv`, `data/aml_nodes.csv`, `data/aml_edges.csv`


