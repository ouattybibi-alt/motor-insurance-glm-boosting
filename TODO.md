# TODO — Code migration

The R and Python implementation is currently only available in the report screenshots.
To restore this repository to a fully executable state, the following scripts should be added.

## Priority 1 — data pipeline

- [ ] `data_loading.R` — merge policy / claims tables, coherence checks
- [ ] `data_cleaning.R` — outliers, missing values, recoding of factors
- [ ] `train_test_split.R` — reproducible partition with seed
- [ ] `cat_separation.R` — attritional / large-claim threshold and surcharge

## Priority 2 — GLM part

- [ ] `glm_frequency.R` — Poisson, Negative Binomial, ZIP, ZINB, Hurdle
  - Backward stepwise AIC selection
  - Overdispersion test (Cameron-Trivedi)
- [ ] `glm_severity.R` — Gamma, Log-normal, Inverse Gaussian
- [ ] `glm_comparison.R` — AIC/BIC/deviance table, out-of-sample MAE/RMSE
- [ ] `pure_premium_glm.R` — combined frequency × severity, per policy

## Priority 3 — ML part

- [ ] `ml_frequency.py` — imbalanced-classification pipeline (SMOTE, class weighting)
- [ ] `ml_attritional.py` — regression models on attritional claims
- [ ] `evt_gpd.py` — GPD fitting on excesses over threshold
- [ ] `ml_hybrid.py` — attritional/atypical classifier + weighted combination
- [ ] `pure_premium_ml.py` — combined pipeline output

## Priority 4 — comparison and reporting

- [ ] `glm_vs_ml.py` — side-by-side benchmarking on the test set
- [ ] `reference_policyholder.py` — reproduces the reference-driver premium quote
- [ ] `requirements.txt` and `renv.lock` for reproducibility

## Data

The original dataset is not included in this repository (proprietary teaching dataset).
Add `data/` to `.gitignore` and document the expected column schema in a `data/README.md`.
