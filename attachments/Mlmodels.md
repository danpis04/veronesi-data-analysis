# Medical Machine Learning Model Guide

Use this concise guide to select models for medical tabular, signal-derived, imaging-derived, or mixed clinical datasets. Prefer interpretable baselines first, then stronger nonlinear models when validation supports them.

1. Logistic Regression: best for binary clinical outcomes, small-to-medium tabular datasets, calibrated probabilities, and interpretable odds-style effects.
2. Regularized Logistic Regression: best when features are many, correlated, or sparse; use L1/L2/elastic-net to reduce overfitting.
3. Linear Support Vector Machine: best for high-dimensional sparse features, text-derived variables, or biomarker panels where linear separation is plausible.
4. Kernel Support Vector Machine: best for small-to-medium datasets with nonlinear boundaries; avoid for very large datasets or strict inference-latency needs.
5. Random Forest: best for robust tabular baselines, mixed feature types, nonlinear interactions, missingness-tolerant preprocessing, and feature-importance screening.
6. Extra Trees: best when Random Forest is strong but variance or training speed needs improvement; useful for noisy tabular medical data.
7. XGBoost: best for structured medical tabular data where top predictive accuracy is needed; strong with nonlinearities, interactions, missing values, and imbalanced classes.
8. LightGBM: best for large tabular datasets requiring fast training and strong gradient-boosting performance; use carefully with small datasets.
9. CatBoost: best for datasets with many categorical clinical variables and limited preprocessing budget.
10. Gradient Boosting Machine: best as a scikit-learn-native boosting baseline when XGBoost/LightGBM/CatBoost are unavailable.
11. Naive Bayes: best for text-derived clinical notes, symptom flags, or very small high-dimensional datasets requiring a quick probabilistic baseline.
12. k-Nearest Neighbors: best as a local-similarity baseline for normalized low-dimensional data; usually weak for high-dimensional or noisy clinical data.
13. Decision Tree: best for transparent rule-style baselines and clinical explanation, but prone to overfitting if used alone.
14. Linear Discriminant Analysis: best for low-dimensional continuous features with approximately Gaussian class structure and small sample sizes.
15. Quadratic Discriminant Analysis: best when classes have different covariance structures and the dataset is small but well-conditioned.
16. Multilayer Perceptron: best for moderate-to-large tabular or embedding features when nonlinear interactions are expected and interpretability is secondary.
17. Convolutional Neural Network: best for medical images, spectrograms, pathology tiles, and spatially structured signals.
18. Recurrent Neural Network or LSTM/GRU: best for sequential visits, physiological time series, and longitudinal measurements when order matters.
19. Transformer Model: best for clinical text, long sequences, multimodal embeddings, and large datasets where pretraining or transfer learning is available.
20. Survival Models: best when the endpoint is time-to-event; use Cox regression for interpretability and random survival forests or boosting for nonlinear risk.

Selection recommendations:

- For small labeled tabular datasets, start with regularized logistic regression and random forest.
- For medium or large tabular datasets, prioritize XGBoost, LightGBM, CatBoost, or Random Forest, with logistic regression as an interpretable baseline.
- For highly categorical clinical records, consider CatBoost or properly encoded gradient boosting.
- For imbalanced binary outcomes, prefer models with class weighting, threshold tuning, ROC-AUC, PR-AUC, calibration, and sensitivity-specificity reporting.
- For medical deployment, prefer the simplest model that reaches acceptable validation performance and can be explained, calibrated, and monitored.
