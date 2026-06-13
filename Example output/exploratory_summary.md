# Exploratory Summary

## Consolidated Interpretation

The combined processed UCI Heart Disease table contains 920 records from four clinical sites and supports a binary disease-presence task derived from `num > 0`. The strongest overall finding is not merely that the predictors are clinically informative, but that site structure is deeply entangled with both outcomes and missingness. Disease prevalence ranges from 36.05% in the Hungarian cohort to 93.50% in the Swiss cohort, while missingness in variables such as `ca`, `thal`, and `slope` is concentrated by site.

Exploratory clinical signal is clear. Disease-present records have lower median maximum heart rate (`thalach`, 128 vs 151) and higher median ST depression (`oldpeak`, 1.1 vs 0.0). Chest pain type (`cp`) is the strongest feature-target association in the p-value screen, with Benjamini-Hochberg adjusted q = 9.85e-57. Numeric correlation also identifies `thalach` as the strongest numeric correlate of the binary endpoint.

Data quality risk is also clear. `ca` is missing in 66.41% of rows, `thal` in 52.83%, and `slope` in 33.59%. Cholesterol values of zero occur in 172 records, including all Swiss records, and likely encode unavailable data rather than physiologic values. One resting blood pressure value is zero and should be treated as invalid/missing.

The baseline cross-validated logistic model excluding direct `source_site` achieved ROC-AUC 0.883 and average precision 0.889. This supports the feasibility of machine-learning experiments, but the leakage audit warns that random cross-validation can still overestimate external generalization because missingness and procedure-adjacent features may indirectly encode site and target timing.

## High-Impact Insights

- The binary classification task is feasible and moderately balanced overall: 411 absent vs 509 present.
- Multiclass severity modeling is less stable because class 4 has only 28 rows.
- `cp`, `thalach`, `oldpeak`, and several categorical stress-test/procedure-related features are high-signal.
- Site prevalence and site-specific missingness are the main threats to honest validation.
- Complete-case analysis is inappropriate because it would remove too much data and bias toward better-measured sites.

## Data Quality Risks And Biases

- Cohort imbalance: disease prevalence differs sharply by source site.
- Structured missingness: missingness patterns can act as cohort proxies.
- Clinical coding issue: cholesterol zero likely means missing/unavailable for entire site slices.
- Target timing ambiguity: `ca` and `thal` may be unavailable at early screening time and should be evaluated with the intended prediction moment in mind.
- Random split optimism: ordinary stratified cross-validation can mix site-specific signatures across folds.

## Gallery And Tables

Representative generated outputs:

- `analysis_01_composition_chart.png`
- `analysis_02_missingness_chart.png`
- `analysis_08_boxplots_by_class_chart.png`
- `analysis_10_correlation_chart.png`
- `analysis_19_baseline_curves_chart.png`
- `analysis_20_leakage_audit_chart.png`
- `schema_summary.csv`
- `missingness_summary.csv`
- `clinical_range_validation.csv`
- `analysis_13_adjusted_pvalues_table.csv`
- `analysis_19_baseline_curves_metrics.csv`

## Recommendations

Use regularized logistic regression as the interpretable baseline and a random forest as the nonlinear tabular comparator. Exclude `num`, do not use direct `source_site` as a predictor for primary transportability claims, convert impossible cholesterol/blood-pressure values to missing, and fit all imputers/encoders inside cross-validation folds. Report both stratified random cross-validation and, where possible, site-held-out sensitivity checks.
