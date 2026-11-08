[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.24054143-blue.svg)](https://doi.org/10.5281/zenodo.24054143) [![R](https://img.shields.io/badge/R-4.4.1-blue.svg)]() [![glmmTMB](https://img.shields.io/badge/glmmTMB-1.1-blue.svg)]() [![nlme](https://img.shields.io/badge/nlme-3.1-blue.svg)]() [![emmeans](https://img.shields.io/badge/emmeans-2.0-blue.svg)]() [![DHARMa](https://img.shields.io/badge/DHARMa-0.4-blue.svg)]() [![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

# 6DoF Rendering Comparison - Supplementary Materials

Supplementary materials for the paper:

***"Walking Through a Virtual Orchestra: Localization–Quality Trade-offs in Six-Degrees-of-Freedom Audio Rendering for Virtual Reality"***  
Bartłomiej Mróz · submitted to *IEEE Transactions on Visualization and Computer Graphics* (manuscript TVCG-2026-11-1423, 8 November 2026)

Archived on Zenodo: the release used for the paper is v1.0.0, [doi:10.5281/zenodo.24054144](https://doi.org/10.5281/zenodo.24054144); the badge DOI always resolves to the latest version.

This repository contains raw experimental data and reproducible analysis code
supporting all reported statistics, figures, and tables in the paper.

## Repository Structure

```
6dof-rendering-comparison/
├── data/
│   ├── {PG,ZL}-*-Localization.csv   # Trial-level localization responses (35 participants)
│   └── {PG,ZL}-*-MUSHRA.csv         # Quality rating responses (35 files; 34 analyzed)
├── rdocs/
│   └── 6DoF_rendering_comparison.Rmd   # Reproducible analysis script (R Markdown)
├── results/
│   ├── analysis_report.md      # Pre-rendered results (readable without running R)
│   └── latex_values.tex        # Auto-generated LaTeX macros for the paper
├── plots/                      # Figure files (PNG), generated on knit
├── CITATION.cff                # Citation metadata (also read by GitHub and Zenodo)
├── LICENSE
└── README.md
```

## Data

**Participants**: 36 tested (ages 25-50) at two sites running the same software:
27 at Gdańsk University of Technology (`PG-*`) and 9 at Zylia sp. z o.o., Poznań (`ZL-*`)  
**Analyzed**: 35 for localization, 34 for quality ratings (see below)  
**Rendering algorithms**: 5 (ScnRot, Com.BinVR, Com.6DoF, Zyl.6DoF, Del.wgts)  
**Total localization observations**: 175 (35 x 5)  
**Total quality rating observations**: 170 (34 x 5)

**Files are the raw logs, unmodified** (byte-identical to the files written by the
test application). Runs marked invalid by the experimenter during data collection
are not included. As a result:
- ZL-106 has a rating file but no valid localization run; the script therefore
  excludes this participant from the rating analysis (ratings are analyzed only for
  participants with a valid localization run). Hence 36 tested, 35 analyzed for
  localization, 34 for ratings.
- ZL-101 has localization data only (invalid rating run).

**Decimal separator.** PG files use a decimal comma and ZL files a decimal period.
The files are not edited; instead, `read_participant_data()` in the Rmd detects the
decimal mark of each file before parsing it. (Parsing period-decimal files with a
comma locale silently turns `158.8585` into `1588585`, which is why this step matters.)

**Sensitivity analyses** (in the Rmd, chunk `sensitivity`; values in
`results/latex_values.tex`): site as a fixed effect, and all pairwise comparisons
refitted without the author's own session (PG-004) and without the second site (ZL).

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
  "rmarkdown", "knitr", "kableExtra",
  "tidyverse",
  "glmmTMB",   # Gamma GLMM for localization error
  "nlme",      # LMM for quality ratings
  "car",       # Type II Wald test, Brown-Forsythe (median-centred Levene) test
  "emmeans",   # Estimated marginal means and post-hoc comparisons
  "multcomp",
  "DHARMa",    # Simulation-based residual diagnostics
  "MASS",
  "ggpubr", "gridExtra", "viridis"
))
```

The paper's values were produced with R 4.4.1.

```
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
  statistics, included directly by the paper's LaTeX source (the copy committed
  here is the one used for the paper)
- **`rdocs/6DoF_rendering_comparison.html`** - Full rendered analysis with all
  figures and diagnostic plots
- **`plots/`** - Individual figure files (PNG)

`results/analysis_report.md` is a hand-written summary of the rendered results
for reading without R.

All reported numerical values in the paper are auto-generated from
`latex_values.tex`; re-running the script on the provided data exactly
reproduces the paper's statistics.

## Statistical Methods

| Outcome | Model | Link |
|---------|-------|------|
| Localization error (deg) | Gamma GLMM | log |
| Quality rating (0-100) | LMM | identity |

Both models include participant as a random intercept. The localization main
effect is a Type II Wald chi-square test (`car::Anova`); the rating main effect is
the F-test of `anova.lme` (one fixed factor, so sequential and marginal tests
coincide); variance homogeneity is tested with the Brown-Forsythe variant of
Levene's test (`car::leveneTest(center = median)`).
Post-hoc pairwise comparisons use Holm-Bonferroni correction.
Model fit was assessed using simulation-based residual diagnostics (DHARMa).

## Citation

If you use this data or analysis code, please cite the main paper:

```
[BibTeX citation will be added upon publication]
```

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: https://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

## Contact

Bartłomiej Mróz · bartlomiej.mroz@pg.edu.pl · Department of Multimedia Systems, Gdańsk University of Technology · [bmroz.eu](https://bmroz.eu)
