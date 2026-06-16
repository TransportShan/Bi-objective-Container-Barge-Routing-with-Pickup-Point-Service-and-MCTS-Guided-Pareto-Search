# Container barge routing with pickup-point service

This repository contains the reproducibility package for the computational study on container barge routing with pickup-point service and MCTS-guided Pareto search.

The instances are adapted from public VRPTW benchmark files. They are not field-observed maritime data. The package includes the processed test instances, the public-source benchmark files used to construct them, the algorithm source code, result tables, and manuscript figures.

## Public benchmark sources

The source VRPTW files in `data/source_instances/text` come from the ML4VRP2023 public repository, which redistributes Solomon and Homberger-style VRPTW benchmark instances documented by the SINTEF TOP benchmark pages.

Use the manuscript reference list for formal citation. Public source pages:

- ML4VRP2023 repository: https://github.com/ML4VRP/ML4VRP2023
- SINTEF TOP VRPTW benchmark pages: https://www.sintef.no/projectweb/top/vrptw/

## Repository structure

- `src/`: Python implementation of instance construction, constructive routing, deterministic local search, MCTS-guided service-mode search, summary tables, and figure generation.
- `data/source_instances/text/`: selected public VRPTW source files used in the experiments.
- `data/processed_instances/`: processed barge-pickup test instances used in the reported experiments.
- `results/`: processed instances and result files in the locations expected by the scripts.
- `results/pareto_ls/`: threshold-only plus deterministic local-search outputs.
- `results/tables/`: manuscript numerical tables and summary CSV files.
- `results/figures/`: manuscript figure files.

## Environment

Python 3.10 or newer is recommended.

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

On Linux or macOS, activate the virtual environment with `source .venv/bin/activate`.

## Reproducing processed instances

The processed instances used by the manuscript are already included. To regenerate one processed instance from a public source file, run for example:

```bash
python src/derive_barge_instances.py data/source_instances/text/Customer100/C102.txt --output-dir data/processed_instances --customers 50 --pickup-ratio 0.2 --alpha-ratio 0.25
```

For 100-customer instances, use `--customers 100 --pickup-ratio 0.2`. For 200-customer instances, use `--customers 200 --pickup-ratio 0.2`.

## Reproducing MCTS comparison results

The MCTS batch summary script reads `results/single_*.json` and `results/pareto_ls/*_pareto_ls.csv`.

```bash
python src/run_mcts_batch_summary.py --iterations 120 --max-passes 100 --seed 20260610 --exploration 0.75 > results/tables/mcts_threshold_comparison_regenerated.csv
```

The stochastic seed is fixed. Minor runtime differences are expected across machines.

## Reproducing numerical tables and figures

```bash
python src/generate_numerical_analysis_assets.py
```

This regenerates the numerical-analysis CSV tables and figure assets from the stored result files.

## Data and code availability statement for the manuscript

A GitHub-ready reproduction package has been prepared for this study. It contains the instance-construction scripts, algorithm source code, processed benchmark test sets, numerical result tables, final figures, checksums, and reproduction commands. After repository creation and archival deposit, replace the manuscript placeholder with the public GitHub URL and permanent DOI.

## License

No license is assigned in this package. Add the intended code and data license before making the repository public.
