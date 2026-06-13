# Medical Dataset Analyses

Use this list to choose about 20 high-impact analyses for CSV and `.data` medical datasets. Each analysis should produce a chart, table, or statistical result and a dedicated Flywheel node.

1. Dataset composition by target class or endpoint.
2. Missing-value matrix and missingness percentage by feature.
3. Duplicate-row and duplicate-patient summary.
4. Feature type inventory: numeric, categorical, ordinal, datetime, identifier, free text.
5. Label imbalance analysis with counts, percentages, and imbalance ratio.
6. Numeric feature distribution histograms or density plots.
7. Categorical feature frequency plots for clinically important variables.
8. Boxplots by class for top numeric predictors.
9. Scatterplots for clinically meaningful numeric feature pairs.
10. Correlation heatmap for numeric variables.
11. Cramer's V or association heatmap for categorical variables.
12. P-value screening table for feature-target associations, using appropriate tests by dtype.
13. Multiple-testing-adjusted p-value table for exploratory screening.
14. Outlier detection plots using z-score, IQR, or robust MAD rules.
15. Clinical range validation table for impossible or suspicious values.
16. Temporal distribution plots for dates, visits, diagnosis times, or acquisition times.
17. Patient/record aggregation summary when repeated measurements exist.
18. FreeViz-style supervised projection for labeled data; use a documented approximation if FreeViz tooling is unavailable.
19. PCA or UMAP/t-SNE embedding projection for numeric feature structure, when sample size supports it.
20. ROC or precision-recall baseline curve for simple reference predictors, when a target is available.
21. Calibration plot for probabilistic baseline predictions, when applicable.
22. Pairplot or small-multiple scatter matrix for a limited set of high-signal features.
23. Stratified missingness analysis by class, site, cohort, or acquisition group.
24. Data leakage audit for columns that encode labels, future information, or post-outcome measurements.
