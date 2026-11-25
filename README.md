# LHC Intelligent Anomaly Detection

An offline scientific machine-learning prototype for studying unusual patterns in proton–proton collision-like events. Current reported experiments use controlled synthetic events. Real CMS NanoAOD validation is still pending.

## Get the project files

The project source and experiment outputs are stored in 13 `.tar.xz` bundles in this repository. Extract all bundles into the repository root to restore the project folder structure.

**Linux / macOS**
```bash
for f in lhc-source-*.tar.xz; do tar -xJf "$f"; done
```

**Windows PowerShell**
```powershell
Get-ChildItem lhc-source-*.tar.xz | ForEach-Object { tar -xJf $_.Name }
```

The original project README is preserved at `docs/PROJECT_README.md`. Source code, tests, configs, CI workflow, and CSV/JSON experiment outputs are included in the bundles. PNG figure files were left out of the GitHub bundles to keep the upload smaller; they remain in the uploaded source ZIP.

## What is included

- Feature engineering for jet, muon, electron, missing transverse energy, and invariant-mass observables
- Isolation Forest, PyTorch autoencoder, and XGBoost baselines
- SHAP-based model interpretation and event-level anomaly explanations
- Benchmarking, robustness, drift, and contamination experiments
- Evaluation on anomaly categories held out from supervised training
- A NanoAOD ingestion path and a checker for validating real ROOT files
- A Streamlit dashboard and a small C++ invariant-mass utility

## Research status and caveats

This repository is a research prototype, not a validated CMS analysis or a trigger implementation. Main reported metrics come from synthetic data. The synthetic pileup and jet-energy-scale shifts are feature-table stress tests, not detector simulation. The NanoAOD reader has been exercised on a ROOT fixture generated from synthetic events; it has **not** yet been validated on a real CMS Open Data file.

Docker configuration and GitHub Actions CI are included. Check the Actions result for the current CI status; do not assume the image was manually validated on a local Docker daemon.

## Quick start

After extracting the bundles:

```bash
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell: .venv\\Scripts\\Activate.ps1

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

## License

Add a license before reuse or redistribution.
