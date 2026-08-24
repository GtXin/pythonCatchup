---
title: pythonNotes
tags:
  - python
  - qlib
  - quant
  - study-notes
status: active
---

# pythonNotes

## 1. Session Overview

### 1.a Purpose

- Catch up Python min less than 5 hours; 
- 20-80 rule 
- provide a knowledge tree for quick checking
- anything python new in the future goes here
### 1.b Assumed Background

-  C++ - 5 yr
-  OOP - 15 yr
-  Mid-level software engineering experience - 3 yr
-  AI tool fluent - 2 yr
-  Passionate - 46 yr
### 1.c Target Outcome

- Vibe coding is a must
- accountable at each class level 
- able to publish interesting repos   
- support the software engineering needs for Eyegorithm and Quant 

### 1.d Suggested Timebox

- 20 80 rule 
- 5 hours condense
### 1.e What Ready For Qlib Means

- Can read a Qlib example repo without getting blocked by Python syntax.
- Can explain the flow: raw data -> features -> labels -> model -> prediction -> strategy -> backtest.
- Can use Pandas to check date index, missing values, rolling windows, shift, and joins.
- Can spot basic leakage risk before trusting a result.
- Can run an existing Qlib example, inspect outputs, and know where to modify config.
- Can debug import, environment, data path, and DataFrame shape issues in VS Code.
- Can incorporate the learned patterns into a new package or repo without copying blindly.

### 1.f Key Rules And Tags

> [decision] This document stays as one living Markdown note. Do not split into multiple notes unless explicitly requested.

> [workflow] Note-taking style
>
> - Step 1: write compact notes.
>   - System: Obsidian Markdown note.
>   - Path: `C:\pythonCatchup\pythonNotes.md`.
>   - Verify: bullets stay short and easy to scan.
>
> - Step 2: prefer concrete material.
>   - System: learning record.
>   - Path: current section being edited.
>   - Verify: commands, runnable examples, mistakes, decisions, or open questions are present.
>
> - Step 3: remove filler.
>   - System: documentation style.
>   - Path: current section being edited.
>   - Verify: no long explanation unless it directly helps execution or understanding.

> [concept] **Note tags**
>
> - `[concept]`: definition or mental model.
> - `[decision]`: chosen tool, convention, default, or tradeoff.
> - `[workflow]`: executable step-by-step process.
> - `[execution]`: command run, check performed, output observed, or next verification step.
> - `[note]`: contextual reminder, caveat, gotcha, or short observation.
> - `[new filetype]`: file format purpose, syntax, and repo usage.
> - `[example]`: compact sample code, config, command, or data.
> - `[convention]`: naming, style, layout, or team-agreed coding/documentation convention.

> [concept] **Live session**
>
> - A live session is the current Codex-user interaction where commands are actually run against this local repo or machine.
> - If a command is executed during the live session, record what happened in a nearby `[execution]` block.
> - Execution summaries are facts from this machine, not generic instructions.

> [concept] **First-appearance rule**
>
> - Define important terms where they first appear.
> - Later sections should refer back or add only new context.
> - Avoid scattering duplicate definitions across the document.

> [concept] **Workflow shape**
>
> - Workflow steps are numbered.
> - Each step should include impacted system, relevant path, and verification.
> - Add a blank quoted line between steps.
>
> > [example] Standard workflow step shape
> >
> > ```md
> > > - Step 1: action.
> > >   - System: impacted tool or runtime.
> > >   - Path: relevant file, folder, executable, or environment path.
> > >   - Verify: expected result or check.
> > ```

> [concept] **Example nesting**
>
> - Put examples inside the tag they explain when useful.
> - Use `> > [example]` inside parent blocks like `[new filetype]`.
> - Filetype examples should show file contents or syntax only.
> - Commands that act on files belong in `[workflow]` or `[execution]`.

> [concept] **Tag recursion**
>
> - Tags are independent building blocks.
> - Tags may be nested recursively when useful.
> - Nesting is optional; use it only when it makes the note clearer.
> - Avoid forcing a rigid hierarchy between tags.

## 2. Environment Setup

### 2.a Tool Choice

> [concept] **`uv`** is a fast Python project tool: Python version manager, virtual environment creator, package installer, and command runner.

> [decision] Environment tool choice
>
> - Primary: `uv`
> - Fallback: `python -m venv` + `pip`
> - Reason: faster install, cleaner workflow, reproducible setup.

> [workflow] Choose environment tool
>
> - Step 1: use `uv` for normal setup.
>   - System: package manager and Python environment tooling.
>   - Path: `C:\Users\xinwe\.local\bin\uv.exe`.
>   - Verify: `uv --version` prints a version after shell restart.
>
> - Step 2: use `python -m venv` + `pip` only if `uv` is unavailable.
>   - System: built-in Python tooling.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: `.venv` exists and `python --version` works inside the activated environment.

### 2.b Install uv

> [concept] **`cmd` and PowerShell** are both Windows shells. A shell is a program that takes user commands and asks the operating system to run programs, manage files, and set environment variables. PowerShell is newer and better for scripting.

> [workflow] Install `uv`
>
> - Step 1: open PowerShell from the Start Menu.
>   - System: Windows shell.
>   - Path: `PowerShell`.
>   - Verify: terminal window is open and accepts commands.
>
> - Step 2: run `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`.
>   - System: PowerShell installer process.
>   - Path: installer URL `https://astral.sh/uv/install.ps1`.
>   - Verify: installer prints `everything's installed!`.
>
> > [syntax] `powershell` starts a PowerShell process; `-ExecutionPolicy ByPass` allows this installer script for that process; `-c` runs the quoted command; `irm` downloads the script; `| iex` executes it.
>
> - Step 3: close and reopen PowerShell if `uv` is not found.
>   - System: Windows user PATH refresh.
>   - Path: `C:\Users\xinwe\.local\bin\`.
>   - Verify: `uv --version` prints version text with no error.
>
> - Step 4: find the executable path.
>   - System: Windows command lookup.
>   - Path: `C:\Users\xinwe\.local\bin\uv.exe`.
>   - Verify: `Get-Command uv` in PowerShell, or `where uv` in `cmd`.

> [note] If VS Code was already open before installing `uv`, close and reopen VS Code so the integrated terminal reloads the updated PATH.

> [execution] `uv` installed successfully.
>
> - Version: `uv 0.12.5`
> - Path: `C:\Users\xinwe\.local\bin\uv.exe`
> - Also installed: `uvx.exe`, `uvw.exe`
> - Current shell did not find `uv` on PATH yet.
> - User PATH contains `C:\Users\xinwe\.local\bin`.
> - If VS Code was open before install, close and reopen VS Code so its terminal sees the updated PATH.
> - Next check after reopening PowerShell: `uv --version`

### 2.c Python Version

> [concept] **Python version** matters because package compatibility, Qlib examples, and local tooling can behave differently across versions.

> [decision] Python version choice
>
> - Target: Python 3.11
> - Minimum: Python 3.10
> - Reason: modern enough for current tooling, conservative enough for library compatibility.

> [workflow] Install Python and confirm project interpreter
>
> - Step 1: install target Python with `uv python install 3.11`.
>   - System: `uv` Python manager.
>   - Path: `C:\Users\xinwe\AppData\Roaming\uv\python\`.
>   - Verify: install finishes with a `CPython 3.11.x` message.
>
> - Step 2: list available Python versions with `uv python list`.
>   - System: `uv` Python manager.
>   - Path: `uv` managed Python registry.
>   - Verify: `cpython-3.11.x-windows-x86_64-none` appears.
>
> - Step 3: find the installed Python path with `uv python find 3.11`.
>   - System: `uv` Python resolver.
>   - Path: returned `python.exe` path under `C:\Users\xinwe\AppData\Roaming\uv\python\`.
>   - Verify: command prints a concrete `python.exe` path.
>
> - Step 4: run Python inside this repo with `uv run python --version`.
>   - System: repo environment and `uv` command runner.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: output is `Python 3.11.x`; if `.venv` does not exist, `uv run` may create it.

> [concept] **A virtual environment**, usually `.venv`, is a project-local Python environment that keeps this repo's packages separate from global Python and other repos. Summary: `.venv` is a folder containing this repo's Python executable, installed packages, and activation scripts. Installing a new global Python elsewhere on `C:\` should not affect this repo as long as VS Code, terminal commands, and scripts use `.venv` or `uv run`.

> [execution] Python 3.11 installed and verified with `uv`.
>
> - Installed: `CPython 3.11.16`
> - Interpreter path: `C:\Users\xinwe\AppData\Roaming\uv\python\cpython-3.11-windows-x86_64-none\python.exe`
> - Check: `uv python find 3.11`
> - Result: found the Python 3.11 interpreter above.
> - Check: `uv run python --version`
> - Result: `Python 3.11.16`
> - Side effect: `uv run` created the project virtual environment at `.venv`.
> - PATH note: `uv` warned that `C:\Users\xinwe\.local\bin` was not active in the current shell PATH yet.

### 2.d Create Virtual Environment (optional if already created)

> [concept] **Creating `.venv`** makes the repo-local Python environment explicit. In this repo, `.venv` may already exist because `uv run python --version` created it during `2.c`.

> [workflow] Create `.venv`
>
> - Step 1: create `.venv` only if missing with `uv venv --python 3.11`.
>   - System: `uv` virtual environment creator.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: command creates `.venv` with a Python 3.11 environment.

> [workflow] Verify `.venv`
>
> - Step 1: check whether `.venv` exists.
>   - System: filesystem.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: folder exists in repo root.
>
> - Step 2: check the repo Python version with `uv run python --version`.
>   - System: `uv` command runner.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: output is `Python 3.11.x`.

> [workflow] Activate `.venv`
>
> - Step 1: activate `.venv` only when running manual terminal commands.
>   - System: PowerShell session.
>   - Path: `C:\pythonCatchup\.venv\Scripts\Activate.ps1`.
>   - Command: `.venv\Scripts\Activate.ps1`
>   - Verify: terminal prompt shows `(pythonCatchup)`, or `python --version` prints `Python 3.11.x`.
>
> - Step 2: skip manual activation when using `uv run`.
>   - System: `uv` command runner.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Command: `uv run python --version`
>   - Verify: command runs inside the project environment.

> [note] Use the next workflow only when the activated terminal prompt shows an old repo/project name.

> [workflow] Rename `.venv` prompt by recreating environment
>
> - Step 1: recreate `.venv` with `uv venv --python 3.11 --clear --prompt pythonCatchup`.
>   - System: `uv` virtual environment creator.
>   - Path: `C:\pythonCatchup\.venv\`.
>   - Verify: command prints `Creating virtual environment at: .venv`.
>
> - Step 2: reinstall dependencies with `uv pip install -r requirements.txt`.
>   - System: `uv` pip-compatible installer.
>   - Path: `C:\pythonCatchup\requirements.txt`.
>   - Verify: packages install into `.venv`.
>
> - Step 3: verify prompt metadata in `.venv\pyvenv.cfg`.
>   - System: venv metadata.
>   - Path: `C:\pythonCatchup\.venv\pyvenv.cfg`.
>   - Verify: file contains `prompt = pythonCatchup`.
>
> - Step 4: verify runtime and pandas.
>   - System: `.venv` Python runtime.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: `uv run python` uses `.venv` and pandas imports.

> [execution] Recreated `.venv` with repo prompt name
>
> - Command: `uv venv --python 3.11 --clear --prompt pythonCatchup`
> - Result: `.venv` recreated with `CPython 3.11.16`.
> - Command: `uv pip install -r requirements.txt`
> - Result: reinstalled `pandas==3.0.5` and transitive packages including `numpy==2.4.6`.
> - Check: `.venv\pyvenv.cfg`
> - Result: contains `prompt = pythonCatchup`.
> - Check: `uv run python -c "import pandas as pd; print(pd.__version__)"`
> - Result: `3.0.5`.

### 2.e Install Dependencies

> [concept] **Runtime** is the program that actually runs code. For this repo, the Python runtime should be `C:\pythonCatchup\.venv\Scripts\python.exe` or `uv run python`.

> [concept] **Dependencies** are packages or tools the project environment needs. Runtime dependencies are imported by project code, like `pandas`. Developer dependencies are used by engineers and tools, like `ruff` for formatting/linting or `pytest` for tests. In this repo, both kinds can start in `requirements.txt` and install into `.venv`.

> [note] `pandas` and `ruff` are both dependencies in the broad sense. Difference: `pandas` is usually imported by Python code; `ruff` is usually run as a command-line executable from `.venv\Scripts\ruff.exe`.

> [new filetype] TOML is a human-readable config format made of sections like `[project]` and key-value settings like `name = "python-notes"`. In this repo, `pyproject.toml` stores Python project metadata, dependency config, and tool settings such as `[tool.ruff]`.
>
> > [example] Minimal `pyproject.toml` shape
> >
> > ```toml
> > # Project metadata and runtime requirements.
> > [project]
> > name = "python-notes"
> > version = "0.1.0"
> > requires-python = ">=3.11"
> > # Packages needed when the project code runs.
> > dependencies = ["pandas", "numpy"]
> >
> > # Packages needed by engineers while developing.
> > [dependency-groups]
> > dev = ["pytest", "ruff"]
> >
> > # Tool-specific config.
> > [tool.ruff]
> > line-length = 88
> > ```

> [new filetype] `requirements.txt` is a plain text dependency list used by `pip`-style installers. In this repo, it is the simple starter place for runtime packages before moving dependency metadata into `pyproject.toml`.
>
> > [example] Minimal `requirements.txt` shape
> >
> > ```text
> > # Runtime packages imported by repo code.
> > pandas
> > numpy
> >
> > # Testing / tooling packages can start here, then move to dev dependency groups later.
> > pytest
> > ruff
> > ```

> [workflow] Simple path: install dependencies from `requirements.txt`
>
> - Step 1: check `requirements.txt` has package names, not only comments.
>   - System: dependency manifest.
>   - Path: `C:\pythonCatchup\requirements.txt`.
>   - Verify: file contains packages such as `pandas`, `numpy`, `pytest`, or `ruff`.
>
> - Step 2: run `uv pip install -r requirements.txt`.
>   - System: `uv` pip-compatible installer.
>   - Path: `C:\pythonCatchup\requirements.txt`.
>   - Verify: packages install into `C:\pythonCatchup\.venv\Lib\site-packages\`.
>
> - Step 3: verify imports with `uv run python -c "import pandas, numpy; print('ok')"`.
>   - System: Python import system.
>   - Path: `C:\pythonCatchup\.venv\Lib\site-packages\`.
>   - Verify: command prints `ok`.

> [execution] Dependency install from `requirements.txt`
>
> - File update: added `pandas` to `requirements.txt`.
> - Command: `uv pip install -r requirements.txt`
> - Result: installed `pandas==3.0.5` and transitive packages including `numpy==2.4.6`.
> - Command: `uv run python -c "import pandas, numpy; print('ok')"`
> - Result: `ok`
> - Installed packages observed: `pandas`, `numpy`, `python-dateutil`, `six`, `tzdata`.

### 2.f Run Commands

> [workflow] Run project commands with `uv run`
>
> - Step 1: check the repo Python runtime with `uv run python --version`.
>   - System: `uv` command runner and `.venv` Python runtime.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: output is `Python 3.11.x`.
>
> - Step 2: run tests with `uv run pytest`.
>   - System: test runner.
>   - Path: `C:\pythonCatchup\tests\`.
>   - Verify: pytest starts and reports pass/fail results.
>
> - Step 3: run lint checks with `uv run ruff check .`.
>   - System: Ruff linter.
>   - Path: `C:\pythonCatchup\`.
>   - Verify: Ruff reports no issues or lists files to fix.
>
> - Step 4: format code with `uv run ruff format .`.
>   - System: Ruff formatter.
>   - Path: `C:\pythonCatchup\`.
>   - Verify: Ruff formats files or reports they are unchanged.

> [execution] `2.f` command run summary
>
> - Command: `uv run python --version`
> - Result: `Python 3.11.16`
> - Command: `uv run pytest`
> - Result: failed because `pytest` is not installed in `.venv`.
> - Command: `uv run ruff check .`
> - Result: failed because `ruff` is not installed in `.venv`.
> - Command: `uv run ruff format .`
> - Result: failed because `ruff` is not installed in `.venv`.
> - Next step: install dev tools before rerunning tests/lint/format.

### 2.g Fallback Without uv

> [note] Use this only when `uv` is unavailable or blocked. Normal repo workflow should prefer `uv` and `uv run`.

```powershell
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 2.h VS Code PowerShell Terminal Verification

> [workflow] Verify repo environment from VS Code PowerShell terminal
>
> - Step 1: open VS Code integrated terminal with PowerShell.
>   - System: VS Code terminal.
>   - Path: `C:\pythonCatchup\`.
>   - Verify: terminal starts in repo root, or `pwd` prints `C:\pythonCatchup`.
>
> - Step 2: check `uv` is visible from VS Code with `uv --version`.
>   - System: VS Code process PATH.
>   - Path: `C:\Users\xinwe\.local\bin\uv.exe`.
>   - Verify: command prints `uv 0.12.5` or newer.
>
> - Step 3: check repo Python with `uv run python -c "import sys; print(sys.executable); print(sys.version)"`.
>   - System: `uv` command runner and `.venv` Python runtime.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: executable path points inside `.venv` and version is `Python 3.11.x`.
>
> - Step 4: check pandas import and version with `uv run python -c "import pandas as pd; print(pd.__version__)"`.
>   - System: Python import system.
>   - Path: `C:\pythonCatchup\.venv\Lib\site-packages\`.
>   - Verify: command prints installed pandas version.
>
> - Step 5: check no hardcoded local path is required.
>   - System: repo portability.
>   - Path: `C:\pythonCatchup\`.
>   - Verify: commands work from repo root using relative project files and `.venv`.

> [execution] Pandas verification
>
> - Command: `uv run python -c "import pandas as pd; print(pd.__version__)"`
> - Result: `3.0.5`

## 3. VS Code IDE Setup And Code Standards

### 3.a Recommended VS Code Extensions

> [concept] **A VS Code extension** is an add-on that teaches the editor new behavior, such as Python language support, linting, formatting, notebooks, Git tools, or better file navigation.

> [concept] **Linting** is static code checking: a tool reads code before it runs and flags likely bugs, unused imports, style issues, unsafe patterns, or inconsistent structure.

> [decision] Minimal VS Code extension set
>
> - Required: `ms-python.python`
> - Strongly recommended: `charliermarsh.ruff`
> - Optional for notebooks: `ms-toolsai.jupyter`
>
> > [note] Extension function
> >
> > - `ms-python.python`: Python language support, interpreter selection, debugging, test discovery, and environment awareness.
> > - `charliermarsh.ruff`: linting, formatting, import cleanup, and fast code-quality feedback.
> > - `ms-toolsai.jupyter`: notebook editing and interactive Python exploration when `.ipynb` is useful.

> [note] Keep the extension set small. Add extensions only when they support the current Python/Qlib workflow.

> [workflow] Install recommended VS Code extensions
>
> - Step 1: install Python extension `ms-python.python`.
>   - System: VS Code extension marketplace.
>   - Path: VS Code Extensions panel.
>   - Verify: Python interpreter selection and Python language features are available.
>
> - Step 2: install Ruff extension `charliermarsh.ruff`.
>   - System: VS Code extension marketplace.
>   - Path: VS Code Extensions panel.
>   - Verify: Ruff lint/format integration appears for Python files.
>
> - Step 3: install Jupyter extension `ms-toolsai.jupyter` only if using notebooks.
>   - System: VS Code extension marketplace.
>   - Path: VS Code Extensions panel.
>   - Verify: `.ipynb` files open with notebook support.

> [workflow] Alternative: install VS Code extensions from command line
> >![[Pasted image 20260823132542.png]]
>
> - Step 1: check VS Code CLI with `code --version`.
>   - System: VS Code command-line interface.
>   - Path: `C:\Users\xinwe\AppData\Local\Programs\Microsoft VS Code\bin\code.cmd`.
>   - Verify: command prints VS Code version.
>
> - Step 2: install Python extension with `code --install-extension ms-python.python`.
>   - System: VS Code extension installer.
>   - Path: VS Code user extensions folder.
>   - Verify: command reports installed or already installed.
>
> - Step 3: install Ruff extension with `code --install-extension charliermarsh.ruff`.
>   - System: VS Code extension installer.
>   - Path: VS Code user extensions folder.
>   - Verify: command reports installed or already installed.
>
> - Step 4: list relevant installed extensions with `code --list-extensions --show-versions | Select-String "ms-python.python|charliermarsh.ruff|ms-toolsai.jupyter"`.
>   - System: VS Code extension registry.
>   - Path: VS Code user extensions folder.
>   - Verify: expected extension IDs and versions appear.

> [execution] VS Code extension installation
>
> - Command: `code --version`
> - Result: VS Code CLI available.
> - Command: `code --install-extension ms-python.python`
> - Result: already installed, `ms-python.python@2026.4.0`.
> - Command: `code --install-extension charliermarsh.ruff`
> - Result: installed, `charliermarsh.ruff@2026.74.0`.
> - Jupyter: not installed because it is optional until notebooks are needed.

### 3.b Interpreter Selection

> [concept] **VS Code interpreter selection** means choosing which `python.exe` VS Code uses for running files, debugging, resolving imports, discovering tests, and powering Python editor features.

> [decision] VS Code should use the repo interpreter, not global Python.
>
> - Repo interpreter: `C:\pythonCatchup\.venv\Scripts\python.exe`
> - Base Python came from `uv`: `C:\Users\xinwe\AppData\Roaming\uv\python\...`
> - Repo environment lives at: `C:\pythonCatchup\.venv\`
> - Reason: keeps VS Code aligned with the same Python and packages used by `uv run`.
>
> > [note] `2.c` and `2.d` created or confirmed the interpreter. `3.b` is only about telling VS Code to use it.

> [note] If running plain `python` in the VS Code PowerShell terminal, activate `.venv` first with `.venv\Scripts\Activate.ps1`. If using `uv run python`, manual activation is not required.

> [workflow] Select repo interpreter in VS Code
>
> - Step 1: open the Command Palette with `Ctrl + Shift + P`.
>   - System: VS Code command palette.
>   - Path: VS Code UI.
>   - Verify: command search box opens.
>
> - Step 2: run `Python: Select Interpreter`.
>   - System: Python extension.
>   - Path: `ms-python.python`.
>   - Verify: interpreter list opens.
>
> - Step 3: choose `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - System: VS Code Python environment selection.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: VS Code status bar shows the `.venv` Python interpreter.
>
> - Step 4: verify from VS Code PowerShell terminal after activation with `python -c "import sys; print(sys.executable)"`.
>   - System: VS Code integrated terminal and selected interpreter.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: printed path points to `.venv\Scripts\python.exe`.
>   - >![[Pasted image 20260823134428.png]]

### 3.c Formatting -Ruff and VS Code Extension

> [concept] **Ruff** is a Python code-quality tool with two main functions here: `ruff check` diagnoses code issues, and `ruff format` rewrites code layout. The VS Code Ruff extension is editor integration, while `ruff` installed in `.venv` is the actual project command-line tool. Extension = editor capability; `.venv` dependency = project capability. The extension can run Ruff-like checks in the background while editing, show issues in the VS Code UI, and call formatting/fixes on save or command. Background linting changes UI only; formatting or quick fixes may rewrite `.py` files in place. Ruff normally writes terminal output, not report files, unless explicitly redirected.

> [concept] **VS Code Problems panel** is a structured diagnostic stream from editor-connected tools, not strings printed by project code. Terminal output comes from commands/programs; Problems panel entries come from tools like Ruff, Python extension, or type checker and point to file, line, severity, and message.

> [note] Ruff name origin: likely from "rough prototype" -> "Ruff". Treat this as historical context, not a functional concept.

> [workflow] Simple path: add Ruff through `requirements.txt`
>
> - Step 1: add `ruff` to `requirements.txt`.
>   - System: dependency manifest.
>   - Path: `C:\pythonCatchup\requirements.txt`.
>   - Verify: file contains `ruff`.
>
> - Step 2: install with `uv pip install -r requirements.txt`.
>   - System: `uv` pip-compatible installer.
>   - Path: `C:\pythonCatchup\.venv\Scripts\ruff.exe`.
>   - Verify: `ruff.exe` exists in `.venv\Scripts`.
>
> - Step 3: verify Ruff with `uv run ruff --version`.
>   - System: `.venv` command-line tool.
>   - Path: `C:\pythonCatchup\.venv\Scripts\ruff.exe`.
>   - Verify: command prints Ruff version.

> [workflow] Structured path: add Ruff through `pyproject.toml`
>
> - Step 1: add `ruff` under `[dependency-groups].dev`.
>   - System: Python project metadata.
>   - Path: `C:\pythonCatchup\pyproject.toml`.
>   - Verify: `ruff` appears in the dev dependency group.
>
> - Step 2: run `uv sync`.
>   - System: `uv` dependency synchronizer.
>   - Path: `C:\pythonCatchup\pyproject.toml` and `C:\pythonCatchup\uv.lock`.
>   - Verify: `.venv` matches the locked project dependencies.
>
> - Step 3: verify Ruff with `uv run ruff check .` and `uv run ruff format .`.
>   - System: Ruff linter and formatter.
>   - Path: `C:\pythonCatchup\`.
>   - Verify: Ruff reports issues, formats files, or reports unchanged files.

> [new filetype] JSON is a strict key-value config/data format. In this repo, `.vscode/settings.json` stores workspace-level VS Code settings that connect the editor to `.venv`, Python, and Ruff.
>
> > [example] Minimal VS Code Ruff settings
> >
> > ```json
> > {
> >   "ruff.importStrategy": "fromEnvironment",
> >   "ruff.interpreter": [".venv/Scripts/python.exe"],
> >   "[python]": {
> >     "editor.defaultFormatter": "charliermarsh.ruff",
> >     "editor.formatOnSave": true
> >   }
> > }
> > ```

> [workflow] Connect VS Code Ruff extension to repo Ruff
>
> - Step 1: set Ruff to load from the selected environment.
>   - System: VS Code workspace settings.
>   - Path: `C:\pythonCatchup\.vscode\settings.json`.
>   - Verify: `"ruff.importStrategy": "fromEnvironment"` is present.
>
> - Step 2: point Ruff extension at the repo interpreter.
>   - System: VS Code Ruff extension.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: `"ruff.interpreter": [".venv/Scripts/python.exe"]` is present.
>
> - Step 3: set Ruff as the Python formatter.
>   - System: VS Code formatter selection.
>   - Path: `C:\pythonCatchup\.vscode\settings.json`.
>   - Verify: `[python].editor.defaultFormatter` is `charliermarsh.ruff`.
>
> - Step 4: verify both sides exist.
>   - System: VS Code extension and `.venv` command-line tool.
>   - Path: `charliermarsh.ruff` extension and `C:\pythonCatchup\.venv\Scripts\ruff.exe`.
>   - Verify: `code --list-extensions --show-versions` shows Ruff extension, and `uv run ruff --version` prints Ruff version.

> [workflow] Hello Ruff demo
>
> - Step 1: create a tiny Python file with one intentional lint issue.
>   - System: repo script file.
>   - Path: `C:\pythonCatchup\scripts\hello_ruff.py`.
>   - Verify: file exists and runs.
>
> - Step 2: check the file with `uv run ruff check scripts\hello_ruff.py`.
>   - System: Ruff linter.
>   - Path: `C:\pythonCatchup\scripts\hello_ruff.py`.
>   - Verify: Ruff reports the unused import.
>
> - Step 3: fix the issue with `uv run ruff check scripts\hello_ruff.py --fix`.
>   - System: Ruff linter auto-fix.
>   - Path: `C:\pythonCatchup\scripts\hello_ruff.py`.
>   - Verify: Ruff reports the issue fixed.
>
> - Step 4: format and re-check the file.
>   - System: Ruff formatter and linter.
>   - Path: `C:\pythonCatchup\scripts\hello_ruff.py`.
>   - Verify: `ruff format` reformats if needed and `ruff check` reports all checks passed.

> [execution] Installed Ruff and pytest through `pyproject.toml`
>
> - File update: added `pandas` to `[project].dependencies` in `pyproject.toml`.
> - File update: added `ruff` and `pytest` to `[dependency-groups].dev` in `pyproject.toml`.
> - File update: added `ruff` and `pytest` to `requirements.txt` for the simple path.
> - Command: `uv sync`
> - Result: installed `ruff==0.16.4` and `pytest==9.1.1` into `.venv`.
> - Check: `uv run ruff --version`
> - Result: `ruff 0.16.4`
> - Check: `uv run pytest --version`
> - Result: `pytest 9.1.1`
> - Check: `uv run python -c "import pandas as pd; print(pd.__version__)"`
> - Result: `3.0.5`

> [execution] Connected VS Code Ruff extension to repo Ruff
>
> - File update: added Ruff workspace settings to `.vscode/settings.json`.
> - Setting: `"ruff.importStrategy": "fromEnvironment"`
> - Setting: `"ruff.interpreter": [".venv/Scripts/python.exe"]`
> - Setting: `[python].editor.defaultFormatter = "charliermarsh.ruff"`
> - Check: `.vscode/settings.json` parses as valid JSON.
> - Check: `.venv\Scripts\ruff.exe` exists.
> - Check: `uv run ruff --version`
> - Result: `ruff 0.16.4`
> - Check: `code --list-extensions --show-versions`
> - Result: `charliermarsh.ruff@2026.74.0` and `ms-python.python@2026.4.0`

> [execution] Hello Ruff demo
>
> - File created: `scripts\hello_ruff.py`
> - Command: `uv run ruff check scripts\hello_ruff.py`
> - Result: Ruff reported `F401` for unused `os` import.
> - Command: `uv run ruff format scripts\hello_ruff.py`
> - Result: `1 file left unchanged`.
> - Command: `uv run python scripts\hello_ruff.py`
> - Result: `hello, ruff`
> - Command: `uv run ruff check scripts\hello_ruff.py --fix`
> - Result: `Found 1 error (1 fixed, 0 remaining).`
> - Command: `uv run ruff format scripts\hello_ruff.py`
> - Result: `1 file reformatted`.
> - Command: `uv run ruff check scripts\hello_ruff.py`
> - Result: `All checks passed!`
> - Live edit: typed random invalid Python into `scripts\hello_ruff.py`.
> - Command: `uv run ruff check scripts\hello_ruff.py`
> - Result: Ruff reported `invalid-syntax` errors on the invalid line.

### 3.d Linting

> [concept] **Linting** is static code checking: Ruff reads Python files before they run and reports likely bugs, syntax errors, unused imports, style issues, or fixable code-quality problems.

> [note] No extra linting setup is needed right now. `3.c` already installed Ruff in `.venv`, installed the VS Code Ruff extension, and connected VS Code to the repo Ruff tool. In VS Code, Ruff extension coordinates linting through editor squiggles and the Problems panel; in terminal, use `uv run ruff check .`.

### 3.e Type Checking

> [concept] **Type checking** is static reasoning about value types before code runs. Pylance is the VS Code language server that provides Python intelligence: type checking, autocomplete, hover info, go-to-definition, import analysis, and Problems panel diagnostics. Pylance lives as a VS Code extension under `C:\Users\xinwe\.vscode\extensions\`, not inside `.venv`; it reads the selected interpreter `C:\pythonCatchup\.venv\Scripts\python.exe` to understand repo packages and types.

> [note] Type checking rationale: Ruff checks code quality and formatting, but Pylance checks type logic. It helps catch mistakes like passing `str` where `int` is expected, returning the wrong type, or forgetting to handle `None`. It becomes more useful when functions and variables have type hints.

### 3.f PEP 8

> [concept] **PEP 8** is Python's community style standard. It defines common naming, spacing, import, and layout conventions so Python code looks familiar across projects.

> [convention] Follow PEP 8 naming unless this repo later adopts a stronger local convention.
>
> - Files/modules: `snake_case.py`
> - Functions: `snake_case`
> - Variables: `snake_case`
> - Classes: `PascalCase`
> - Constants: `UPPER_SNAKE_CASE`
> - Private helpers: `_leading_underscore`
> - Tests: `test_*.py`
> - Scripts: `verb_noun_demo.py`
>
> > [example] Naming shape
> >
> > ```python
> > MAX_LOOKBACK_DAYS = 252
> >
> >
> > class FactorCalculator:
> >     pass
> >
> >
> > def calculate_return(close_price: float, previous_close: float) -> float:
> >     return close_price / previous_close - 1
> >
> >
> > def _validate_price(price: float) -> None:
> >     if price <= 0:
> >         raise ValueError("price must be positive")
> > ```

> [convention] PEP 8 essentials for this repo
>
> - Indentation: 4 spaces.
> - Line length: 88 characters, managed by Ruff.
> - Imports: standard library first, then third-party packages, then local project imports.
> - Blank lines: separate top-level functions/classes with two blank lines.
> - Whitespace: use spaces around normal assignment/operators, like `a = 1`; avoid extra spaces inside calls/brackets, like `func(x)` not `func( x )`.
> - Comments: explain why, not obvious what.
> - Docstrings: use for public functions/classes when behavior is not obvious.
> - Comparisons: use `is None` / `is not None` for `None` checks.
> - Exceptions: raise specific exceptions like `ValueError`, not broad generic errors.

> [note] Python comments use `#`. Python does not use `//` or `/* */` for comments. Use `#` for short human notes, and use triple-quoted docstrings `"""..."""` for module, class, or function documentation.

> [note] Type annotation spacing: use `name: type`, `name: type = value`, and `def f(x: int = 1) -> int:`. No space before `:`, one space after `:`, spaces around `=`, and spaces around `->`. Function call keyword arguments still use no spaces, like `f(x=1)`.

> [note] Prefer names that describe domain role, not implementation trivia: `daily_return`, `future_return`, `lookback_days`, `instrument`, `trade_date`, `signal_score`.

### 3.g Scripts Vs Reusable Code

> [concept] **`scripts/`** is for command-style code: small files you run to do one task, such as checking an environment, downloading data, trying an API call, or running a quick experiment. A script has an entry point and usually starts from "do this now."

> [concept] **Reusable code** belongs under `src/`: functions, classes, and modules that other code can import. Reusable code usually starts from "provide this behavior so many callers can use it."

> [decision] Default split for this repo:
> - Put one-off learning, checks, and local experiments in `scripts/`.
> - Put stable domain logic in `src/catchup/`.
> - Put tests for reusable logic in `tests/`.
> - Do not import important business/domain logic from `scripts/`; promote it into `src/` first.

> [workflow] Promote a script idea into reusable code
> - Step 1: start in `scripts/` when the idea is still exploratory.
>   - System: repo working files.
>   - Path: `C:\pythonCatchup\scripts\`.
>   - Verify: the script can run directly with `uv run python scripts\<name>.py`.
>
> - Step 2: identify the part that should be reused.
>   - System: Python code organization.
>   - Path: current script file.
>   - Verify: the reusable part can be described as a function with clear inputs and outputs.
>
> - Step 3: move reusable behavior into `src/catchup/`.
>   - System: local Python package.
>   - Path: `C:\pythonCatchup\src\catchup\`.
>   - Verify: scripts or tests import it from `catchup`, not from `scripts`.
>
> - Step 4: keep the script as a thin runner.
>   - System: repo command layer.
>   - Path: `C:\pythonCatchup\scripts\`.
>   - Verify: the script mostly parses inputs, calls reusable code, and prints or saves results.

> [example] Shape only
>
> ```text
> scripts/check_env.py          # run directly; command-style
> src/catchup/returns.py        # importable reusable logic
> tests/test_returns.py         # verifies reusable logic
> ```

### 3.h Environment Variables

> [concept] **An environment variable** is a named value supplied by the operating system or shell to a running program. Python code can read it at runtime, so the code does not need to hardcode local paths, API keys, or machine-specific settings.

> [concept] **A `.env` file** is a local text file that stores environment-style key/value pairs for one machine or one developer. It is useful for local settings, but it should usually be ignored by Git.

> [new filetype] `.env.example`
>
> `.env.example` is a committed template. It shows which environment variables the project expects, without storing private values.
>
> > [example] Minimal `.env.example`
> >
> > ```text
> > # Local Qlib data location. Each engineer sets this path for their own machine.
> > QLIB_PROVIDER_URI=C:\path\to\qlib_data
> >
> > # Example only. Real secrets go in `.env`, not in `.env.example`.
> > DATA_API_KEY=
> > ```

> [decision] Use environment variables for values that change by machine, account, dataset, deployment, or secret status. Keep stable code behavior in Python files, and keep local/private settings outside source code.

> [decision] For this repo:
> - Commit `.env.example`.
> - Do not commit `.env`.
> - Use placeholder values in notes and examples.
> - Do not paste real API keys, tokens, passwords, or private data paths into `pythonNotes.md`.

> [workflow] Create or update the environment template
> - Step 1: add variable names to `.env.example`.
>   - System: repo configuration template.
>   - Path: `C:\pythonCatchup\.env.example`.
>   - Verify: names are present, values are blank or fake placeholders.
>
> - Step 2: keep `.env` private.
>   - System: Git ignore rules.
>   - Path: `C:\pythonCatchup\.gitignore`.
>   - Verify: `.env` is ignored by Git.
>
> - Step 3: document what each variable means.
>   - System: study notes.
>   - Path: `C:\pythonCatchup\pythonNotes.md`.
>   - Verify: the variable has a short explanation without exposing private values.

> [workflow] Set a temporary environment variable in PowerShell
> - Step 1: set the variable for the current terminal session.
>   - System: PowerShell process environment.
>   - Path: current VS Code PowerShell terminal only.
>   - Command: `$env:QLIB_PROVIDER_URI = "C:\path\to\qlib_data"`
>   - Verify: `echo $env:QLIB_PROVIDER_URI` prints the same value.
>
> - Step 2: run Python from the same terminal.
>   - System: `.venv` Python runtime.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Command: `uv run python -c "import os; print(os.environ['QLIB_PROVIDER_URI'])"`
>   - Verify: Python prints the value set in Step 1.
>
> - Step 3: open a new terminal if needed.
>   - System: shell session state.
>   - Path: new VS Code PowerShell terminal.
>   - Verify: temporary variables from the old terminal do not automatically carry over.

> [note] Environment variables are runtime inputs. Changing an environment variable changes what the running program sees, but it does not edit Python source files.

### 3.i Section 3 Closeout

> [note] Section 3 closes the repo editing standard: VS Code is the editor, `.venv` is the selected interpreter, Ruff handles formatting/checking, Pylance handles Python intelligence/type analysis, PEP 8 gives naming/style conventions, `scripts/` stays command-style, `src/` holds reusable logic, and environment variables keep local/private settings outside source code.

## 4. Debugging Options

> [concept] **Debugging** is the process of locating why actual program behavior differs from expected behavior. It is not only "fixing errors"; it is building evidence about program state, control flow, data shape, and runtime configuration.

> [decision] Debugging options should escalate from simple to structured:
> - Use `print()` for quick visibility.
> - Read stack traces when Python crashes; the error type, message, and call chain usually point to the failing line and cause.
> - Use REPL/IPython for interactive exploration.
> - Use VS Code breakpoints when state and control flow matter.
> - Use pytest debugging when the behavior should become a repeatable test.
> - Use logging when visibility should stay in long-running scripts or workflows.

### 4.a Print Debugging - quick dirty view

> [concept] **Print debugging** means inserting temporary `print()` calls to expose program state while code runs. It is the fastest way to answer small questions like "did this line run?", "what is this value?", or "what shape is this data?"

> [workflow] Use print debugging
> - Step 1: print the location.
>   - System: Python runtime output.
>   - Path: VS Code PowerShell terminal.
>   - Verify: the message appears when the code reaches that line.
>
> - Step 2: print the value and its type or shape.
>   - System: Python runtime state.
>   - Path: the variable being inspected.
>   - Verify: output answers what the variable is at that exact moment.
>
> - Step 3: remove or replace the print after the question is answered.
>   - System: source code hygiene.
>   - Path: edited Python file.
>   - Verify: temporary debug prints are not left in reusable code.

> [example] Simple value check
>
> ```python
> price = 101.25
> print("debug price:", price, type(price))
> ```

> [example] Pandas shape check
>
> ```python
> print("rows/cols:", df.shape)
> print(df.head())
> ```

> [note] Print debugging is not a serious framework. It is a quick visibility tool. If the same print is useful repeatedly, turn it into logging, a test, or a clearer function boundary.

### 4.b REPL And IPython

> [concept] **A REPL** is an interactive runtime: Read, Evaluate, Print, Loop. It reads one expression or statement, runs it immediately, prints the result when appropriate, then waits for the next input.

> [concept] **IPython** is a richer Python REPL. It adds better display, command history, tab completion, help shortcuts, and friendlier exploration for data work.

> [decision] Use the plain Python REPL first. IPython is optional later. Use REPL when the question is small and interactive: checking syntax, testing one expression, inspecting an object, trying a pandas operation, or exploring a package API before writing code into a file.

> [workflow] Start and use the Python REPL from the repo
> - Step 1: open the VS Code PowerShell terminal in the repo.
>   - System: shell working directory.
>   - Path: `C:\pythonCatchup`.
>   - Verify: prompt shows `PS C:\pythonCatchup>`.
>
> - Step 2: start the repo Python runtime.
>   - System: `.venv` Python runtime through `uv`.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Command: `uv run python`
>   - Verify: the prompt changes to Python's `>>>`.
>
> - Step 3: run small checks interactively.
>   - System: live Python process memory.
>   - Path: current REPL session.
>   - Verify: each line runs immediately and prints results or errors.

> [workflow] Exit the Python REPL
> - Step 1: confirm the prompt is Python's `>>>`.
>   - System: live Python process.
>   - Path: current REPL session.
>   - Verify: terminal prompt starts with `>>>`, not `PS`.
>
> - Step 2: run the Python exit command.
>   - System: Python REPL.
>   - Path: current REPL session.
>   - Command: `exit()`
>   - Verify: Python process closes.
>
> - Step 3: confirm PowerShell is back.
>   - System: VS Code PowerShell terminal.
>   - Path: `C:\pythonCatchup`.
>   - Verify: prompt returns to `PS C:\pythonCatchup>`.

> [example] Plain REPL checks
>
> ```python
> >>> price = 101.25
> >>> price * 1.01
> 102.2625
> >>> type(price)
> <class 'float'>
> ```

> [example] Pandas exploration
>
> ```python
> >>> import pandas as pd
> >>> df = pd.DataFrame({"price": [100, 101, 103]})
> >>> df["return"] = df["price"].pct_change()
> >>> df
> ```

> [note] A REPL session is temporary memory. Useful discoveries should be copied into a script, reusable function, test, or note before closing the session.

### 4.c VS Code Breakpoints

> [concept] **A breakpoint** is a marker on a source-code line where the debugger pauses execution. While paused, the Python process is still alive, and VS Code can inspect variables, call stack, and control flow.

> [concept] **Stepping** means moving through code while paused. Step Over runs the current line and stops at the next line in the same function. Step Into enters a called function. Step Out finishes the current function and returns to the caller.

> [concept] **`debugpy`** is the Python debugger engine used by VS Code. VS Code shows the UI, the Python extension coordinates the session, `debugpy` controls or attaches to the Python process, and the selected interpreter runs the code.

> [new filetype] `.vscode\launch.json`
>
> `launch.json` is a VS Code JSON configuration file that tells VS Code how to start a debug session. It does not store breakpoint lines. It defines the run shape: which debugger type to use, what program to run, and which terminal or console to use.
>
> > [example] Current debug configuration
> >
> > ```json
> > {
> >   "version": "0.2.0",
> >   "configurations": [
> >     {
> >       "name": "Python: Current File",
> >       "type": "debugpy",
> >       "request": "launch",
> >       "program": "${file}",
> >       "console": "integratedTerminal"
> >     }
> >   ]
> > }
> > ```
> >
> > - `"type": "debugpy"` means use the Python debugger engine.
> > - `"request": "launch"` means VS Code starts the Python process.
> > - `"program": "${file}"` means debug the currently open file.
> > - `"console": "integratedTerminal"` means run inside the VS Code terminal.

> [decision] Use VS Code breakpoints when `print()` is not enough: the bug depends on changing state, branches, loops, function calls, or the order in which code runs.

> [workflow] Debug a Python file with VS Code breakpoints
> - Step 1: confirm VS Code uses the repo interpreter.
>   - System: VS Code Python extension.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Verify: selected interpreter points to `.venv`.
>
> - Step 2: open the Python file and place a breakpoint.
>   - System: VS Code editor.
>   - Path: target `.py` file.
>   - Verify: a red dot appears in the left gutter beside the line.
>
> - Step 3: start debugging.
>   - System: VS Code debugger.
>   - Path: `.vscode\launch.json` or current Python file.
>   - Command: press `F5` or use Run And Debug.
>   - Verify: execution pauses on the breakpoint line.
>
> - Step 4: inspect runtime state.
>   - System: paused Python process.
>   - Path: VS Code Variables, Watch, Call Stack, and Debug Console panels.
>   - Verify: variable values match the exact paused line.
>
> - Step 5: continue or step through.
>   - System: VS Code debugger controls.
>   - Path: current debug session.
>   - Verify: Step Over, Step Into, Step Out, and Continue move execution as expected.

> [example] Breakpoint target
>
> ```python
> def calculate_return(today_price: float, yesterday_price: float) -> float:
>     return today_price / yesterday_price - 1
>
>
> result = calculate_return(103.0, 100.0)
> print(result)
> ```

> [note] Breakpoints inspect a live running process. If the file is not being executed, the breakpoint will not be hit.

### 4.d Pytest Debugging

> [concept] **`pytest`** has two related forms in this repo. `pytest.exe` is the command-line entry point that scans for test files, calls test functions, and reports pass/fail results. The `pytest` package is the Python module imported inside tests when helper tools are needed.

> [concept] **Pytest discovery** is naming-based. By default, pytest looks for files like `test_*.py` or `*_test.py`, then functions or methods named `test_*`.

> [concept] **`assert`** is built into Python, not pytest. Pytest runs the test function, lets Python evaluate `assert`, catches `AssertionError` when the assertion fails, then reports the failure clearly.

> [decision] Use pytest debugging when a bug should become repeatable. `print()` and breakpoints help inspect one run; pytest records expected behavior so future edits do not silently break it.

> [example] No `import pytest` needed
>
> ```python
> def test_basic_math():
>     assert 1 + 1 == 2
> ```
>
> Pytest finds this because the file and function follow test naming conventions.

> [example] `pytest.approx()` for floating-point comparison
>
> ```python
> import pytest
>
>
> def test_return_calculation():
>     result = 0.1 + 0.2
>
>     assert result == pytest.approx(0.3)
> ```
>
> Use this because floating-point math can produce tiny representation differences.

> [example] `pytest.raises()` for expected errors
>
> ```python
> import pytest
>
>
> def validate_price(price: float) -> None:
>     if price <= 0:
>         raise ValueError("price must be positive")
>
>
> def test_validate_price_rejects_negative_price():
>     with pytest.raises(ValueError):
>         validate_price(-1.0)
> ```
>
> Python `raise` creates the error path. `pytest.raises(...)` checks that the expected error is raised inside the block.

> [example] `pytest.mark.parametrize()` for repeated cases
>
> ```python
> import pytest
>
>
> def is_positive_price(price: float) -> bool:
>     return price > 0
>
>
> @pytest.mark.parametrize(
>     "price, expected",
>     [
>         (100.0, True),
>         (0.0, False),
>         (-1.0, False),
>     ],
> )
> def test_is_positive_price(price: float, expected: bool):
>     assert is_positive_price(price) is expected
> ```
>
> Use parametrization when the same rule should be checked against several inputs.

> [example] `pytest.fixture()` for reusable test setup
>
> ```python
> import pandas as pd
> import pytest
>
>
> @pytest.fixture
> def sample_prices():
>     return pd.DataFrame({"price": [100.0, 101.0, 103.0]})
>
>
> def test_sample_price_row_count(sample_prices):
>     assert len(sample_prices) == 3
> ```
>
> Fixture essence: replace repeated setup code with a named setup provider. By default, pytest calls the fixture once per test function, so each test receives fresh setup. It is mainly for cleaner tests and independent state, not a performance cache.

> [workflow] Run pytest from PowerShell
> - Step 1: open the VS Code PowerShell terminal in the repo.
>   - System: shell working directory.
>   - Path: `C:\pythonCatchup`.
>   - Verify: prompt shows `PS C:\pythonCatchup>`.
>
> - Step 2: run the pytest executable through `uv`.
>   - System: `.venv` command entry point.
>   - Path: `C:\pythonCatchup\.venv\Scripts\pytest.exe`.
>   - Command: `uv run pytest`
>   - Verify: pytest prints collected tests and pass/fail results.
>
> - Step 3: read failures from top to bottom.
>   - System: pytest report output.
>   - Path: VS Code PowerShell terminal.
>   - Verify: failure output shows test name, failing assertion or exception, and file line.
>
> - Step 4: fix the code or test expectation.
>   - System: source code and tests.
>   - Path: `C:\pythonCatchup\src\`, `C:\pythonCatchup\tests\`.
>   - Verify: rerun `uv run pytest` until the relevant test passes.

> [note] `pytest.exe` can run tests that never import `pytest`. Import `pytest` only when the test code needs helpers like `pytest.approx`, `pytest.raises`, `pytest.mark.parametrize`, or `pytest.fixture`.

> [note] Use verbose mode when you want pytest to show each collected test name and result: `uv run pytest -v`. Clear test function names act like readable messages in the test report.

> [execution] Ran pytest in the repo
> - Command: `C:\Users\xinwe\.local\bin\uv.exe run pytest`
> - Root: `C:\pythonCatchup`
> - Config: `pyproject.toml`
> - Test path: `tests`
> - Result: pytest ran successfully, collected `0` tests, and reported `no tests ran`.
> - Meaning: pytest is installed and callable, but the repo does not yet contain any discoverable `test_*.py` test files.

### 4.e Pandas Inspection

> [concept] **Pandas inspection** is data-form debugging. The critical use: check the actual shape, schema, types, missingness, ordering, and alignment of a table-like object before trusting the analysis.

> [concept] **A `DataFrame`** is a two-dimensional labeled table: rows plus columns. **A `Series`** is a one-dimensional labeled vector, often one column from a `DataFrame`.

> [decision] Use pandas inspection before and after operations that can silently change meaning: `merge`, `groupby`, `sort_values`, `shift`, `pct_change`, `rolling`, `resample`, filtering, and joins.

> [decision] For quant data, inspect instrument/date alignment. Code can run without crashing but still be analytically wrong if returns cross instruments, dates are unsorted, duplicates exist, or future data leaks into earlier rows.

> [workflow] Inspect a pandas DataFrame
> - Step 1: check object type and shape.
>   - System: Python runtime memory.
>   - Path: current `DataFrame` variable.
>   - Command: `print(type(df)); print(df.shape)`
>   - Verify: object is a pandas `DataFrame`, and row/column counts are plausible.
>
> - Step 2: check columns and sample rows.
>   - System: pandas table schema.
>   - Path: `df.columns`, `df.head()`, `df.tail()`.
>   - Command: `print(df.columns); print(df.head()); print(df.tail())`
>   - Verify: expected columns exist and sample rows look sane.
>
> - Step 3: check dtypes and missing values.
>   - System: pandas column metadata.
>   - Path: `df.dtypes`, `df.isna()`.
>   - Command: `print(df.dtypes); print(df.isna().sum())`
>   - Verify: numeric columns are numeric, date columns are date-like when needed, and missingness is understood.
>
> - Step 4: check duplicates.
>   - System: pandas row identity.
>   - Path: row keys such as `instrument` and `trade_date`.
>   - Command: `print(df.duplicated().sum())`
>   - Verify: duplicate rows are expected or explained.
>
> - Step 5: check index and time order.
>   - System: pandas index and sort order.
>   - Path: `df.index`, date columns, or instrument/date keys.
>   - Command: `print(df.index); print(df.index.is_monotonic_increasing)`
>   - Verify: index shape and sort order match the intended workflow.
>
> - Step 6: check summary ranges.
>   - System: pandas descriptive statistics.
>   - Path: numeric columns.
>   - Command: `print(df.describe())`
>   - Verify: min, max, mean, and count do not reveal impossible values.

> [example] Minimal inspection block
>
> ```python
> print("type:", type(df))
> print("shape:", df.shape)
> print("columns:", list(df.columns))
> print(df.head())
> print(df.tail())
> print(df.dtypes)
> print(df.isna().sum())
> print("duplicates:", df.duplicated().sum())
> ```

> [example] Quant-specific inspection
>
> ```python
> print(df[["instrument", "trade_date"]].head())
> print("instruments:", df["instrument"].nunique())
> print("date range:", df["trade_date"].min(), df["trade_date"].max())
> print("duplicate keys:", df.duplicated(["instrument", "trade_date"]).sum())
> print(df.sort_values(["instrument", "trade_date"]).head())
> ```

> [note] Pandas inspection is less about technical crashes and more about awareness of data form/state. A script can run successfully and still be wrong if rows, dates, instruments, or calculated columns are misaligned.

### 4.f Stack Traces

> [concept] **A stack trace** is Python's crash report. The critical use: it shows the error type, error message, failing file/line, and call path that led to the failure. A stack trace is not a random wall of text; it is the runtime path Python followed before it crashed.

> [workflow] Read a Python stack trace
> - Step 1: find the final error line.
>   - System: Python runtime error output.
>   - Path: VS Code PowerShell terminal.
>   - Verify: identify the error type and message, such as `ZeroDivisionError: division by zero`.
>
> - Step 2: find the lowest file/line frame that belongs to your code.
>   - System: Python call stack.
>   - Path: files listed in the traceback.
>   - Verify: this line usually points to the operation that failed.
>
> - Step 3: read upward to understand who called it.
>   - System: function call chain.
>   - Path: stack frames above the failing line.
>   - Verify: the path explains how execution reached the failure.
>
> - Step 4: fix the first real cause, then rerun.
>   - System: source code and runtime.
>   - Path: failing file or caller file.
>   - Verify: the same stack trace no longer appears.
>
> > [example] Stack trace shape
> >
> > ```text
> > Traceback (most recent call last):
> >   File "demo.py", line 8, in <module>
> >     main()
> >   File "demo.py", line 5, in main
> >     divide(10, 0)
> >   File "demo.py", line 2, in divide
> >     return a / b
> > ZeroDivisionError: division by zero
> > ```
> >
> > Read the final line first for the error type/message. Then read the lowest project file line to find where the failure happened.

### 4.g Logging

> [concept] **`logging`** is a built-in Python standard-library module. The critical use: keep durable runtime messages for scripts or workflows that may run repeatedly, without leaving random temporary `print()` calls everywhere.

> [concept] **Logging moving parts**: a logger receives messages, a level decides message importance, a handler sends messages somewhere such as terminal or file, and a formatter controls how the message looks.

> [workflow] Add basic logging to a script
> - Step 1: import the standard-library module.
>   - System: Python standard library.
>   - Path: current Python file.
>   - Command: `import logging`
>   - Verify: no package install is needed.
>
> - Step 2: configure logging once near the script entry point.
>   - System: Python logging module.
>   - Path: current Python process.
>   - Command: `logging.basicConfig(level=logging.INFO, format="%(levelname)s:%(message)s")`
>   - Verify: `INFO` and above messages are visible.
>
> - Step 3: replace durable progress prints with logging calls.
>   - System: runtime message stream.
>   - Path: VS Code PowerShell terminal by default.
>   - Command: `logging.info("loaded data")`
>   - Verify: terminal shows a structured log message.
>
> - Step 4: keep temporary inspection as `print()`.
>   - System: source code hygiene.
>   - Path: exploratory script or REPL.
>   - Verify: random debug prints do not remain in reusable `src/` code.

> [example] Minimal logging setup
>
> ```python
> import logging
>
> logging.basicConfig(level=logging.INFO, format="%(levelname)s:%(message)s")
>
> logging.info("starting script")
> logging.warning("missing values detected")
> logging.error("failed to load data")
> ```

> [example] Level name and message mapping
>
> ```python
> import logging
>
> logging.basicConfig(level=logging.INFO, format="%(levelname)s:%(message)s")
>
> logging.info("starting data load")
> logging.warning("missing values detected")
> logging.error("failed to load price file")
> ```
>
> Output:
>
> ```text
> INFO:starting data load
> WARNING:missing values detected
> ERROR:failed to load price file
> ```
>
> `%(levelname)s` comes from the logging call, such as `logging.warning(...)`. `%(message)s` comes from the text inside the call, such as `"missing values detected"`.

> [note] Common logging levels:
> - `DEBUG`: detailed developer information.
> - `INFO`: normal progress.
> - `WARNING`: suspicious but not fatal.
> - `ERROR`: operation failed.
> - `CRITICAL`: serious failure.

> [note] Common logging keywords:
> - `level`: minimum importance level to show.
> - `format`: text pattern for each log message.
> - `filename`: write logs to a file instead of only terminal.
> - `logger`: named logging object, useful when code grows beyond one script.
> - `handler`: output destination such as terminal or file.
> - `formatter`: controls final message layout.

### 4.h Qlib Troubleshooting

> [concept] **Qlib troubleshooting** means separating environment problems, data-provider problems, config problems, and model/backtest logic problems. The critical use: Qlib failures often look like one stack trace, but the cause may live in Python environment, local data path, dataset config, calendar/instrument setup, or pandas-shaped data.

> [decision] Debug Qlib in layers:
> - Environment layer: Python, `.venv`, installed packages, import path.
> - Data layer: provider URI, calendar, instruments, feature files, date range.
> - Config layer: YAML/Python config keys, paths, model/dataset settings.
> - Runtime layer: stack trace, logging output, pandas inspection, generated artifacts.

> [note] Practical troubleshooting order:
> - Python environment: right interpreter and package environment.
> - Qlib installation: Qlib importable inside `.venv`.
> - Qlib data environment: provider path and config point to real data.
> - Static data sanity: instruments, calendars, dates, columns, missing values, duplicates.
> - Runtime failure: stack trace and logs during execution.
> - Analytical correctness: labels, features, train/test split, leakage, and backtest assumptions.

> [workflow] Triage a Qlib issue
> - Step 1: confirm the repo Python environment.
>   - System: `.venv` Python runtime.
>   - Path: `C:\pythonCatchup\.venv\Scripts\python.exe`.
>   - Command: `uv run python -c "import sys; print(sys.executable)"`
>   - Verify: output points to `C:\pythonCatchup\.venv\Scripts\python.exe`.
>
> - Step 2: confirm Qlib can be imported.
>   - System: installed Python packages.
>   - Path: current `.venv`.
>   - Command: `uv run python -c "import qlib; print(qlib.__version__)"`
>   - Verify: command prints a Qlib version instead of `ModuleNotFoundError`.
>
> - Step 3: confirm the data provider path.
>   - System: environment variable or config value.
>   - Path: `QLIB_PROVIDER_URI` or Qlib config file.
>   - Verify: path exists on disk and contains expected Qlib data files.
>
> - Step 4: read the stack trace bottom-up.
>   - System: Python runtime error output.
>   - Path: VS Code PowerShell terminal.
>   - Verify: identify the first project/Qlib line where the failure becomes specific.
>
> - Step 5: inspect data if the code runs but results look wrong.
>   - System: pandas `DataFrame` or Qlib dataset output.
>   - Path: current data variable.
>   - Verify: shape, columns, date range, instruments, missing values, and duplicates are understood.
>
> - Step 6: add logging for long-running workflows.
>   - System: Python logging module.
>   - Path: current script or reusable workflow.
>   - Verify: output shows which stage failed: init, load data, build dataset, train model, backtest, or save results.

> [example] Fast environment checks
>
> ```powershell
> uv run python -c "import sys; print(sys.executable)"
> uv run python -c "import qlib; print(qlib.__version__)"
> ```

> [example] Fast provider path check
>
> ```powershell
> echo $env:QLIB_PROVIDER_URI
> Test-Path $env:QLIB_PROVIDER_URI
> ```

> [note] Do not start by changing many Qlib config values at once. First locate the layer that is failing, then change one thing and rerun.

## 5. Python Basic For Engineering

### 5.a Data Types And Values

> [concept] **A value** is a concrete piece of data in Python runtime memory. **A data type** is the category that defines what operations the value supports. The critical use: types tell you what a value can do, what errors to expect, and how to design function inputs/outputs.

> [concept] **Core scalar types**:
> - `int`: whole number, like `252`.
> - `float`: decimal number, like `0.035`.
> - `bool`: truth value, `True` or `False`.
> - `str`: text, like `"AAPL"`.
> - `None`: absence of a value.
>
> > [example] Basic values and types
> >
> > ```python
> > instrument = "AAPL"
> > lookback_days = 20
> > signal_score = 0.73
> > is_tradeable = True
> > last_error = None
> >
> > print(type(instrument))
> > print(type(lookback_days))
> > print(type(signal_score))
> > print(type(is_tradeable))
> > print(type(last_error))
> > ```
>
> > [note] In Python, scalar values like `1` are still objects. `1` is an `int` object, and operators call object behavior underneath. Normal code uses `1 + 2`, but the object method exists as `(1).__add__(2)`.
> >
> > ```python
> > print(type(1))
> > print(1 + 2)
> > print((1).__add__(2))
> > ```

> [concept] **Python variables** are names bound to objects. The variable is not the object itself; it is a name pointing to a value in runtime memory.
>
> > [example] Type affects valid operations
> >
> > ```python
> > price = 101.25
> > shares = 10
> > instrument = "AAPL"
> >
> > market_value = price * shares
> > label = instrument + "_close"
> > ```

> [note] For engineering code, do not rely only on memory. Use type annotations to document expected values at function boundaries.
>
> > [example] Type-annotated function boundary
> >
> > ```python
> > def calculate_return(today_price: float, yesterday_price: float) -> float:
> >     return today_price / yesterday_price - 1
> > ```

### 5.b Collections And Data Structures

> [concept] **A collection** stores multiple values under one object. The critical use: collections let code represent real grouped concepts such as instruments, feature names, config values, rows, and lookup tables. A collection is also called a container because it contains other objects.
>
> > [example] Qlib-style container use
> >
> > ```python
> > feature_names = ["close", "volume", "return_5d"]
> > model_params = {"learning_rate": 0.05, "num_leaves": 64}
> > train_period = ("2010-01-01", "2018-12-31")
> > universe = {"AAPL", "MSFT", "NVDA"}
> > ```
> >
> > `feature_names` is a `list`; `model_params` is a `dict`; `train_period` is a `tuple`; `universe` is a `set`.
>
> > [note] Container choice is about the access pattern: index by position, lookup by name, preserve fixed grouping, or test membership.

> [concept] **`list`** is an ordered, mutable sequence. Use it when order matters and items may be added, removed, or changed.
>
> > [example] List: ordered batch
> >
> > ```python
> > instruments = ["AAPL", "MSFT", "NVDA"]
> >
> > first_instrument = instruments[0]
> > last_instrument = instruments[-1]
> >
> > instruments.append("TSLA")
> > instruments.remove("MSFT")
> >
> > for instrument in instruments:
> >     print(instrument)
> > ```
> >
> > Use a `list` when the order is meaningful or when the collection will change. Access uses integer position: `0` is first, `-1` is last.
>
> > [note] Python allows mixed-type lists, like `["AAPL", 101.25, True]`, but engineering code should usually keep list items the same kind of thing. Homogeneous lists are easier to loop over, type-check, test, and reason about.
>
> > [note] Common list mistake: changing a list while looping over it can skip items or create confusing behavior. Prefer building a new list when filtering.
> >
> > ```python
> > instruments = ["AAPL", "MSFT", "NVDA"]
> > filtered = [name for name in instruments if name != "MSFT"]
> > ```

> [concept] **`tuple`** is an ordered, usually immutable sequence. Use it for fixed groups of values where the position has meaning.
>
> > [example] Tuple: fixed pair
> >
> > ```python
> > date_range = ("2020-01-01", "2020-12-31")
> >
> > start_date, end_date = date_range
> > print(start_date)
> > print(end_date)
> > ```
> >
> > Use a `tuple` when the group is fixed and position carries meaning. Here, position `0` means start date and position `1` means end date.
>
> > [example] Tuple as a stable key
> >
> > ```python
> > key = ("AAPL", "2020-01-02")
> > price_by_key = {
> >     key: 101.25,
> > }
> >
> > print(price_by_key[("AAPL", "2020-01-02")])
> > ```
> >
> > A tuple can be used as a `dict` key if its contents are immutable. A `list` cannot be used as a `dict` key.
>
> > [note] Dict keys must be hashable. Hashable means Python can compute a stable lookup identity for the key. The object used as a key must not change its hash/equality behavior while stored in the dict. A tuple of strings is stable, so `("AAPL", "2020-01-02")` can be a key. A list is mutable, so `["AAPL", "2020-01-02"]` cannot be a key and raises `TypeError: unhashable type: 'list'`.
>
> > [note] Tuple does not mean "small list." It usually means fixed structure. If you need to append/remove items, use a `list`.

> [concept] **`dict`** is a key/value mapping. Use it when values should be looked up by name, such as config, metadata, or parameters.
>
> > [example] Dict: named config
> >
> > ```python
> > config = {
> >     "provider_uri": "C:\\path\\to\\qlib_data",
> >     "benchmark": "SPY",
> >     "lookback_days": 20,
> > }
> >
> > provider_uri = config["provider_uri"]
> > lookback_days = config.get("lookback_days", 10)
> >
> > config["lookback_days"] = 30
> >
> > for key, value in config.items():
> >     print(key, value)
> > ```
> >
> > Use a `dict` when names matter more than position. `config["provider_uri"]` reads a required key; `config.get("lookback_days", 10)` reads a key with a fallback value.
>
> > [example] Dict creation styles
> >
> > ```python
> > # Dict literal: written manually in code.
> > config = {
> >     "benchmark": "SPY",
> >     "lookback_days": 20,
> > }
> >
> > # Build from two lists.
> > instruments = ["AAPL", "MSFT"]
> > prices = [101.25, 220.50]
> > price_by_instrument = dict(zip(instruments, prices))
> >
> > # Fill step by step.
> > sector_by_instrument = {}
> > sector_by_instrument["AAPL"] = "technology"
> > sector_by_instrument["JPM"] = "financials"
> > ```
> >
> > Dicts can be written as literals, built from other collections, filled step by step, or loaded from config/data files such as JSON, TOML, YAML, or CSV-derived data.
>
> > [example] Dict as lookup table
> >
> > ```python
> > sector_by_instrument = {
> >     "AAPL": "technology",
> >     "JPM": "financials",
> > }
> >
> > sector = sector_by_instrument["AAPL"]
> > ```
> >
> > Use a lookup dict when the question is "given this key, what value belongs to it?"
>
> > [note] Common dict mistake: `config["missing_key"]` raises `KeyError` if the key is absent. Use direct indexing for required keys and `.get()` only when a fallback is acceptable.

> [concept] **`set`** is an unordered collection of unique values. Use it for membership checks and duplicate removal.
>
> > [example] Set: uniqueness and membership
> >
> > ```python
> > instruments = ["AAPL", "MSFT", "AAPL"]
> > unique_instruments = set(instruments)
> >
> > has_aapl = "AAPL" in unique_instruments
> > unique_instruments.add("NVDA")
> >
> > print(unique_instruments)
> > ```
> >
> > Use a `set` when duplicate values should collapse and membership checks are the main operation. Do not use a `set` when stable order matters.
>
> > [example] Set operations
> >
> > ```python
> > qlib_universe = {"AAPL", "MSFT", "NVDA"}
> > model_universe = {"MSFT", "NVDA", "TSLA"}
> >
> > overlap = qlib_universe & model_universe
> > only_in_qlib = qlib_universe - model_universe
> > combined = qlib_universe | model_universe
> > ```
> >
> > `&` means intersection, `-` means difference, and `|` means union.
>
> > [note] Set output order is not stable. If you need sorted output, convert after the set operation: `sorted(unique_instruments)`.

> [decision] Default choices:
> - Use `list` for ordered batches.
> - Use `dict` for named config or lookup values.
> - Use `tuple` for fixed pairs/groups.
> - Use `set` for uniqueness and membership checks.

### 5.c Keywords And Operators

> [concept] **Keywords** are reserved words in Python syntax. The critical use: they define language structure, so they cannot be used as variable names.
>
> > [example] Common keywords
> >
> > ```python
> > if is_tradeable:
> >     return signal_score
> > else:
> >     return None
> > ```
> >
> > `if`, `else`, `return`, and `None` are Python keywords.

> [concept] **Operators** are symbols or words that combine, compare, or transform values. The critical use: operators express calculation, comparison, boolean logic, membership, identity, and assignment.
>
> > [example] Operator categories
> >
> > ```python
> > price * shares              # arithmetic
> > price > 0                   # comparison
> > is_tradeable and has_data   # boolean logic
> > "AAPL" in universe          # membership
> > value is None               # identity
> > signal_score = 0.73         # assignment
> > ```

> [concept] **Arithmetic operators** calculate numeric values.
>
> > [example] Arithmetic
> >
> > ```python
> > price = 101.25
> > previous_price = 100.00
> >
> > daily_return = price / previous_price - 1
> > doubled = price * 2
> > remainder = 10 % 3
> > power = 2 ** 3
> > ```
> >
> > Common arithmetic operators: `+`, `-`, `*`, `/`, `//`, `%`, `**`.

> [concept] **Comparison operators** produce `True` or `False`.
>
> > [example] Comparison
> >
> > ```python
> > price = 101.25
> >
> > is_positive = price > 0
> > is_exact = price == 101.25
> > is_not_zero = price != 0
> > ```
> >
> > Common comparison operators: `==`, `!=`, `<`, `<=`, `>`, `>=`.

> [concept] **Boolean operators** combine truth values. Use `and`, `or`, and `not` to express conditions.
>
> > [example] Boolean logic
> >
> > ```python
> > has_price = True
> > has_volume = False
> >
> > usable = has_price and has_volume
> > partial = has_price or has_volume
> > blocked = not has_price
> > ```
> >
> > `and` requires both sides true. `or` requires at least one side true. `not` flips a truth value.

> [concept] **Membership operators** test whether a value is inside a container.
>
> > [example] Membership
> >
> > ```python
> > universe = {"AAPL", "MSFT", "NVDA"}
> >
> > if "AAPL" in universe:
> >     print("tradable")
> >
> > if "TSLA" not in universe:
> >     print("not in universe")
> > ```
> >
> > Use `in` and `not in` with `list`, `tuple`, `dict`, `set`, strings, and other containers.

> [concept] **Identity operators** test whether two names point to the same object. The critical use: use `is None` and `is not None` for missing sentinel checks.
>
> > [example] Identity
> >
> > ```python
> > last_error = None
> >
> > if last_error is None:
> >     print("no error")
> >
> > if last_error is not None:
> >     print(last_error)
> > ```
> >
> > Use `==` for value equality. Use `is` mainly for `None`, `True`, and `False` identity checks.
>
> > [note] C++ mental mapping: `==` is value equality; `is` is closer to asking whether two Python names refer to the same object identity. It is not a data-type check. Use `isinstance(x, int)` for type/category checks.
> >
> > ```python
> > a = []
> > b = []
> > c = a
> >
> > print(a == b)  # True: same value/content
> > print(a is b)  # False: different list objects
> > print(a is c)  # True: same list object
> > ```

> [concept] **Assignment operators** bind or update values.
>
> > [example] Assignment
> >
> > ```python
> > count = 0
> > count += 1
> >
> > total_return = 0.05
> > total_return *= 100
> > ```
> >
> > `=` binds a name. `+=`, `-=`, `*=`, and `/=` update from the current value.

> [note] Common mistake: `=` assigns a value, while `==` compares values.
>
> > [example] Assignment vs comparison
> >
> > ```python
> > score = 1.0       # assign
> > score == 1.0      # compare
> > ```

### 5.d Control Flow

### 5.e Frequent Built-In Functions

### 5.f Functions

### 5.g Imports, Modules, And Packages

### 5.h Errors And Exceptions

### 5.i File I/O And Paths

### 5.j Classes And OOP

### 5.k Frequent Standard Library Tools

### 5.l Pandas Frequent Functions And Use

### 5.m Software Engineering Basics

### 5.n Mini Exercises

## 6. NumPy And Pandas For Financial Data

### 6.a Goal

### 6.b Key Concepts

### 6.c Examples

### 6.d Common Mistakes

### 6.e Mini Exercise

## 7. Quant Research Concepts

### 7.a Instruments

### 7.b Features

### 7.c Labels

### 7.d Factors

### 7.e Alpha

### 7.f Universe

### 7.g Benchmark

### 7.h Rebalance

### 7.i Transaction Costs

### 7.j Drawdown

### 7.k Information Coefficient

## 8. ML Workflow Basics

### 8.a Features And Labels

### 8.b Train Validation Test

### 8.c Leakage

### 8.d Model Fitting

### 8.e Prediction Scores

### 8.f Metrics

## 9. Qlib Mental Model

### 9.a Data Provider

### 9.b Calendar

### 9.c Instruments

### 9.d Dataset Config

### 9.e Model

### 9.f Recorder

### 9.g Strategy

### 9.h Backtest

### 9.i Experiment Tracking

## 10. Qlib First-Run Lab

### 10.a Install Qlib

### 10.b Initialize Data

### 10.c Run An Existing Example

### 10.d Inspect Outputs

### 10.e Understand What Happened

## 11. Mini Exercises

### 11.a Calculate Returns

### 11.b Create A Rolling Factor

### 11.c Create A Future-Return Label

### 11.d Train A Simple Model

### 11.e Rank Assets By Score

### 11.f Identify Leakage

## 12. Python Software Engineering Patterns

### 12.a Project Architecture

### 12.b Dependency Boundaries

### 12.c Config Design

### 12.d Type-Driven Design

### 12.e Error Design

### 12.f Logging And Observability

### 12.g Testing Strategy

### 12.h CLI Design

### 12.i Data Pipeline Design

### 12.j Wrapper Design For Qlib

### 12.k Notebooks Vs Scripts Vs Package Code

### 12.l Refactoring Patterns

### 12.m Packaging And Distribution

### 12.n Performance And Scaling Basics

## 13. Common Mistakes

## 14. Glossary

## 15. Next Steps
