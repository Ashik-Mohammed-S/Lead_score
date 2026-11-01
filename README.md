# Lead Conversion Scoring

[![Validation](https://github.com/Ashik-Mohammed-S/Lead_score/actions/workflows/validate.yml/badge.svg)](https://github.com/Ashik-Mohammed-S/Lead_score/actions/workflows/validate.yml)

Evaluate historical conversion propensity using acquisition attributes and engagement snapshots.

Independent public portfolio work; historical educational notebooks remain under `historical/`. The current implementation and results described here take precedence over historical in-sample numbers.

## Data and approach

9,240 labeled leads; 7,392 train and 1,848 test records.

Use an explicit feature whitelist, excluding identifiers, manual lead-quality tags and post-outcome activity labels. Fit preprocessing only on a stratified training partition and evaluate class-balanced logistic regression.

## Current full-data result

| Measure | Current analysis | Baseline where applicable |
| --- | --- | --- |
| ROC-AUC | 0.851 | 0.500 |
| PR-AUC (average precision) | 0.781 | 0.385 |
| Conversion recall | 0.722 | 0.000 |
| Accuracy | 0.790 | 0.615 |

Results are specific to the documented dataset and split. See generated `results/analysis.json` after execution for full metrics and assumptions.

## Run locally

Use the Python version in `.python-version`, then:

```sh
python -m pip install -r requirements.txt
python scripts/fetch_data.py
python scripts/run_notebook.py --mode full
```

Reference data is committed under `dataset/`, directly or as reconstructable compressed parts. The downloader verifies checksums and restores stored data offline. See [DATA.md](DATA.md) and [dataset-sources.json](dataset-sources.json) for provenance and upstream terms. Package installation and the spaCy model, where needed, require network access on a fresh machine.

## Review the implementation

Inspect the feature whitelist and availability assumption before interpreting the scores. Start with [scripts/analysis.py](scripts/analysis.py), then the root notebook. The workflow validates dependencies, smoke checks and full-data notebook execution with dataset downloads disabled.

## Limitations

Engagement snapshots must precede the conversion decision. The dataset lacks event timestamps, so this split does not establish prospective feature availability or causal lead-scoring impact.

[Method notes](ANALYSIS.md) · [All portfolio projects](https://github.com/Ashik-Mohammed-S/Ashik-Mohammed-S/blob/main/PORTFOLIO.md)
