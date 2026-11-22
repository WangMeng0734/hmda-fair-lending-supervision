# HMDA Data Preparation and Prediction Models

This repository contains the scripts for downloading and processing public HMDA data and training the three application-level prediction models in the manuscript.

## Data source

The study uses 2018–2024 HMDA data for California (CA), New York (NY), and Texas (TX). The official CSV endpoint is `https://ffiec.cfpb.gov/v2/data-browser-api/view/csv?states=CA&years=2018`. Substitute the state abbreviation and year for each file. `experiments/scripts/01_download_hmda.py` constructs the URLs from `experiments/config/project.json` and records download metadata and checksums.

## Directory layout

- `experiments/scripts/01_download_hmda.py` downloads source CSV files.
- `experiments/scripts/02_build_database.py` and `03_validate_database.py` process and check the database.
- `experiments/scripts/04_build_main_database.py` orchestrates source preparation.
- `experiments/scripts/05_build_modeling_tables.py` applies the sample rules and constructs modeling tables.
- `models/01_logistic_baseline`, `02_lightgbm_baseline`, and `03_lightgbm_optuna` contain the formal prediction scripts and model-specific documentation.

Run these stages in order from the repository root after installing Python dependencies. The historical requirements files in `experiments/` are retained for reference; install additional packages imported by the scripts, including Optuna and reporting libraries. Large generated files are written under `data/`, `models/*/results/`, and `experiments/logs/`, all excluded by `.gitignore`. The orchestration script uses the current Python interpreter. The optional `experiments/vendor` and `experiments/vendor_py39` import paths may be empty; standard installed packages will then be used.

