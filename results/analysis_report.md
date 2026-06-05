# 6DoF Rendering Comparison — Statistical Analysis Results

Generated from `rdocs/6DoF_rendering_comparison.Rmd` · N = 27 participants · 5 algorithms

---

## 1. Overview

| Parameter | Value |
|-----------|-------|
| Participants | 27 (ages 25–50) |
| Rendering algorithms | 5 |
| Localization observations | 135 (27 × 5) |
| Quality rating observations | 135 (27 × 5) |
| Ground truth azimuth | 312° |
| Localization model | Gamma GLMM, log link |
| Quality rating model | Linear Mixed Model (LMM) |
| Random effect | Participant intercept |
| Post-hoc correction | Holm–Bonferroni |

### Algorithms

| Abbreviation | Full Name | Type |
|---|---|---|
| ScnRot | IEM SceneRotator | 3DoF baseline |
| Com.BinVR | COMPASS BinauralVR | Parametric, single HOA sphere |
| Com.6DoF | COMPASS 6DoF | Parametric, multiple HOA spheres |
| Zyl.6DoF | Zylia 6DoF HOA Renderer | Loudness crossfading interpolation |
| Del.wgts | Delaunay weights | Barycentric triangulation |

---

## 2. Main Effects

### 2.1 Localization Error (Gamma GLMM)

**Type II Wald chi-square test:**

| Effect | χ² | df | p |
|--------|------|-----|---------|
| Algorithm | 41.89 | 4 | < 0.001 |

**Pseudo R² (Nakagawa & Schielzeth):**

| R² marginal | R² conditional | ICC (subject) |
|---|---|---|
| 0.174 | 0.221 | 0.056 |

Marginal R² reflects variance explained by Algorithm alone; conditional R² adds the participant random intercept.

### 2.2 Quality Rating (LMM)

**Type III F-test:**

| Effect | F | df₁ | df₂ | p | η² |
|--------|------|-----|-----|---------|------|
| Algorithm | 4.31 | 4 | 108 | 0.003 | 0.138 |

**Variance components:**

| ICC (subject) |
|---|
| 0.275 |

27.5% of total variance in quality ratings is attributable to between-participant differences.

---

## 3. Estimated Marginal Means

### 3.1 Localization Error (°)

Model-estimated means on the response scale (degrees), back-transformed from Gamma GLMM with log link. Lower = better.

| Algorithm | EMM (°) | 95% CI lower | 95% CI upper |
|-----------|---------|-------------|-------------|
| ScnRot | 3.54 | 2.47 | 5.04 |
| Zyl.6DoF | 7.10 | 5.00 | 10.08 |
| Del.wgts | 11.28 | 7.97 | 15.95 |
| Com.BinVR | 12.06 | 8.48 | 17.14 |
| Com.6DoF | 13.71 | 9.69 | 19.36 |

**Best localization accuracy:** ScnRot (3.54°) — the 3DoF baseline.  
**Worst localization accuracy:** Com.6DoF (13.71°).

### 3.2 Quality Rating (0–100)

LMM estimated marginal means. Higher = better.

| Algorithm | EMM | 95% CI lower | 95% CI upper |
|-----------|-----|-------------|-------------|
| ScnRot | 66.8 | 57.1 | 76.6 |
| Del.wgts | 65.4 | 55.6 | 75.1 |
| Com.BinVR | 63.4 | 53.6 | 73.1 |
| Zyl.6DoF | 56.4 | 46.7 | 66.1 |
| Com.6DoF | 46.5 | 36.8 | 56.2 |

All estimates share SE = 4.74 (common random-effects structure).

**Highest rated:** ScnRot (66.8) and Del.wgts (65.4).  
**Lowest rated:** Com.6DoF (46.5).

---

## 4. Post-hoc Pairwise Comparisons (Holm–Bonferroni)

### 4.1 Localization Error

Ratios from Gamma GLMM (log link). Ratio < 1 → numerator algorithm has smaller (better) error.  
`*` p < 0.05 · `**` p < 0.01 · `***` p < 0.001

| Contrast | Ratio | SE | z | p (adj.) | Sig. |
|---|---|---|---|---|---|
| ScnRot / Com.BinVR | 0.299 | 0.071 | −5.03 | < 0.001 | *** |
| ScnRot / Com.6DoF | 0.263 | 0.063 | −5.55 | < 0.001 | *** |
| ScnRot / Zyl.6DoF | 0.505 | 0.119 | −2.92 | 0.027 | * |
| ScnRot / Del.wgts | 0.320 | 0.076 | −4.76 | < 0.001 | *** |
| Com.BinVR / Com.6DoF | 0.881 | 0.212 | −0.54 | 1.000 | |
| Com.BinVR / Zyl.6DoF | 1.688 | 0.403 | +2.17 | 0.142 | |
| Com.BinVR / Del.wgts | 1.069 | 0.255 | +0.28 | 1.000 | |
| Com.6DoF / Zyl.6DoF | 1.916 | 0.459 | +2.72 | 0.040 | * |
| Com.6DoF / Del.wgts | 1.213 | 0.289 | +0.81 | 1.000 | |
| Zyl.6DoF / Del.wgts | 0.633 | 0.150 | −1.93 | 0.217 | |

**5 of 10 comparisons significant.** ScnRot is the best localisation algorithm, significantly outperforming all four 6DoF renderers. Among 6DoF renderers, Zyl.6DoF has significantly better localisation accuracy than Com.6DoF.

### 4.2 Quality Rating

Differences from LMM (positive = numerator rated higher).

| Contrast | Diff. | SE | t | df | p (adj.) | Sig. |
|---|---|---|---|---|---|---|
| ScnRot − Com.BinVR | +3.5 | 5.71 | 0.61 | 108 | 1.000 | |
| ScnRot − Com.6DoF | +20.3 | 5.71 | 3.56 | 108 | 0.006 | ** |
| ScnRot − Zyl.6DoF | +10.4 | 5.71 | 1.83 | 108 | 0.494 | |
| ScnRot − Del.wgts | +1.5 | 5.71 | 0.26 | 108 | 1.000 | |
| Com.BinVR − Com.6DoF | +16.9 | 5.71 | 2.95 | 108 | 0.031 | * |
| Com.BinVR − Zyl.6DoF | +7.0 | 5.71 | 1.22 | 108 | 0.901 | |
| Com.BinVR − Del.wgts | −2.0 | 5.71 | −0.35 | 108 | 1.000 | |
| Com.6DoF − Zyl.6DoF | −9.9 | 5.71 | −1.73 | 108 | 0.517 | |
| Com.6DoF − Del.wgts | −18.9 | 5.71 | −3.30 | 108 | 0.012 | * |
| Zyl.6DoF − Del.wgts | −9.0 | 5.71 | −1.57 | 108 | 0.597 | |

**3 of 10 comparisons significant.** Com.6DoF is rated significantly lower than ScnRot, Com.BinVR, and Del.wgts.

---

## 5. Algorithm Rankings

| Algorithm | Localisation rank (lower error = 1) | Quality rank (higher rating = 1) |
|---|:---:|:---:|
| ScnRot | **1** | **1** |
| Zyl.6DoF | 2 | 4 |
| Del.wgts | 3 | 2 |
| Com.BinVR | 4 | 3 |
| Com.6DoF | 5 | 5 |

ScnRot (3DoF baseline) ranks first on both measures. Com.6DoF ranks last on both. The ranking is not monotone across the 6DoF methods: Zyl.6DoF shows comparatively better localisation while Del.wgts shows comparatively better quality ratings.

---

## 6. Correlation Between Measures

Pearson correlation between participant-level mean localization error and mean quality rating (N = 135 paired observations):

| r | t | df | p |
|---|---|---|---|
| −0.100 | −1.158 | 133 | 0.249 |

95% CI: [−0.264, +0.070]. No significant correlation between localization accuracy and perceived quality.

---

## 7. Model Diagnostics

### 7.1 Localization Error (Gamma GLMM — DHARMa simulation-based)

| Test | Statistic | p | Passed |
|---|---|---|:---:|
| Uniformity (KS) | D = 0.067 | 0.589 | ✓ |
| Dispersion | ratio = 0.813 | 0.626 | ✓ |
| Outliers | — | 1.000 | ✓ |

All DHARMa diagnostics indicate satisfactory model fit.

### 7.2 Quality Rating (LMM — traditional tests)

| Test | Statistic | p | Passed |
|---|---|---|:---:|
| Shapiro–Wilk (residuals) | W = 0.990 | 0.439 | ✓ |
| Levene (variance homogeneity) | F = 1.083 | 0.368 | ✓ |

Normality and homoscedasticity assumptions are met.
