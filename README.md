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
- `withdraw_amount`: Withdrawal amount (if withdrawal)

### Behavioral Fields
- `game_result`: Win/Lose outcome
- `device`: Device type (iPhone, Android, PC, ETG)
- `ip_address`: IP address
- `location`: Geographic location (Macau, US, EU, VPN)
- `time_since_last_action`: Seconds between actions
- `bet_direction`: Bet type (player/banker/tie for Baccarat)

### Labels
- `player_label`: Detailed player type classification
- `is_suspicious`: Boolean flag for suspicious behavior

## Player Types Simulated

### Normal Players (Baseline Behavior)

1. **Normal Type A - Casual Low Bettor**
   - Small bets (10-50)
   - Slow rhythm (5-12 seconds between bets)
   - Linear deposit/withdraw patterns
   - No sudden spikes

2. **Normal Type B - Medium Stable Bettor**
   - Consistent range (50-200)
   - Mild variance
   - Long stable sessions (20-40 minutes)

3. **Normal Type C - Hot/Cold Player**
   - Behavioral swings based on wins/losses
   - Higher variance
   - Chase behavior after losses

### Suspicious Players (AML Risk Patterns)

1. **Structuring Behavior**
   - 20+ small deposits just under reporting thresholds (700-950)
   - Minimal gameplay
   - Quick withdrawal

2. **Rapid In/Out**
   - Large deposit (8,000-12,000)
   - 5-10 minimal bets
   - Immediate withdrawal of 95-98%

3. **High Volatility Spike**
   - Normal betting baseline (30-70)
   - Sudden massive bets (3,000-6,000)
   - Return to normal

4. **Coordinated Accounts**
   - Multiple accounts with identical betting rhythm
   - Same IP range
   - Shared device patterns

5. **Bot-Like Behavior**
   - Perfectly consistent timing (exact intervals)
   - No variance in bet amounts
   - No emotional variation

6. **Crypto Laundering**
   - VPN/crypto deposits
   - Intentional losses (70% loss rate)
   - Withdrawal via different method

## Repository Structure

```
aml/
├── README.md                           # This file
├── data/
│   ├── aml_synthetic_data.csv         # Generated dataset (4.8 MB)
│   └── data_generation_summary.png    # Visualization of data patterns
├── notebooks/
│   └── 01_data_generation.ipynb       # Data generation notebook
├── src/                                # Future: feature extraction, models
└── venv/                               # Python virtual environment
```

## Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook/Lab
- Required packages: `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`

### Installation

```bash
# Activate virtual environment
source venv/bin/activate

# Install dependencies (if needed)
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

### Running the Notebook

```bash
cd notebooks
jupyter notebook 01_data_generation.ipynb
```

Or open directly in VS Code with Jupyter extension.

## Usage

### Generate New Dataset

The notebook is organized into sections:

1. **Import libraries** - Load required Python packages
2. **Helper functions** - Random data generators
3. **Action generators** - Bets, deposits, withdrawals
4. **Normal player simulators** - 3 baseline behavior types
5. **Suspicious player simulators** - 6 AML risk patterns
6. **Dataset generation** - Combine all player types
7. **Statistics & visualization** - Analyze results

### Customization

Adjust dataset parameters in the main generation cell:

```python
df = generate_full_dataset(
    num_normal_A=50,              # Casual low bettors
    num_normal_B=50,              # Medium stable bettors
    num_normal_C=50,              # Hot/cold players
    num_suspicious_structuring=10,
    num_suspicious_rapid=10,
    num_suspicious_spike=10,
    num_suspicious_bot=8,
    num_suspicious_crypto=8,
    num_coordinated_groups=5      # Groups of 2-3 accounts
)
```

## Data Quality Features

**Realistic Patterns**: Simulated from actual casino behavior patterns  
**Noise & Variance**: Random jitter in timing and amounts  
**Game-Agnostic**: Based on financial behavior, not game rules  
**Balanced Dataset**: Mix of normal (72%) and suspicious (28%) players  
**Rich Metadata**: Device, IP, location, timing information  
**Labeled Ground Truth**: Clear labels for supervised learning

## Design Approach

### Game-Agnostic Design

AML modeling focuses on financial behavior patterns rather than game-specific rules. The approach captures:
- Betting patterns and deposit/withdrawal cycles
- Transaction timing and rhythm
- Device and IP patterns
- AML red flags consistent across game types

### Synthetic Data Methodology

The implementation generates realistic synthetic data by:
- Applying domain knowledge of actual AML patterns
- Incorporating behavioral variance and noise
- Simulating known money laundering techniques
- Including contextual metadata (devices, IPs, locations)

## Technical Implementation

### Data Schema Structure

**Transaction Actions**: Each row represents a single action (bet, deposit, or withdrawal). Fields not applicable to the action type contain null values, maintaining data normalization.

**Time-Series Design**: The schema supports temporal analysis through timestamp ordering, inter-transaction timing capture, and session-based grouping.

**Behavioral Context**: Rich metadata enables multi-dimensional analysis including device fingerprinting, IP geolocation, balance tracking, and session consistency checks.

### Player Behavior Simulation

**Normal Behaviors**: Three types representing casual low bettors, medium stable bettors, and hot/cold players with variance.

**Suspicious Patterns**: Six AML risk patterns based on FATF guidelines and casino AML best practices - structuring, rapid in/out, volatility spikes, coordinated accounts, bot behavior, and crypto laundering.

## References

- **AML Standards**: FATF guidelines and international AML regulations
- **Behavioral Modeling**: Transaction-level approach for real-time monitoring
- **Future Integration**: Designed for GRIP-AML API and LTGuardian ecosystem

---

**Last Updated**: January 2026  
**Version**: 0.1.0 (Phase 1-2 Complete)
   