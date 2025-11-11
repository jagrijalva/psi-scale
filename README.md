# Power-Sharing Index: Measuring Group-Level Democracy

**Author**: Jessala Grijalva  
**Affiliation**: Institute for Latino Studies, University of Notre Dame  
**Version**: 1.0  
**Last Updated**: November 2025

---

## Overview

This repository contains code and documentation for constructing the **Power-Sharing Index (PSI)**, a measure of *de facto* power distribution across social groups in democratic systems.

### The Problem

Standard democracy indices show moderate-to-high scores during periods of massive group-level exclusion. For example:

- **V-Dem's Electoral Democracy Index averaged 0.48 during Jim Crow** (1877-1965)
- Yet during this period:
  - African Americans systematically disenfranchised
  - Women could not vote until 1920
  - Indigenous peoples not citizens until 1924
  - Citizenship restricted to "free white persons" (1790-1952)

**Question**: How can a democracy measure score nearly 0.50 when more than half the population is excluded from political power?

**Answer**: Existing measures focus on *institutional arrangements* (electoral procedures, rights protections, constraints on executive) rather than *actual power distribution across social groups*.

### The Solution

The Power-Sharing Index distinguishes between:

- **Herrenvolk democracy**: Democratic procedures for dominant groups, systematic exclusion for others
- **Power-sharing democracy**: Political power distributed across social groups

---

## Key Features

### Superior Discrimination Power
- **PSI gap (Jim Crow → Post-Civil Rights)**: 0.76
- **Best V-Dem dimension (Egalitarian)**: 0.38
- **PSI is 2x more sensitive** to exclusionary dynamics

### Excellent Psychometric Properties
- **Cronbach's α**: 0.98 (excellent internal consistency)
- **Temporal coverage**: 1789-2024 (full US history)
- **Convergent validity**: High correlations with V-Dem dimensions (r > 0.96)

### Transparent Methodology
- Theory-guided indicator selection
- Empirical validation using known historical periods
- Full code and documentation provided
- Reproducible results

---

## Repository Contents

```
Power-Sharing-Index/
│
├── Power_Sharing_Index_Analysis.qmd    # Main analysis file (Quarto)
├── README.md                            # This file
├── LICENSE                              # MIT License
│
├── data/
│   └── [V-Dem data not included - download from v-dem.net]
│
├── output/
│   ├── figures/                        # All visualizations (PNG)
│   ├── power_sharing_index_timeseries.csv
│   ├── validation_summary.csv
│   └── indicator_specifications.csv
│
└── docs/
    └── Appendix_Indicator_Selection.qmd # Detailed methodology
```

---

## Quick Start

### Prerequisites

```r
# Install required packages
install.packages(c("tidyverse", "psych", "knitr", "kableExtra", "scales"))
```

### Download V-Dem Data

1. Go to [https://v-dem.net/data/dataset-archive/](https://v-dem.net/data/dataset-archive/)
2. Download V-Dem v15 (Country-Year: Full+Others)
3. Save as `V-Dem-CY-Full+Others-v15.rds`

### Run Analysis

```r
# Open Power_Sharing_Index_Analysis.qmd in RStudio
# Click "Render" or run:
quarto render Power_Sharing_Index_Analysis.qmd
```

This will:
- Construct the Power-Sharing Index
- Run all validation tests
- Generate 6 figures
- Export time series data and validation metrics
- Create organized output directory

---

## Methodology

### Conceptual Framework

The PSI measures four domains of group-level power:

1. **Formal Exclusion** - Legal restrictions on political participation
2. **Power Distribution** - Group-level access to political power
3. **Civil Liberties** - Equal protection and rights across groups  
4. **Access to Justice** - Equal treatment in legal systems

### Indicator Selection Criteria

Indicators must satisfy:

1. **Theoretical alignment**: Measures group-level (not individual) dynamics
2. **Temporal coverage**: Data available from US founding (1789)
3. **Empirical discrimination**: Distinguishes Jim Crow from Post-Civil Rights periods
4. **Conceptual balance**: Represents multiple domains

### Final Specification (7 Indicators)

| Variable | Domain | Description |
|----------|--------|-------------|
| v2elsuffrage | Exclusion | % adult citizens with legal right to vote |
| v2clsocgrp | Power | Social group equality in civil liberties |
| v2pepwrgen | Power-Gender | Power distributed by gender |
| v2clacjstw | Rights | Women's access to justice |
| v2clacjstm | Rights | Men's access to justice |
| v2pepwrsoc | Power | Power distributed by social group |
| v2clacjust | Power-SES | Class equality in civil liberties |

### Construction Method

1. **Standardization**: Min-max normalization to [0,1] scale
2. **Aggregation**: Unweighted mean of 7 standardized indicators
3. **Validation**: 
   - Internal consistency (Cronbach's α)
   - Discrimination power (Jim Crow vs Post-Civil Rights)
   - Convergent validity (correlations with V-Dem dimensions)

---

## Validation Results

### Internal Consistency
- **Cronbach's α = 0.98** → Excellent

### Discrimination Power
| Measure | Jim Crow Mean | Post-CR Mean | Gap |
|---------|---------------|--------------|-----|
| **Power-Sharing** | 0.06 | **0.82** | **0.76** |
| Egalitarian | 0.21 | 0.59 | 0.38 |
| Electoral | 0.48 | 0.83 | 0.35 |

### Convergent Validity
| V-Dem Dimension | Correlation with PSI |
|----------------|---------------------|
| Egalitarian | 0.990 |
| Electoral | 0.989 |
| Liberal | 0.986 |

---

## Key Visualizations

### The Herrenvolk Gap
Shows divergence between electoral democracy (procedures) and power-sharing (actual distribution):

- **1789-1920**: Large gap (democracy for some, exclusion for others)
- **1920**: Women's suffrage → gap narrows
- **1965**: Voting Rights Act → convergence

### Six Democracy Dimensions
Compares Power-Sharing Index with V-Dem's five dimensions:

- **Period 1 (1789-1920)**: PSI flat, V-Dem rising → herrenvolk era
- **Period 2 (1920-1965)**: Both rise but gap persists → partial inclusion
- **Period 3 (1965-2013)**: Convergence → power-sharing democracy
- **Period 4 (2013-2024)**: New divergence → contemporary crisis

---

## Citation

If you use this index in your research, please cite:

```
Grijalva, Jessala. (2025). "The Herrenvolk Blindspot: Power-Sharing, 
Tocqueville, and the Real Test of Democracy." Working Paper, Institute 
for Latino Studies, University of Notre Dame.
```

BibTeX:
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

---

## Theoretical Background

### What is Herrenvolk Democracy?

**Herrenvolk democracy** (Van den Berghe, 1967) refers to democratic systems that extend full political rights only to a dominant group while excluding or subordinating others.

Core characteristics:
- Democratic procedures function *for included groups*
- Systematic exclusion of other groups from political power
- Institutions (elections, rights protections) operate normally *within the demos*
- But the demos itself is racially/ethnically restricted

### Historical Examples

- **United States (1789-1965)**: White male democracy with systematic Black, women, Indigenous, Asian exclusion
- **South Africa (1910-1994)**: White democracy under apartheid
- **Australia (pre-1967)**: White democracy with Indigenous exclusion

### Why Existing Measures Miss It

Democracy indices assess:
- Electoral procedures ✓
- Rights protections ✓  
- Constraints on executive ✓
- Institutional checks and balances ✓

But they don't assess:
- **Who constitutes "the people"** ✗
- **Whether power is shared across groups** ✗
- **De facto vs de jure inclusion** ✗

The PSI fills this gap.

---

## Contemporary Relevance

The herrenvolk democracy framework helps diagnose contemporary democratic crises:

### United States (2013-2024)
- Voter suppression targeting communities of color
- Gerrymandering diluting minority voting power
- Attacks on immigration and citizenship
- Rhetoric about "real Americans" vs "outsiders"

**Question**: Is this "democratic backsliding" or "herrenvolk consolidation"?

The distinction matters because:
- **Backsliding diagnosis** → Restore institutional norms
- **Herrenvolk diagnosis** → The crisis is over power-sharing itself

### Other Cases
- **India**: Hindu nationalism and minority exclusion
- **Israel**: Tension between Jewish state and democratic values
- **Hungary**: Ethnic nationalism under Orbán

The PSI provides a tool to measure these dynamics comparatively.

---

## Limitations and Future Directions

### Current Limitations

1. **Geographic scope**: Currently validated only for United States
2. **Indicator availability**: Limited by V-Dem variable coverage
3. **Group specification**: Focus on ethnoracial/gender groups (could expand to religion, sexuality, etc.)
4. **Aggregation**: Unweighted mean (could explore weighted approaches)

### Future Development (Version 2.0)

Ideal enhancements:
- Direct measures of group representation in governance
- Economic power distribution across groups
- State violence targeting specific groups
- Policy responsiveness by group
- Descriptive representation in bureaucracy
- Cross-national validation

**Feedback welcome**: Open an issue or contact author

---

## License

MIT License - see LICENSE file for details

This means you can:
- ✓ Use for academic research
- ✓ Modify and extend
- ✓ Use for teaching
- ✓ Include in publications

Just provide attribution!

---

## Contact

**Jessala Grijalva**  
Postdoctoral Fellow  
Institute for Latino Studies  
University of Notre Dame  
Email: jgrijal2@nd.edu

---

## Acknowledgments

This work builds on:
- V-Dem Institute's democracy measurement project
- Tocqueville's observations on American democracy and race
- Van den Berghe's herrenvolk democracy concept
- Critical race theory and comparative politics scholarship

---

## Version History

**v1.0 (November 2025)**
- Initial release
- 7-indicator specification
- US temporal coverage (1789-2024)
- Full validation results

---

## References

Coppedge, Michael, et al. (2025). *V-Dem Codebook v15*. Varieties of Democracy (V-Dem) Project.

Tocqueville, Alexis de. (1835). *Democracy in America*.

Van den Berghe, Pierre L. (1967). *Race and Racism: A Comparative Perspective*. New York: Wiley.
