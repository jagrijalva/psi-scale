# CLAUDE.md - AI Assistant Guide for Power-Sharing Index

## Project Overview

This repository contains the **Power-Sharing Index (PSI)**, a novel measure of *de facto* power distribution across social groups in democratic systems. The project addresses a critical blindspot in existing democracy measures: standard indices like V-Dem show moderate-to-high scores during periods of massive group-level exclusion (e.g., Electoral Democracy = 0.48 during Jim Crow).

**Author**: Jessala Grijalva, Institute for Latino Studies, University of Notre Dame

**Core Concept**: The PSI distinguishes between:
- **Herrenvolk democracy**: Democratic procedures for dominant groups, systematic exclusion for others
- **Power-sharing democracy**: Political power genuinely distributed across social groups

## Repository Structure

```
Power-Sharing-Index/
├── Power-Sharing Index           # Main Quarto analysis document (.qmd without extension)
├── Herrenvolk Presentation Nov 11.qmd  # Beamer presentation slides
├── README.md                     # Project documentation
├── LICENSE                       # MIT License
├── codebook.pdf                  # V-Dem codebook reference
├── cautionary_notes.pdf          # V-Dem cautionary notes
├── .gitignore                    # Ignores *.rds data files
└── CLAUDE.md                     # This file
```

### Key Files

| File | Purpose |
|------|---------|
| `Power-Sharing Index` | Main R/Quarto document for PSI construction and validation |
| `Herrenvolk Presentation Nov 11.qmd` | Beamer slides for academic presentations |
| `README.md` | Comprehensive project documentation |
| `codebook.pdf` | V-Dem v15 variable codebook (reference) |

## Technology Stack

- **R** (4.0+) - Primary analysis language
- **Quarto** - Document rendering (HTML, PDF, Beamer slides)
- **Key R Packages**:
  - `tidyverse` - Data manipulation and visualization
  - `psych` - Reliability analysis (Cronbach's alpha)
  - `knitr`, `kableExtra` - Table formatting
  - `scales` - Axis formatting

## Data Requirements

**V-Dem Dataset** (not included in repo due to size):
- Source: https://v-dem.net/data/dataset-archive/
- Version: V-Dem v15 (Country-Year: Full+Others)
- File: `V-Dem-CY-Full+Others-v15.rds`
- Expected location: `~/Desktop/V-Dem/` (configurable in code)

The `.gitignore` excludes `*.rds` files to prevent large data files from being committed.

## Power-Sharing Index Specification

### Component Indicators (7 total)

| Variable | Domain | Description |
|----------|--------|-------------|
| `v2elsuffrage` | Exclusion | % adult citizens with legal right to vote |
| `v2clsocgrp` | Power | Social group equality in civil liberties |
| `v2pepwrgen` | Power-Gender | Power distributed by gender |
| `v2clacjstw` | Rights | Women's access to justice |
| `v2clacjstm` | Rights | Men's access to justice |
| `v2pepwrsoc` | Power | Power distributed by social group |
| `v2clacjust` | Power-SES | Class equality in civil liberties |

### Construction Method

1. **Standardization**: Min-max normalization to [0,1] scale
2. **Aggregation**: Unweighted mean of 7 standardized indicators
3. **Temporal coverage**: United States, 1789-2024

### Validation Metrics

- **Cronbach's α**: 0.98 (excellent internal consistency)
- **Discrimination power**: 0.76 gap (Jim Crow → Post-Civil Rights)
- **Convergent validity**: r > 0.96 with V-Dem dimensions

## Development Workflow

### Running the Analysis

```r
# Install dependencies
install.packages(c("tidyverse", "psych", "knitr", "kableExtra", "scales"))

# Render the main analysis
quarto render "Power-Sharing Index"
```

### Rendering Presentations

```bash
quarto render "Herrenvolk Presentation Nov 11.qmd"
```

### Output Structure

The analysis creates a timestamped output directory:
```
~/Desktop/V-Dem/PSI_Output_YYYYMMDD_HHMMSS/
├── Fig1_VDem_Puzzle.png
├── Fig2_Five_Dimensions.png
├── Fig3_Component_Contribution.png
├── Fig4_Six_Dimensions.png
├── Fig5_Herrenvolk_Gap.png
├── Fig6_Discrimination_Performance.png
├── Fig7_Validation_Summary.png
├── power_sharing_index_1789_2024.csv
└── validation_metrics.csv
```

## Code Conventions

### R Style

- Use `tidyverse` conventions for data manipulation
- Pipe operators (`%>%`) for data transformation chains
- `ggplot2` for all visualizations with `theme_minimal()`
- Comments explain methodology, not just code

### Quarto Conventions

- YAML front matter specifies output format and theme
- Code chunks use `{r chunk-name}` naming
- `code-fold: show` for transparency
- `warning: false, message: false` to suppress noise

### Figure Standards

- Resolution: 300 DPI for publication quality
- Dimensions: Typically 10-14" wide, 6-8" tall
- Color scheme: Consistent with academic standards
  - Green (`#2E7D32`) for Electoral
  - Black for Power-Sharing
  - Red (`#C62828`) for Egalitarian

## Historical Periods for Analysis

| Period | Years | Description |
|--------|-------|-------------|
| Slavery | 1789-1865 | Pre-Civil War era |
| Jim Crow | 1877-1965 | Systematic disenfranchisement |
| Post-Civil Rights | 1966-2024 | Post-Voting Rights Act |
| Women's suffrage | 1920 | 19th Amendment milestone |

## Key Terminology

- **Herrenvolk democracy**: Democracy for the dominant group, tyranny for others (Van den Berghe, 1967)
- **PSI**: Power-Sharing Index
- **V-Dem**: Varieties of Democracy project
- **Discrimination power**: Ability to distinguish between known historical periods

## AI Assistant Guidelines

### When Modifying Code

1. Preserve the methodological comments explaining *why* choices were made
2. Maintain the 7-indicator specification unless explicitly changing it
3. Keep validation sections (discrimination, alpha, convergent validity)
4. Use consistent variable naming (`v2*` for V-Dem variables)

### When Adding Visualizations

1. Follow existing ggplot2 style and theme
2. Save to output directory with descriptive names
3. Use 300 DPI for publication quality
4. Include figure captions explaining the insight

### When Updating Documentation

1. Keep README.md comprehensive for external users
2. Update validation metrics if specification changes
3. Maintain citation information

### Data Handling

- Never commit `.rds` files (they're gitignored)
- V-Dem data path is hardcoded to `~/Desktop/V-Dem/` - may need adjustment
- Filter for USA: `country_name == "United States of America"`

## Common Tasks

### Add a New Indicator

1. Add variable name to `psi_indicators` vector
2. Update `indicator_info` table with description
3. Re-run validation (check alpha doesn't drop significantly)
4. Update README with new specification

### Change Time Period

1. Modify filter in `usa <- vdem %>% filter(...)`
2. Update period definitions (`jim_crow`, `post_cr`)
3. Re-validate discrimination power

### Export for Different Country

1. Change filter from USA to target country
2. Verify indicator availability (check for NA patterns)
3. Define appropriate historical periods for validation

## Citation

```bibtex
@unpublished{grijalva2025herrenvolk,
  author = {Grijalva, Jessala},
  title = {The Herrenvolk Blindspot: Power-Sharing, Tocqueville,
           and the Real Test of Democracy},
  year = {2025},
  note = {Working Paper},
  institution = {Institute for Latino Studies, University of Notre Dame}
}
```

## Contact

Jessala Grijalva - jgrijal2@nd.edu
Institute for Latino Studies, University of Notre Dame
