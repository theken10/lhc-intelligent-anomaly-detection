# LHC Intelligent Anomaly Detection

An offline scientific machine-learning prototype for studying unusual patterns in proton–proton collision-like events. The current experiments use a controlled synthetic event generator; real CMS NanoAOD validation is still pending.

## What is included

- Feature engineering for jet, muon, electron, missing transverse energy, and invariant-mass observables
- Isolation Forest, PyTorch autoencoder, and XGBoost baselines
- SHAP-based model interpretation and event-level anomaly explanations
- Benchmarking, robustness and drift experiments
- Evaluation on anomaly categories held out from supervised training
- A NanoAOD ingestion path and a checker for validating real ROOT files
- A Streamlit dashboard and a small C++ invariant-mass utility

## Research status and caveats

This repository is a research prototype, not a validated CMS analysis or a trigger implementation. Main reported metrics come from synthetic data. The synthetic pileup and jet-energy-scale shifts are feature-table stress tests, not detector simulation. The NanoAOD reader has been exercised on a ROOT fixture generated from synthetic events; it has **not** yet been validated on a real CMS Open Data file.

Docker configuration and GitHub Actions CI are included. Check the Actions result for the current CI status; do not assume the image was manually validated on a local Docker daemon.

## Quick start

```bash
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1

pip install -r requirements.txt
python run_pipeline.py
```

Run experiments:

```bash
python run_experiments.py
```

Run tests:

```bash
pytest -q
```

Run the dashboard after generating the pipeline outputs:

```bash
streamlit run app/dashboard.py
```

For real-data validation steps, see [data/README.md](data/README.md). Once a real CMS NanoAOD file is available, run:

```bash
python check_nanoaod.py data/yourfile.root --score
```

## Repository structure

- `src/lhcanom/` — ingestion, feature engineering, models, scoring, explanations, experiments
- `app/dashboard.py` — interactive dashboard
- `tests/` — unit and fixture-based tests
- `results/` — tracked experiment summaries, CSV outputs, and figures
- `cpp/invmass.cpp` — standalone invariant-mass calculation
- `.github/workflows/ci.yml` — automated checks

Generated model binaries and test-score dumps are intentionally excluded from version control.

## License

Add a license before reuse or redistribution.
