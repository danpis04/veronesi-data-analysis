---
name: veronesi-data-analysis
description: Flywheel-first medical dataset analysis workflow for CSV and .data files. Use when Codex must profile a medical dataset, create exploratory visual/statistical analyses, persist every data result as Flywheel nodes, generate a research-paper draft, select and test machine-learning models, and maintain strict node lineage with Python-in-venv execution.
---

# Veronesi Data Analysis

## Core Rules

- Manage graph state only through Flywheel skills and Flywheel MCP tools. Before creating, editing, linking, or attaching node artifacts, load and follow the relevant Flywheel skill.
- Create exactly one ancestorless node: the initial dataset node. Every later node must be a child of the node or nodes whose data, charts, tables, or conclusions it derives from.
- Create a new Flywheel node for every new data elaboration. Include the objective, source parent node IDs, method, produced data/results, observations, warnings, and output artifact references.
- Local output files are allowed for charts, tables, papers, logs, and reproducibility assets, but the same result must also be captured in a Flywheel node.
- Create a project virtual environment at the start. After bootstrapping the venv, run all Python code only through the venv interpreter. Shell commands are allowed for setup, package installation, file inspection, LaTeX compilation, and orchestration, but analysis/model code must be Python.
- Expect CSV and `.data` datasets. Infer `.data` delimiters and headers conservatively; document any ambiguity in the initial dataset node.
- Use actual Codex subagents for graphical analyses and model tests when subagent tools are available. If the host exposes no subagent tool, run the same units sequentially and record that fallback in the relevant nodes.
- Use an `outputs/` folder for generated charts, tables, papers, compiled PDFs, and reports.

## Required Attachments

Read these files before running the corresponding stage:

- `attachments/necessary_pyhton_modules.md`: baseline pinned modules for the venv and `requirements.txt`.
- `attachments/analisys_to_do.md`: candidate graphical and statistical analyses. Use it to assign graphical-analysis subagents.
- `attachments/Mlmodels.md`: general medical ML model guidance. Use it to select the two models for testing.

## Workflow

### 1. Initial Dataset Node

Create the first Flywheel node from the raw dataset. Include:

- Dataset table preview and full schema summary.
- Row/column counts, dtypes, target/label candidates, ID columns, date/time columns, and categorical/numeric splits.
- Missing values, duplicate rows, inconsistent codes, impossible clinical values, unit issues, and metadata gaps.
- Dataset quality observations and known limitations.
- Preliminary PIPO analysis when applicable: population/patients, inputs or predictors, procedures/interventions/processes, and outcomes/endpoints.

This node is the only root. Store its node ID and use it as the parent for all first-generation analyses.

### 2. Virtual Environment

Create a dedicated venv before analysis work. Generate or update `requirements.txt` from `attachments/necessary_pyhton_modules.md`, then add additional packages only when the dataset or selected model requires them.

Use the system Python only to create the venv. Afterward, invoke Python code with the venv interpreter, for example `.venv\Scripts\python.exe` on Windows. Document the exact setup commands and final dependency list in a Flywheel node derived from the initial dataset node.

### 3. Graphical Analysis Subagents

Read `attachments/analisys_to_do.md`. For each selected analysis, spawn one subagent with:

- The dataset path and relevant parent node ID.
- The specific analysis objective.
- The requirement to save files under `outputs/`.
- The requirement to create a child Flywheel node with method, graph/table, interpretation, warnings, and limitations.

Each subagent performs exactly one primary visual or statistical analysis. The main agent waits until all subagents finish, verifies that each produced node has the correct parent, and creates missing lineage only through Flywheel.

### 4. Summary Analysis Node

Create a summary node derived from all graphical-analysis nodes. Include:

- Consolidated interpretation of the generated plots/tables.
- High-impact insights, trends, anomalies, and limitations.
- Data quality risks and potential biases.
- Gallery or index of all generated charts/tables.
- Recommendations for further analysis.

### 5. Preliminary Paper Node

Create a paper node derived from the summary node. Prefer LaTeX and compile to PDF. If PDF compilation is impossible after a real attempt, generate a Markdown paper instead and document the blocker in the node.

The paper should be about 4,000 words and include title, abstract, introduction, dataset description, exploratory data analysis, methodological considerations, preliminary results, discussion, limitations, future work, and conclusion.

Select the five most relevant graphs and five most relevant data tables. Include them in the paper and explain in the node why they were chosen. Attach or reference the LaTeX source, compiled PDF when available, or Markdown fallback.

### 6. Model Selection Node

Read `attachments/Mlmodels.md`. Starting from the latest summary/paper node, select the two most suitable models for the dataset using:

- Dataset type, sample size, feature types, missingness, and label availability.
- Expected accuracy and ROC-AUC suitability.
- Interpretability needs in a medical context.
- Inference efficiency and deployment constraints.
- Evidence from prior nodes.

Create a model-selection node with the two chosen models and the rationale.

### 7. Model Testing Subagents

Spawn one subagent per selected model. Each subagent must:

- Implement a working Python example in the venv.
- Train/test on the dataset or a documented representative subset.
- Use clinically appropriate splits and leakage checks where feasible.
- Optimize ROC-AUC when the task is binary or multiclass classification and ROC-AUC is meaningful.
- Report accuracy, precision, ROC-AUC when applicable, efficiency, inference time, and implementation details.
- Create a Flywheel child node derived from the model-selection node and any dataset/feature nodes used.

The main agent waits for both model-testing subagents and verifies node lineage.

### 8. Final Paper And Report Nodes

Update the paper using the preliminary paper node plus both model-testing nodes. Add:

- Machine-learning methodology.
- Model descriptions and implementation details.
- Metrics comparison, including accuracy, precision, ROC-AUC when applicable, and inference time.
- Best-model discussion and selection rationale.
- Experiment limitations and future model improvements.

Generate updated outputs: final LaTeX source or Markdown fallback, final PDF when compilation succeeds, updated summary node, and final workflow report node.

## Node Content Template

For every analysis node, use this structure:

```markdown
## Objective
## Parent Data Sources
## Method
## Outputs
## Results
## Interpretation
## Warnings And Limitations
## Reproducibility Notes
```

When a node derives from multiple parents, attach all parent edges through Flywheel and state what each parent contributed.
