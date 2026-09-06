# LTGuardian AML - AI Modeling Module

## Project Overview

This is the AI research and modeling component for LTGuardian AML, an Anti-Money Laundering intelligence system for casino and online gaming operations. The focus is behavioral fingerprinting and transaction anomaly detection.

## Project Scope

This prototype covers:

1. Behavioral fingerprinting model - extract features representing player behavior patterns
2. Transaction anomaly detection - identify suspicious patterns using ML models
3. Risk scoring prototype - combine rule-based and ML approaches
4. Synthetic data generation - realistic transaction datasets for training

## Current Status (Up to Phase 05)

Phase 1-3 completed, Phase 4 completed through behavioral fingerprinting and drift detection, and Phase 5 completed through anomaly detection modeling and evaluation.

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

### Phase 4: Behavioral Fingerprinting and Drift Detection (Completed)

- Built behavior representations from the account-level feature table in notebooks/04_behavioral_fingerprinting.ipynb
- Compared multiple clustering approaches for behavioral fingerprints:
  - PCA + KMeans
  - Gaussian Mixture Models
  - UMAP + HDBSCAN
- Evaluated cluster quality with silhouette and Davies-Bouldin scores
- Checked AML enrichment inside clusters using account-level labels
- Ran a supervised probe on PCA embeddings to confirm the fingerprints carry strong fraud signal
- Rebuilt monthly account fingerprints from transaction data for behavior consistency and shift detection
- Measured population drift with PSI, JS divergence, and KS tests
- Measured per-account embedding drift to flag accounts with sudden behavioral changes

### Phase 5: Anomaly Detection (Completed)

- Built anomaly detection experiments in notebooks/05_anomaly_detection.ipynb
- Trained and compared multiple anomaly detection model configurations on engineered behavior features
- Evaluated anomaly scoring behavior to separate suspicious and normal account patterns
- Finalized Phase 5 notebook workflow for repeatable anomaly detection testing

## Key Notebooks

- notebooks/01_data_generation.ipynb - synthetic transaction generation
- notebooks/02_early_model_testing.ipynb - early inspection and model experiments
- notebooks/03_behavior_feature_engineering.ipynb - feature engineering pipeline
- notebooks/04_behavioral_fingerprinting.ipynb - clustering and drift detection for behavior fingerprints
- notebooks/05_anomaly_detection.ipynb - anomaly detection modeling and evaluation

## Outputs (Current)

- data/aml_synthetic_data.csv - transaction-level log
- data/aml_edges.csv - transaction graph edges
- data/aml_nodes.csv - account node features
- data/aml_behavior_features.csv - engineered account-level behavior features
- data/feature_ablation_results.json - feature ablation results

## Phase 4 Highlights

- The behavior feature space was separable enough that PCA + KMeans produced clear clusters with strong AML enrichment.
- The PCA probe classifier showed that the embeddings contain strong signal for separating suspicious from normal accounts.
- Drift analysis showed that timing and activity features changed the most across windows, and a small set of accounts showed very large behavior jumps.
- Together, these results indicate that behavioral fingerprints can be used both for grouping similar accounts and for spotting unusual changes over time.

## How to Re-Run Phase 03

1. Activate the project venv:

```bash
source venv/bin/activate
```

2. Run the feature engineering notebook from repo root:

```bash
jupyter nbconvert --to notebook --execute notebooks/03_behavior_feature_engineering.ipynb --inplace
```

## How to Re-Run Phase 04

1. Activate the project venv:

```bash
source venv/bin/activate
```

2. Run the behavioral fingerprinting notebook from repo root:

```bash
jupyter nbconvert --to notebook --execute notebooks/04_behavioral_fingerprinting.ipynb --inplace
```

## How to Re-Run Phase 05

1. Activate the project venv:

```bash
source venv/bin/activate
```

2. Run the anomaly detection notebook from repo root:

```bash
jupyter nbconvert --to notebook --execute notebooks/05_anomaly_detection.ipynb --inplace
```


