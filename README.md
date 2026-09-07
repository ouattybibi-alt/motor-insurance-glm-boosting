# Motor Insurance Pricing — GLM versus Machine Learning

Full pricing pipeline for a motor third-party liability portfolio, comparing a classical GLM approach against modern machine-learning methods. Frequency-severity decomposition, separation of attritional and large claims (EVT), and a benchmarked pure-premium calculation.

Academic project (M2 Actuariat), Co-authored with S. Diouf, C. A. D. Kouamé and S. Ouattara.

## What this project does

Full end-to-end pricing pipeline, run twice on the same dataset — once with a classical GLM approach, once with machine learning — then benchmarked against each other on a common test set.

### Part 1 — GLM approach

**Data preparation**
- Merging of policy and claims tables
- Full cleaning: outliers, missing values, coherence checks
- Attritional / large-claim (CAT) separation, with dedicated CAT surcharge
- Variable recoding and reference-modality selection
- Train / test split

**Frequency modelling**
- Poisson (`pois0` null, `pois1` full)
- Backward stepwise AIC selection (`pois4` → `pois5`)
- Overdispersion test and switch to Negative Binomial (`nbinom1`)
- Zero-inflated variants: ZIP, ZINB, Hurdle
- Model comparison table

**Severity modelling**
- Gamma with variable selection (`gamma4`)
- Log-normal (`gauss2`)
- Inverse Gaussian (`igauss4`)
- Model comparison and final choice

**Output**: pure premium per policy on the test set, combining the retained frequency and severity models.

### Part 2 — Machine Learning approach

**Frequency**
- Class-imbalance handling via preferential resampling
- ML classifiers combined with the resampling strategy

**Severity**
- **Attritional claims**: ML regression models, benchmarked on holdout
- **Large claims (CAT)**: EVT / GPD extreme-value modelling combined with ML classification of the "attritional vs atypical" probability — hybrid architecture rather than a single model
- Total cost prediction: weighted combination of both regimes

### Part 3 — Synthesis

- Direct GLM vs ML comparison on frequency and cost predictions
- Reference-policyholder benchmark (predicted premium for a typical driver profile)
- GLM vs ML comparison table
- Practical recommendation on which approach to deploy

## Why this matters

Beyond the technical comparison, the project reflects the real trade-off insurers face today: GLMs are interpretable, regulatorily accepted and easy to defend to a supervisor; ML delivers better predictive accuracy but harder to explain. The synthesis section discusses when each wins in practice.

## Repository status

This repository currently contains only the report PDF. The R and Python implementations exist (GLM fitting under multiple distributions, EVT thresholding, ML models, resampling pipeline, hybrid attritional/CAT prediction) but have not yet been ported here — see `TODO.md`.

## Report

See `PATP.pdf` for the full methodology, plots, model diagnostics and quantitative comparisons.
