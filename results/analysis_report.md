# 6DoF Rendering Comparison — Statistical Analysis Results

Summary of the results produced by `rdocs/6DoF_rendering_comparison.Rmd` · N = 35 participants (localization), 34 (ratings) · 5 algorithms

---

## 1. Overview

| Parameter | Value |
|-----------|-------|
| Participants tested | 36 (ages 25–50) at two sites: 27 at Gdańsk University of Technology (PG), 9 at Zylia sp. z o.o., Poznań (ZL) |
| Analyzed participants | 35 localization, 34 quality rating |
| Rendering algorithms | 5 |
| Localization observations | 175 (35 × 5) |
| Quality rating observations | 170 (34 × 5) |
| Ground truth azimuth | 312° |
| Localization model | Gamma GLMM, log link |
| Quality rating model | Linear Mixed Model (LMM) |
| Random effect | Participant intercept |
| Post-hoc correction | Holm–Bonferroni |

Runs marked invalid by the experimenter during data collection are not included in `data/`. ZL-106 has a rating file but no valid localization run and is therefore excluded from the rating analysis; ZL-101 (invalid rating run) contributes localization data only. Ratings are analyzed only for participants who passed the localization screening (mean error ≤ 45°); all analyzed participants passed.

PG files use a decimal comma and ZL files a decimal period. The script detects the decimal mark per file.

### Algorithms

| Abbreviation | Full Name | Type |
|---|---|---|
| ScnRot | IEM SceneRotator | 3DoF baseline |
| Com.BinVR | COMPASS BinauralVR | Parametric, single HOA sphere |
| Com.6DoF | COMPASS 6DoF | Parametric, multiple HOA spheres (source tracker disabled; ambient stream only) |
| Zyl.6DoF | Zylia 6DoF HOA Renderer | Loudness crossfading interpolation |
| Del.wgts | Delaunay weights | Barycentric triangulation |

---

## 2. Main Effects

### 2.1 Localization Error (Gamma GLMM)

**Type II Wald chi-square test:**

| Effect | χ² | df | p |
|--------|------|-----|---------|
| Algorithm | 50.51 | 4 | < 0.001 |

**Pseudo R² (Nakagawa & Schielzeth):**

| R² marginal | R² conditional | ICC (subject) |
|---|---|---|
| 0.166 | 0.200 | 0.041 |

Marginal R² reflects variance explained by Algorithm alone; conditional R² adds the participant random intercept.

### 2.2 Quality Rating (LMM)

**F-test (anova.lme; single fixed factor, so sequential = marginal):**

| Effect | F | df₁ | df₂ | p | η² |
|--------|------|-----|-----|---------|------|
| Algorithm | 3.87 | 4 | 132 | 0.005 | 0.105 |

**Variance components:**

| ICC (subject) |
|---|
| 0.214 |

21.4% of total variance in quality ratings is attributable to between-participant differences.

---

## 3. Estimated Marginal Means

### 3.1 Localization Error (°)

Model-estimated means on the response scale (degrees), back-transformed from Gamma GLMM with log link. Lower = better.

| Algorithm | EMM (°) | 95% CI lower | 95% CI upper |
|-----------|---------|-------------|-------------|
| ScnRot | 3.64 | 2.69 | 4.93 |
| Zyl.6DoF | 7.74 | 5.74 | 10.42 |
| Com.BinVR | 10.48 | 7.75 | 14.16 |
| Del.wgts | 11.89 | 8.84 | 16.00 |
| Com.6DoF | 13.59 | 10.11 | 18.24 |

**Best localization accuracy:** ScnRot (3.64°), the 3DoF baseline.  
**Worst localization accuracy:** Com.6DoF (13.59°).

### 3.2 Quality Rating (0–100)

LMM estimated marginal means. Higher = better.

| Algorithm | EMM | 95% CI lower | 95% CI upper |
|-----------|-----|-------------|-------------|
| Del.wgts | 65.4 | 56.8 | 74.1 |
| ScnRot | 65.0 | 56.4 | 73.6 |
| Com.BinVR | 63.6 | 55.0 | 72.3 |
| Zyl.6DoF | 56.6 | 47.9 | 65.2 |
| Com.6DoF | 48.2 | 39.5 | 56.8 |

All estimates share SE = 4.25 (common random-effects structure).

**Highest rated:** Del.wgts (65.4) and ScnRot (65.0), not different from each other.  
**Lowest rated:** Com.6DoF (48.2).

---

## 4. Post-hoc Pairwise Comparisons (Holm–Bonferroni)

### 4.1 Localization Error

Ratios from Gamma GLMM (log link). Ratio < 1 → numerator algorithm has smaller (better) error.  
`*` p < 0.05 · `**` p < 0.01 · `***` p < 0.001

| Contrast | Ratio | SE | z | p (adj.) | Sig. |
|---|---|---|---|---|---|
| ScnRot / Com.BinVR | 0.354 | 0.073 | −5.03 | < 0.001 | *** |
| ScnRot / Com.6DoF | 0.274 | 0.056 | −6.28 | < 0.001 | *** |
| ScnRot / Zyl.6DoF | 0.478 | 0.098 | −3.61 | 0.002 | ** |
| ScnRot / Del.wgts | 0.312 | 0.064 | −5.69 | < 0.001 | *** |
| Com.BinVR / Com.6DoF | 0.773 | 0.161 | −1.24 | 0.647 |  |
| Com.BinVR / Zyl.6DoF | 1.349 | 0.279 | +1.45 | 0.590 |  |
| Com.BinVR / Del.wgts | 0.882 | 0.182 | −0.61 | 1.000 |  |
| Com.6DoF / Zyl.6DoF | 1.746 | 0.360 | +2.70 | 0.042 | * |
| Com.6DoF / Del.wgts | 1.141 | 0.235 | +0.64 | 1.000 |  |
| Zyl.6DoF / Del.wgts | 0.654 | 0.134 | −2.07 | 0.191 |  |

**5 of 10 comparisons significant.** ScnRot is the best localization algorithm, significantly outperforming all four 6DoF renderers. Among 6DoF renderers, Zyl.6DoF has significantly better localization accuracy than Com.6DoF.

### 4.2 Quality Rating

Differences from LMM (positive = first algorithm rated higher).

| Contrast | Diff. | SE | t | df | p (adj.) | Sig. |
|---|---|---|---|---|---|---|
| ScnRot − Com.BinVR | +1.4 | 5.33 | 0.25 | 132 | 1.000 |  |
| ScnRot − Com.6DoF | +16.8 | 5.33 | 3.16 | 132 | 0.018 | * |
| ScnRot − Zyl.6DoF | +8.4 | 5.33 | 1.59 | 132 | 0.692 |  |
| ScnRot − Del.wgts | −0.4 | 5.33 | −0.08 | 132 | 1.000 |  |
| Com.BinVR − Com.6DoF | +15.5 | 5.33 | 2.91 | 132 | 0.034 | * |
| Com.BinVR − Zyl.6DoF | +7.1 | 5.33 | 1.33 | 132 | 0.742 |  |
| Com.BinVR − Del.wgts | −1.8 | 5.33 | −0.34 | 132 | 1.000 |  |
| Com.6DoF − Zyl.6DoF | −8.4 | 5.33 | −1.57 | 132 | 0.692 |  |
| Com.6DoF − Del.wgts | −17.3 | 5.33 | −3.24 | 132 | 0.015 | * |
| Zyl.6DoF − Del.wgts | −8.9 | 5.33 | −1.67 | 132 | 0.684 |  |

**3 of 10 comparisons significant.** Com.6DoF is rated significantly lower than ScnRot, Com.BinVR, and Del.wgts.

---

## 5. Algorithm Rankings

| Algorithm | Localization rank (lower error = 1) | Quality rank (higher rating = 1) |
|---|:---:|:---:|
| ScnRot | **1** | 2 |
| Zyl.6DoF | 2 | 4 |
| Com.BinVR | 3 | 3 |
| Del.wgts | 4 | **1** |
| Com.6DoF | 5 | 5 |

ScnRot (3DoF baseline) localizes best; Del.wgts and ScnRot share the top of the quality ratings (difference 0.4 points). Com.6DoF ranks last on both. The ranking is not monotone across the 6DoF methods: Zyl.6DoF shows comparatively better localization, while Del.wgts shows comparatively better quality ratings.

---

## 6. Correlation Between Measures

Pearson correlation between localization error and quality rating (N = 170 paired observations):

| r | t | df | p |
|---|---|---|---|
| −0.056 | −0.723 | 168 | 0.471 |

95% CI: [−0.204, +0.096]. No significant correlation between localization accuracy and perceived quality.

Per algorithm (34 participants with both measures each; Holm adjustment across the five algorithms):

| Algorithm | r | p | p (Holm) |
|---|---|---|---|
| ScnRot | −0.089 | 0.618 | 1.000 |
| Com.BinVR | −0.212 | 0.229 | 0.916 |
| Com.6DoF | −0.018 | 0.920 | 1.000 |
| Zyl.6DoF | +0.334 | 0.053 | 0.267 |
| Del.wgts | +0.046 | 0.798 | 1.000 |

None is significant. The correlation figure (`09_correlation_error_rating.png`) shows the algorithm EMMs with 95% CIs over the individual values and per-algorithm least-squares lines; its error axis ends at 32°, so the three largest errors (up to 55°) are not drawn.

---

## 7. Model Diagnostics

### 7.1 Localization Error (Gamma GLMM — DHARMa simulation-based)

| Test | Statistic | p | Passed |
|---|---|---|:---:|
| Uniformity (KS) | D = 0.048 | 0.823 | ✓ |
| Dispersion | ratio = 0.856 | 0.614 | ✓ |
| Outliers | — | 1.000 | ✓ |

All DHARMa diagnostics indicate satisfactory model fit.

### 7.2 Quality Rating (LMM — traditional tests)

| Test | Statistic | p | Passed |
|---|---|---|:---:|
| Shapiro–Wilk (residuals) | W = 0.990 | 0.264 | ✓ |
| Levene (variance homogeneity) | F = 1.020 | 0.399 | ✓ |

Normality and homoscedasticity assumptions are met.

---

## 8. Sensitivity Analyses

| Check | Result |
|---|---|
| Site (PG vs ZL) as fixed effect, localization | LR χ²(1) = 0.01, p = 0.92 |
| Site (PG vs ZL) as fixed effect, ratings | LR χ²(1) = 0.33, p = 0.57 |
| Without the second site (ZL) | 5 of 10 localization and 3 of 10 rating comparisons significant: the same pairs as with all participants |
| Without the author's session (PG-004) | 4 of 10 localization and 2 of 10 rating comparisons significant; Com.6DoF / Zyl.6DoF (localization) p = 0.081, Com.BinVR − Com.6DoF (ratings) p = 0.095 are no longer significant |
