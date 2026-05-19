# LTGuardian AML - AI Modeling Module

## Project Overview

This is the AI research and modeling component for LTGuardian AML, an Anti-Money Laundering intelligence system for casino and online gaming operations. The focus is behavioral fingerprinting and transaction anomaly detection.

## Project Scope

This prototype covers:

1. Behavioral fingerprinting model - extract features representing player behavior patterns
2. Transaction anomaly detection - identify suspicious patterns using ML models
3. Risk scoring prototype - combine rule-based and ML approaches
4. Synthetic data generation - realistic transaction datasets for training

## Current Status (Up to Phase 03)

Phase 1-2 completed, Phase 3 completed through behavioral feature engineering.

### Phase 1: Research and Setup (Completed)

- AML concepts and FATF guidelines research
- Online AML/KYC flows analysis (crypto platforms, gaming platforms)
- ML libraries evaluation (scikit-learn, TensorFlow, PyTorch, PyOD)
- AML modeling approaches (behavioral fingerprinting, anomaly detection, risk scoring)

### Phase 2: Data Design (Completed)

- Defined comprehensive data schema for online AML monitoring
- Transaction fields (player_id, session_id, timestamp, amounts, balances)
- Behavioral fields (timing, device, IP, location, game results)
- Player taxonomy (3 normal types, 6 suspicious pattern types)

### Phase 3: Data Generation and Feature Engineering (Completed)

- Implemented synthetic data generation in notebooks/01_data_generation.ipynb
- Simulated 3 normal player behavior types and 6 suspicious AML pattern types
- Generated multi-bank, multi-currency transactions with IBM-style fields:
  - from_bank, to_bank (routing)
  - amount_paid, paying_currency (sender perspective)
  - amount_received, receiving_currency (receiver perspective, FX applied)
  - payment_format (ACH, Wire, Credit Card, Cash, Cheque, Reinvestment, Swish)
- Built a canonical account-event table in notebooks/03_behavior_feature_engineering.ipynb
- Normalized transaction amounts to USD when currency is available
- Engineered behavior features for rhythm, volatility, session activity, and money flow
- Saved final account-level feature table for modeling

## Key Notebooks

- notebooks/01_data_generation.ipynb - synthetic transaction generation
- notebooks/02_early_model_testing.ipynb - early inspection and model experiments
- notebooks/03_behavior_feature_engineering.ipynb - feature engineering pipeline

## Outputs (Current)

- data/aml_synthetic_data.csv - transaction-level log
- data/aml_edges.csv - transaction graph edges
- data/aml_nodes.csv - account node features
- data/aml_behavior_features.csv - engineered account-level behavior features
- data/feature_ablation_results.json - feature ablation results

## How to Re-Run Phase 03

1. Activate the project venv:

```bash
source venv/bin/activate
```

2. Run the feature engineering notebook from repo root:

```bash
jupyter nbconvert --to notebook --execute notebooks/03_behavior_feature_engineering.ipynb --inplace
```


