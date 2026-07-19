# Workplace EV Charging: Behavioral Analytics, Forecasting, and Quantum–Classical Control

Reproducible code for an end-to-end study of workplace electric-vehicle (EV) charging, spanning tariff-threshold behavior, user profiling, leakage-aware prediction, chronological load forecasting, dynamic-pricing control, quantum–classical benchmarks, and distribution-feeder evaluation.

## Overview

This repository accompanies the manuscript:

> **Price Response, Demand Forecasting and Hybrid Quantum–Classical Pricing Control of Workplace Electric-Vehicle Charging**

The workflow analyzes a public workplace-charging dataset and connects behavioral evidence to predictive, prescriptive, and power-system analyses. It was designed to keep empirical findings distinct from conditional simulations and to make every reported table, figure, configuration, and principal result auditable.

## Main contributions

- Estimates excess mass immediately below a four-hour free-charging threshold, with session and user-cluster bootstraps, specification sensitivity, placebo cutoffs, and a local density-jump diagnostic.
- Builds activity-based user segments without defining clusters by the fee outcome later used for interpretation.
- Separates strict unseen-user classification from chronological returning-user prediction and controls outcome-history leakage.
- Reconstructs hourly charging demand and evaluates forecasts with rolling-origin validation and seasonal-naive baselines.
- Compares flat, constant-price, time-of-use, and tabular reinforcement-learning policies in a dynamic-pricing environment with deferred demand and capacity penalties.
- Evaluates matched quantum and classical learning benchmarks across folds and seeds, including finite-shot and depolarizing-noise diagnostics.
- Reproduces the Q-EVCS pricing experiment with a five-qubit variational Q-function and a matched-budget classical comparator.
- Propagates charging policies and forecast errors through an IEEE 33-bus distribution-feeder benchmark to evaluate voltage, line loading, losses, and overloads.

## Repository contents

```text
.
├── EV_Charging_Quantum_Revised.ipynb   # Complete Google Colab workflow
└── README.md                           # Repository documentation
```

The notebook generates its own organized output tree:

```text
MyDrive/Outputs/EV_Charging_Quantum/
├── Figures/             # Publication figures in PNG and PDF
├── Tables/              # Result tables in CSV and XLSX
├── Models/              # Saved model-related artifacts
├── outputs_summary.txt  # Human-readable principal results and caveats
├── run_configuration.json
└── output_inventory.csv
```

## Data

The notebook expects the public workplace-charging data file to be named:

```text
station_data_dataverse.csv
```

The preferred Google Drive location is:

```text
MyDrive/Datasets/Energy/station_data_dataverse.csv
```

Several fallback locations are searched automatically. The data are not redistributed in this repository; users should obtain them from their original public source and comply with the source terms.

## Quick start in Google Colab

1. Add `EV_Charging_Quantum_Revised.ipynb` to the repository.
2. Open the notebook in Google Colab.
3. Place `station_data_dataverse.csv` in the preferred Google Drive location shown above.
4. Run the cells sequentially and authorize Google Drive mounting when requested.
5. Review `outputs_summary.txt`, `run_configuration.json`, and `output_inventory.csv` after execution.

The setup cell installs packages that may be absent from a standard Colab runtime:

```python
!pip -q install pennylane pennylane-lightning xgboost openpyxl tabulate pandapower
```

The classical workflow requires NumPy, pandas, SciPy, scikit-learn, XGBoost, Matplotlib, Seaborn, OpenPyXL, and pandapower. The quantum experiments additionally require PennyLane and PennyLane-Lightning.

## Runtime options

The main configuration switches are defined near the beginning of the notebook:

```python
SEED = 42
RUN_QUANTUM = True
FAST_MODE = False
```

- Set `FAST_MODE = True` for a shortened smoke test.
- Set `RUN_QUANTUM = False` for a classical-only run.
- Retain `FAST_MODE = False` when producing manuscript-facing results.

Google Colab CPU is sufficient for the classical sections. The full multi-fold, multi-seed quantum benchmarks require additional runtime.

## Reproducibility design

The workflow uses a fixed random seed, user-disjoint folds where required, chronological validation for forecasting, user-cluster resampling for dependent observations, matched subsets and budgets for quantum–classical comparisons, and multi-seed policy evaluation. Tables are saved in both CSV and Excel formats, while figures are exported as high-resolution PNG and vector PDF files.

## Interpretation boundaries

- Bunching below four hours is evidence consistent with response to the tariff rule; it is not definitive causal identification.
- The bunching result does not identify a continuous price elasticity. Pricing results are therefore sensitivity analyses over assumed elasticities.
- Hourly demand is reconstructed from charging sessions and is not interval-metered feeder demand.
- Pricing-control results are conditional simulations.
- Grid impacts are evaluated on a standard IEEE 33-bus benchmark, not the unidentified feeder serving the observed workplace.
- Quantum experiments are simulator benchmarks. No quantum advantage or hardware readiness is claimed.

## Authors

- Sunawar Khan
- Rahma Zayoud
- Ibrahim Alreshidi
- Sghaier Guizani
- Habib Hamam

## Citation

If this repository supports your work, please cite the accompanying manuscript. Complete journal, DOI, and publication metadata should be added here once available.

```bibtex
@article{KhanWorkplaceEVCharging,
  title   = {Price Response, Demand Forecasting and Hybrid Quantum--Classical Pricing Control of Workplace Electric-Vehicle Charging},
  author  = {Khan, Sunawar and Zayoud, Rahma and Alreshidi, Ibrahim and Guizani, Sghaier and Hamam, Habib},
  note    = {Manuscript}
}
```

## License and data terms

No software license has yet been specified. Before public release, the authors should add a `LICENSE` file stating the permitted uses of the code. The dataset remains governed by the terms of its original source.

## Contact

For questions about the study or its implementation, please contact the corresponding authors through the affiliations provided in the accompanying manuscript.
