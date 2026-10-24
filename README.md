# LTGuardian AML

## Project overview

This project explores how behavioural analytics can support anti-money laundering monitoring in online gaming and digital payment environments. The work combines synthetic data generation, feature engineering, behavioural fingerprinting, drift analysis, and anomaly detection to build a practical AML detection prototype.

The main presentation for the project is the summary website in [report/index.html](report/index.html). This page is designed to explain the work in a clearer, business-friendly way and highlight the key findings without requiring technical reading.

## Scope of the work

The prototype covers:

1. Synthetic data generation for realistic AML scenarios
2. Behavioural feature engineering from transaction activity
3. Behavioural fingerprinting to group similar account patterns
4. Drift detection to find meaningful changes over time
5. Anomaly detection and risk ranking for investigation prioritisation

## Current status

All project phases are complete:

- Phase 1: Research and setup
- Phase 2: Data design
- Phase 3: Data generation and feature engineering
- Phase 4: Behavioural fingerprinting and drift detection
- Phase 5: Anomaly detection and evaluation

## Phase summary

### Phase 1: Research and setup

- Reviewed AML concepts and monitoring requirements
- Analysed online payment and gaming transaction patterns
- Assessed candidate ML approaches for anomaly detection and behavioural modelling

### Phase 2: Data design

- Defined the transaction and account schema
- Included fields such as timestamps, account identifiers, amounts, currencies, payment methods, and session activity
- Built a player taxonomy with normal and suspicious pattern groups

### Phase 3: Data generation and feature engineering

- Created realistic synthetic transaction data in [notebooks/01_data_generation.ipynb](notebooks/01_data_generation.ipynb)
- Simulated normal and suspicious behaviour patterns
- Engineered account-level behaviour features in [notebooks/03_behavior_feature_engineering.ipynb](notebooks/03_behavior_feature_engineering.ipynb)
- Produced the main data outputs used for downstream modelling

### Phase 4: Behavioural fingerprinting and drift detection

- Built behavioural representations from account features in [notebooks/04_behavioral_fingerprinting.ipynb](notebooks/04_behavioral_fingerprinting.ipynb)
- Compared clustering methods and evaluated separation quality
- Measured drift using PSI and related checks to identify behaviour changes over time
- Focused on timing, volume, and rhythm as the clearest indicators of suspicious shifts

### Phase 5: Anomaly detection

- Built and compared anomaly detection models in [notebooks/05_anomaly_detection.ipynb](notebooks/05_anomaly_detection.ipynb)
- Trained multiple detectors and evaluated their ability to rank suspicious accounts
- Combined outputs into a final risk signal to support investigation prioritisation

## Key notebooks

- [notebooks/01_data_generation.ipynb](notebooks/01_data_generation.ipynb) - synthetic AML data generation
- [notebooks/02_early_model_testing.ipynb](notebooks/02_early_model_testing.ipynb) - early modelling and exploratory testing
- [notebooks/03_behavior_feature_engineering.ipynb](notebooks/03_behavior_feature_engineering.ipynb) - feature engineering
- [notebooks/04_behavioral_fingerprinting.ipynb](notebooks/04_behavioral_fingerprinting.ipynb) - behavioural fingerprinting and drift analysis
- [notebooks/05_anomaly_detection.ipynb](notebooks/05_anomaly_detection.ipynb) - anomaly detection and evaluation

## Main project outputs

- [data/aml_synthetic_data.csv](data/aml_synthetic_data.csv) - transaction-level synthetic data
- [data/aml_edges.csv](data/aml_edges.csv) - transaction graph edges
- [data/aml_nodes.csv](data/aml_nodes.csv) - account-level node information
- [data/aml_behavior_features.csv](data/aml_behavior_features.csv) - engineered behavioural features
- [data/feature_ablation_results.json](data/feature_ablation_results.json) - feature ablation results
- [report/index.html](report/index.html) - final summary website for the project

## Viewing the summary website

To view the project summary locally, open [report/index.html](report/index.html) in a browser. If needed, a simple local server can also be used from the project root:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/report/
```

## Re-running the notebooks

Activate the virtual environment:

```bash
source venv/bin/activate
```

Then run the relevant notebook from the repository root:

```bash
jupyter nbconvert --to notebook --execute notebooks/03_behavior_feature_engineering.ipynb --inplace
```

```bash
jupyter nbconvert --to notebook --execute notebooks/04_behavioral_fingerprinting.ipynb --inplace
```

```bash
jupyter nbconvert --to notebook --execute notebooks/05_anomaly_detection.ipynb --inplace
```

## Overall interpretation

The project demonstrates that suspicious AML activity can be identified through behavioural patterns rather than isolated transaction flags alone. The strongest signals were related to timing, transaction volume, and changes in behaviour over time. This suggests that a monitoring system based on behavioural drift and anomaly scoring could help teams identify the accounts most likely to need closer review and investigation.

