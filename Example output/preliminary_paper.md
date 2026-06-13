# Preliminary Exploratory Analysis of the UCI Heart Disease Databases

## Abstract

This preliminary report analyzes the processed 14-feature version of the UCI Heart Disease databases pooled across Cleveland, Hungarian, Swiss, and Long Beach VA cohorts. The combined table contains 920 records, 14 documented clinical variables, a multiclass angiographic outcome `num`, a derived binary disease-presence outcome, and a retained `source_site` cohort indicator. Exploratory analysis shows strong clinical signal in chest pain type, maximum achieved heart rate, ST depression, and several categorical procedure-related variables. However, the dataset is also marked by substantial cohort imbalance and site-specific missingness. Disease prevalence ranges from 36.05% in the Hungarian cohort to 93.50% in the Swiss cohort. Missingness is severe for `ca`, `thal`, and `slope`, and cholesterol zeros appear to encode unavailable measurements for large site-specific slices. A reference logistic classifier excluding direct site labels achieved ROC-AUC 0.883 and average precision 0.889 under stratified random cross-validation, but leakage analysis indicates that random splits may overestimate external-site generalization. These findings support cautious machine-learning experiments with explicit preprocessing, leakage control, and validation sensitivity checks.

## Introduction

The UCI Heart Disease databases are a classic clinical tabular benchmark for coronary artery disease prediction. The dataset documentation describes 76 raw attributes, but historical experiments generally used 14 variables, including age, sex, chest pain type, resting blood pressure, cholesterol, fasting blood sugar, resting ECG, maximum heart rate, exercise-induced angina, ST depression, ST slope, number of vessels colored by fluoroscopy, thalassemia stress-test category, and the target variable `num`.

This preliminary paper focuses on the pooled processed files for Cleveland, Hungarian, Swiss, and Long Beach VA cohorts. The practical goal is to determine whether the processed dataset is suitable for clinical exploratory analysis and predictive modeling, and to identify data-quality and leakage risks before final model testing.

## Dataset Description

The processed modeling table contains 920 rows. The binary endpoint is derived as `disease_binary = num > 0`, following the common historical distinction between absence and presence of heart disease. The binary outcome is moderately balanced overall: 411 absent cases and 509 present cases. Multiclass modeling is less stable because the most severe class, `num = 4`, has only 28 records.

The cohort distribution is uneven in both size and outcome prevalence. Cleveland contributes 303 records with 45.87% disease prevalence, Hungarian contributes 294 records with 36.05%, Switzerland contributes 123 records with 93.50%, and Long Beach VA contributes 200 records with 74.50%. These differences are large enough to influence both descriptive statistics and model validation.

## Exploratory Data Analysis

The strongest descriptive pattern is the combination of meaningful clinical signal and strong cohort structure. Disease-present records show lower median maximum heart rate than disease-absent records, 128 versus 151 beats per minute. Disease-present records also show higher median ST depression, 1.1 versus 0.0. Chest pain type is the strongest feature-target association in p-value screening, with Benjamini-Hochberg adjusted q = 9.85e-57.

Numeric correlation analysis identifies `thalach` as the strongest numeric correlate of binary disease status, with absolute Pearson correlation 0.395. Categorical association analysis correctly identifies `num` as perfectly associated with `disease_binary`, because the binary label is derived from it; this also highlights why target-derived fields must be excluded from predictive feature matrices.

Missingness is a central limitation. `ca` is missing in 66.41% of rows, `thal` in 52.83%, and `slope` in 33.59%. Site-stratified missingness shows that `ca` is missing in 99.00% of Long Beach VA rows. Cholesterol values of zero occur in 172 records, including all Swiss records, and are clinically impossible as true measurements. These values should be treated as missing or unavailable, not as physiologic zeros.

The five most relevant graphs selected for later reporting are: dataset composition by target/site, missingness matrix, numeric boxplots by class, numeric correlation heatmap, and baseline ROC/precision-recall curves. They were chosen because they cover cohort structure, data quality, clinical signal, predictor relationships, and preliminary model feasibility. The five most relevant tables are: schema summary, missingness summary, clinical range validation, adjusted p-value screening, and baseline curve metrics.

## Methodological Considerations

This dataset requires fold-local preprocessing. Imputation, encoding, and scaling must be fit inside cross-validation folds. Direct `source_site` should be excluded from primary predictor matrices when the aim is transportable clinical prediction. However, site should still be retained for auditing and sensitivity analysis. Variables such as `ca` and `thal` may be procedure-adjacent depending on the intended clinical prediction moment; models should be tested with and without these fields if early screening is the target use case.

## Preliminary Results

A reference regularized logistic model excluding direct `source_site` achieved ROC-AUC 0.883 and average precision 0.889 under stratified cross-validation. This indicates substantial predictive signal in the 14-feature table. Nevertheless, this performance should be considered preliminary because site-specific missingness and outcome prevalence can leak cohort information even when direct site labels are excluded.

## Discussion

The dataset is useful for illustrating interpretable clinical tabular modeling, but it is not a simple IID benchmark. Strong class signal coexists with strong cohort bias. The most important practical implication is that model results should be framed as internal cross-validation estimates unless site-held-out validation or external validation is performed.

## Limitations

The analysis uses the processed 14-variable files rather than the raw 76-variable records. The project environment could not create a standard isolated venv from the available bundled runtime, so analysis was run through the bundled Codex Python runtime with documented package versions. LaTeX/PDF compilation was not attempted at this preliminary stage because the runtime/toolchain was not verified; Markdown is used as the paper artifact.

## Future Work

The next steps are to test regularized logistic regression and random forest models using leakage-conscious preprocessing, report accuracy, precision, ROC-AUC, average precision, and inference time, and compare random stratified validation with site-aware sensitivity checks where feasible.

## Conclusion

The UCI Heart Disease processed dataset contains meaningful clinical signal and supports binary disease-presence modeling. Its primary risks are site imbalance, structured missingness, clinically impossible coded values, and potential leakage through target timing or cohort proxies. Interpretable baselines and robust nonlinear models should be evaluated, but performance claims must be guarded by careful validation design.
