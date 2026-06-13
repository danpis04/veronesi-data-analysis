# Environment Setup

## Objective
Document the project execution environment for the UCI Heart Disease workflow.

## Setup Commands Attempted

```powershell
python --version
& 'C:\Users\danie\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' -m venv --system-site-packages .venv
& 'C:\Users\danie\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\pythonw.exe' -m venv --system-site-packages .venv
```

The regular `python` command is not available on PATH, and the reported app-runtime `python.exe` path is absent. The available bundled runtime exposes `pythonw.exe`, which can execute scripts when called through `Start-Process -Wait`, but it did not create a standard venv. A manual Windows venv launcher scaffold was tested and rejected because `.venv\Scripts\python.exe` could not find a base `python.exe` in the bundled runtime home.

## Requirements

The skill-required pinned `requirements.txt` was written at:

`C:\Users\danie\Documents\Codex\2026-06-13\files-mentioned-by-the-user-heart\requirements.txt`

Pinned modules:

```text
numpy==2.4.6
pandas==3.0.3
matplotlib==3.11.0
scikit-learn==1.9.0
scipy==1.17.1
seaborn==0.13.2
```

## Actual Runtime Used

Because a standard project venv could not be bootstrapped from the available runtime, analysis scripts were run through:

`C:\Users\danie\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\pythonw.exe`

The command pattern was:

```powershell
$p = Start-Process -FilePath '...\pythonw.exe' -ArgumentList 'work\<script>.py' -WorkingDirectory '<workspace>' -PassThru -WindowStyle Hidden
$p.WaitForExit()
$p.ExitCode
```

Observed package versions:

- Python: 3.12.13
- numpy: 2.3.5
- pandas: 3.0.1
- matplotlib: 3.11.0
- scikit-learn: 1.9.0
- scipy: 1.17.1
- seaborn: 0.13.2

## Reproducibility Notes

This is a reproducibility limitation: the workflow has a project requirements file and a documented runner, but not a fully functional isolated venv. All analysis and model code in this run is still Python code executed through the bundled Codex Python runtime.
