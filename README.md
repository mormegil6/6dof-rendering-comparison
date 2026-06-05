[![R](https://img.shields.io/badge/R-4.5-blue.svg)]()
[![glmmTMB](https://img.shields.io/badge/glmmTMB-1.1-blue.svg)]()
[![nlme](https://img.shields.io/badge/nlme-3.1-blue.svg)]()
[![emmeans](https://img.shields.io/badge/emmeans-2.0-blue.svg)]()
[![DHARMa](https://img.shields.io/badge/DHARMa-0.4-blue.svg)]()
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

# 6DoF Rendering Comparison - Supplementary Materials

Supplementary materials for the paper:

**"Comparison of Six-Degrees-of-Freedom Rendering Algorithms for Classical Music Reproduction"**  
Bartlomiej Mroz - *Archives of Acoustics*, 2026 [under review]

This repository contains raw experimental data and reproducible analysis code
supporting all reported statistics, figures, and tables in the paper.

## Repository Structure

```
6dof-rendering-comparison/
├── data/
│   ├── PG-*-Localization.csv   # Trial-level localization responses (27 participants)
│   └── PG-*-MUSHRA.csv         # Quality rating responses
├── rdocs/
│   └── 6DoF_rendering_comparison.Rmd   # Reproducible analysis script (R Markdown)
├── results/
│   ├── analysis_report.md      # Pre-rendered results (readable without running R)
│   └── latex_values.tex        # Auto-generated LaTeX macros for the paper
├── plots/                      # Figure files (PNG), generated on knit
├── LICENSE
└── README.md
```

## Data

**Participants**: 27 (ages 25-50)  
**Rendering algorithms**: 5 (ScnRot, Com.BinVR, Com.6DoF, Zyl.6DoF, Del.wgts)  
**Total localization observations**: 135 (27 x 5)  
**Total quality rating observations**: 135 (27 x 5)

**Experimental variables**:
- `Algorithm`: Rendering algorithm (5 levels)
- `Azimuth`: Participant's localization response (degrees)
- `Rating`: MUSHRA-like quality rating (0-100)

**Key measures**:
- Localization error: absolute angular deviation from ground truth (312 deg)
- Quality rating: holistic perceived quality on a 101-point scale

The soprano soloist from the Aria of Donna Elvira (Mozart, *Don Giovanni*) was
the localization target, embedded in a virtual orchestral sound scene rendered
with third-order Ambisonics.

## Reproducing the Analysis

### Prerequisites

```r
install.packages(c(
  "tidyverse",
  "glmmTMB",   # Gamma GLMM for localization error
  "nlme",      # LMM for quality ratings
  "lmerTest",
  "emmeans",   # Estimated marginal means and post-hoc comparisons
  "DHARMa",    # Simulation-based residual diagnostics
  "MuMIn"      # R squared for mixed models
))
```

### Run the Analysis

Open `rdocs/6DoF_rendering_comparison.Rmd` in RStudio and knit, or run from the
command line:

```bash
cd rdocs
Rscript -e "rmarkdown::render('6DoF_rendering_comparison.Rmd')"
```

### Outputs

The script produces:

- **`results/latex_values.tex`** - LaTeX `\newcommand` macros for all reported
  statistics; included directly by the paper's main.tex
- **`results/analysis_report.html`** - Full rendered analysis with all figures
  and diagnostic plots
- **`plots/`** - Individual figure files (PNG)

All reported numerical values in the paper are auto-generated from
`latex_values.tex`; re-running the script on the provided data exactly
reproduces the paper's statistics.

## Statistical Methods

| Outcome | Model | Link |
|---------|-------|------|
| Localization error (deg) | Gamma GLMM | log |
| Quality rating (0-100) | LMM | identity |

Both models include participant as a random intercept.
Post-hoc pairwise comparisons use Holm-Bonferroni correction.
Model fit was assessed using simulation-based residual diagnostics (DHARMa).

## Citation

If you use this data or analysis code, please cite the main paper:

[BibTeX citation will be added upon publication]

## License

Data and code are released under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You are free to share and adapt the material for any purpose, provided
appropriate credit is given.

## Contact

Bartlomiej Mroz - bartlomiej.mroz@pg.edu.pl - [bmroz.eu](https://bmroz.eu)
