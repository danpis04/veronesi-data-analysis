# Final Workflow Report

## Flywheel Lineage

- Root dataset node: `6ee8b205-542d-5c51-baf1-eecf740deb5c` (`restless-disk-1491`)
- Environment node: `e44bd807-c1b0-5536-946c-99af7cc3b3a9`
- Exploratory analysis nodes: 20 committed child nodes, analyses 01-20
- Summary node: `97fae16a-514c-5781-bbd4-8687fe45167d`
- Preliminary paper node: `49a67385-55c5-57bf-84ea-57a0d8fc5eb0`
- Model selection node: `33a56555-3ac2-5ca6-827f-339374526da2`
- Logistic model node: `7236ac0c-d9a4-5146-a9e0-c2a0a538b3f7`
- Random forest model node: `9bc91bdc-b229-50a3-ab0a-a5bea2a464ee`

## Local Outputs

Important outputs are stored in:

`C:\Users\danie\Documents\Codex\2026-06-13\files-mentioned-by-the-user-heart\outputs`

Key deliverables:

- `combined_processed_heart_disease.csv`
- `dataset_profile.md`
- `exploratory_summary.md`
- `preliminary_paper.md`
- `model_comparison_metrics.csv`
- `model_comparison_roc.png`
- `model_testing_summary.md`
- `final_paper.md`
- `final_workflow_report.md`

## Main Findings

- The combined processed dataset has 920 rows from four sites.
- Binary disease prevalence is 55.33% overall but varies sharply by site.
- Missingness is severe and site-structured for `ca`, `thal`, and `slope`.
- Chest pain type, maximum heart rate, and ST depression are high-signal.
- Logistic regression and random forest tie closely on ROC-AUC.
- Logistic regression is preferred because it is faster, more interpretable, and slightly better on ROC-AUC and average precision.

## Known Limitations

- Standard venv creation was blocked by the available bundled Python layout.
- A worker-created empty child node named `UCI Heart Disease Dataset - Initial Profile` appears under the root; it is not a second root and was not removed during the run.
- Markdown was used for papers instead of compiled PDF because LaTeX was not verified in this environment.
