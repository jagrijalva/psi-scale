# Power-Sharing Index (PSI)

**Author:** Jessala A. Grijalva, PhD

Construction, validation, and U.S.-case application of the **Power-Sharing Index (PSI)**, a measure of *de facto* power distribution across social groups in democratic systems. PSI captures whether political power can transfer across demographic boundaries — the dimension that standard democracy indices miss.

## The Problem

Standard democracy indices show moderate-to-high scores during periods of massive group-level exclusion. V-Dem's Electoral Democracy Index averaged approximately 0.35 during the era of foundational exclusion (1789–1865), when African Americans were enslaved, women could not vote, Indigenous peoples were not citizens, and citizenship was restricted to "free white persons." PSI addresses this by measuring cross-group power-sharing rather than procedural quality.

## Components

Five V-Dem indicators with full U.S. coverage from 1789: Social Group Power (`v2pepwrsoc`), Gender Power (`v2pepwrgen`), Civil Liberties Equality (`v2clsocgrp`), Freedom from Torture (`v2cltort`), and Freedom from Killings (`v2clkill`). The additive PSI is the main descriptive score; geometric, coercion-gated, and hybrid specifications are retained for robustness. V-Dem measurement-uncertainty bounds (`codelow`/`codehigh`) are propagated into the exported series.

## Validation Summary

Statistics below are from the rendered V-Dem v16 pipeline in this repository.

- Internal consistency: raw Cronbach's alpha = 0.962 (standardized 0.963; average inter-item r = 0.840).
- Dimensionality: PC1 explains 87.5% of component variance.
- Sampling adequacy: overall KMO = 0.787.
- Robustness: additive, geometric, coercion-gated, and hybrid aggregations preserve the same historical pattern; leave-one-component-out (jackknife) checks preserve the main trajectory; PSI responds in expected directions to known inclusionary and retrenchment events.

## Repository Structure

```
psi/
├── data/
│   ├── raw/        # V-Dem v16 source data (NOT tracked; download required)
│   └── derived/    # usa_psi_final.rda, usa_case_results.rda (pipeline checkpoints)
├── docs/           # V-Dem v16 documentation: codebook, cautionary notes,
│                   # suggested citation, what's new
├── figures/        # Deliberately exported final figures only (GrijalvaFig1.pdf)
├── 01_measurement.qmd   # Constructs and validates PSI; writes usa_psi_final.rda
├── 01_measurement.pdf
├── 02_us_case.qmd       # U.S. case analysis; writes usa_case_results.rda and Figure 1
├── 02_us_case.pdf
├── psi.Rproj
├── README.md
└── LICENSE
```

## Data

The raw V-Dem data file is **not** included in this repository. Download **V-Dem v16** (`V-Dem-CY-Full+Others-v16.rds`) directly from V-Dem and place it in `data/raw/`.

Source: https://www.v-dem.net/data/the-v-dem-dataset/

Official V-Dem documentation (codebook, cautionary notes, suggested citation, release notes) is tracked in `docs/`.

## Replication

1. Clone the repository.
2. Download V-Dem v16 and place `V-Dem-CY-Full+Others-v16.rds` in `data/raw/`.
3. Open `psi.Rproj` in RStudio.
4. Render `01_measurement.qmd`. This constructs and validates the PSI and writes `data/derived/usa_psi_final.rda`.
5. Render `02_us_case.qmd`. This consumes `usa_psi_final.rda`, runs the U.S. case analysis, writes `data/derived/usa_case_results.rda`, and exports `figures/GrijalvaFig1.pdf`.

Rendering 01 before 02 is required: 02 reads the derived object that 01 produces. Each QMD renders to a single PDF in the repository root; all figures, tables, and measurement checks appear inside those PDFs. The broader five-index V-Dem comparison in 02 begins in 1900 because Egalitarian and Deliberative Democracy do not provide earlier U.S. coverage; the full-period institutional comparison uses Electoral Democracy from 1789.
