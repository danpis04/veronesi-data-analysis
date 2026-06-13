# Final Analysis Report: UCI Heart Disease Databases

## Abstract

This report analyzes the processed 14-feature UCI Heart Disease databases pooled across Cleveland, Hungarian, Swiss, and Long Beach VA cohorts. The combined table contains 920 records and supports binary disease-presence modeling using `disease_binary = num > 0`. Exploratory analysis found strong clinical signal in chest pain type, maximum achieved heart rate, ST depression, and related stress-test/procedure variables. It also found substantial validation risk: disease prevalence ranges from 36.05% to 93.50% by site, and missingness is strongly site-dependent. Two models were tested with fold-local preprocessing while excluding direct `source_site` and target-derived `num`: regularized logistic regression and random forest. Logistic regression achieved ROC-AUC 0.8833, accuracy 0.8054, precision 0.8300, and average precision 0.8895. Random forest achieved ROC-AUC 0.8830, accuracy 0.8087, precision 0.8184, and average precision 0.8801. Because logistic regression matched or slightly exceeded random forest on ROC-AUC and average precision while being much faster and more interpretable, it is the preferred model for this run.

## Dataset And Exploratory Findings

The dataset combines four processed clinical cohorts. Overall binary class balance is moderate, with 411 disease-absent and 509 disease-present records. Multiclass severity modeling is less reliable because class 4 contains only 28 records.

EDA showed that disease-present records had lower median maximum heart rate than disease-absent records, 128 versus 151, and higher median ST depression, 1.1 versus 0.0. Chest pain type was the strongest adjusted feature-target association, with BH-adjusted q = 9.85e-57. A baseline logistic ROC/PR analysis already suggested strong signal, with ROC-AUC 0.883 and average precision 0.889.

The principal data-quality concern is not duplicates, which were rare, but structured missingness. `ca` was missing in 66.41% of records, `thal` in 52.83%, and `slope` in 33.59%. Cholesterol values of zero affected 172 rows, including all Swiss records, and should be treated as unavailable rather than physiologic values. One resting blood-pressure zero was also flagged.

## Machine-Learning Methodology

The binary endpoint was `disease_binary`. The feature matrix excluded `num` because it defines the binary label, and excluded direct `source_site` to reduce direct cohort leakage. Impossible cholesterol and resting-blood-pressure zeros were converted to missing. Numeric features were imputed inside folds, and logistic regression additionally scaled numeric variables. Categorical/ordinal variables were imputed and one-hot encoded inside folds. Evaluation used 5-fold stratified cross-validation with ROC-AUC, average precision, accuracy, precision, wall-clock cross-validation time, and inference time for 200 rows.

## Model Comparison

| Model | Accuracy | Precision | ROC-AUC | Average Precision | CV Seconds | Inference ms / 200 rows |
|---|---:|---:|---:|---:|---:|---:|
| Regularized logistic regression | 0.8054 | 0.8300 | 0.8833 | 0.8895 | 0.159 | 5.716 |
| Random forest | 0.8087 | 0.8184 | 0.8830 | 0.8801 | 5.543 | 44.059 |

The two models are nearly tied in ROC-AUC. Random forest has slightly higher accuracy, but logistic regression has higher precision, higher average precision, slightly higher ROC-AUC, faster cross-validation, faster inference, and stronger clinical interpretability.

## Best Model

Regularized logistic regression is the best model for this run. It provides the clearest medical baseline because it is transparent, efficient, and performs at least as well as the random forest on threshold-independent metrics. The random forest remains a useful nonlinear comparator but does not justify its added complexity on these results.

## Limitations

Random stratified cross-validation may overestimate external performance. Site-held-out validation should be used before making transportability claims. The dataset does not fully define the clinical prediction moment, so procedure-adjacent predictors such as `ca` and `thal` may be inappropriate for early-screening scenarios. The local environment could not create a fully isolated standard venv from the available runtime, so scripts were executed through the bundled Codex Python runtime with documented versions.

## Conclusion

The processed UCI Heart Disease dataset is clinically signal-rich but cohort-confounded. Regularized logistic regression is the preferred current model, achieving ROC-AUC 0.8833 and average precision 0.8895 with fast inference and interpretability. Any final scientific claim should pair this result with site-aware validation and careful handling of missingness and target timing.
