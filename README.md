
## Analysis code and figures - Readme

R code and figures for a study of disproportionality analysis under a change in reporting obligations and stimulated (litigation- and media-driven) reporting. The code compares established methods (PRR, ROR, IC, EBGM, Mantel–Haenszel ROR, subgroup ROR) with a regime- and burst-robust (RB) method, in the observed data and in a Monte Carlo simulation.

## Contents

| Folder / file | Content |
|---|---|
| `analysis_step00-12.R` | Complete analysis, steps 00–12, run from top to bottom |
| `data/` | openFDA snapshot used in the study: `step00_openfda_reports.csv`, `step00_openfda_meta.csv`, `step00_api_yearly.csv`, `step00_api_monthly.csv` |
| `figures/` | Figures 1–4 and Supplementary Figures S1–S3 (PNG, 1200 dpi, and PDF) |

## Data

Source: openFDA cosmetic adverse event reports (https://open.fda.gov/apis/cosmetic/event/), downloaded on 18 November 2026 (openFDA metadata date 31 August 2025; last report received 29 August 2025). openFDA adds new reports over time, so a new download will differ from this snapshot. To reproduce the published results, copy the files in `data/` into the working folder; step 00 is then skipped.

## How to run

1. Install R (version 4.3 or later).
2. Copy the four files from `data/` into the working folder of the script and run it; missing packages are installed automatically.

**Note:** the folder paths in section 0 of the script (`cand`) point to the author's computer; replace them with the path to the folder on your own computer before running.

Each step writes its outputs to the working folder and is skipped when they already exist. All simulations use fixed random seeds.

## Code flow

| Step | Task | Main outputs |
|---|---|---|
| 00 | Download openFDA data (skipped when the snapshot is present) | `step00_*.csv` |
| 01 | Cleaning; reporting channel and regime; product categories, event groups, litigation-type flag | `step01_reports_clean.csv`, descriptive tables |
| 02 | Signal detection with all methods in the observed data; main Monte Carlo simulation (24 scenarios × 500 replications) | `step02_real_signals.csv`, `step02_mc_summary.csv` |
| 03 | Main figures and tables | Figures 1–4, S1, S2; Tables 1, 2, S1–S3 |
| 04 | Sensitivity to RB tuning constants; shocks spread over several categories; litigation-type definitions | Figure S3; Tables S4–S6 |
| 05 | Report-level bootstrap; one event group per report; overdispersed simulation; Hartung–Knapp pooling; FDR | Tables S7–S9 |
| 06–08 | Revision and validation of the keyword classification rules | Table S11 |
| 09 | Probable duplicates; true signals in the shocked category | Tables S9, S12 |
| 10 | Paule–Mandel pooling; trailing baseline window | Table S10 |
| 11 | Report-level tables; serious-event enrichment; extreme dominance | Tables S8, S13 |
| 12 | True signal in the shocked pair; burst duration | Table S14 |

## Required R packages

`data.table`, `ggplot2`, `scales`, `jsonlite`, `httr`, `readxl`, `parallel`; optional: `openEBGM`, `ragg`.
