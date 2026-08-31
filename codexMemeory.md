# Codex Memory

## 2026-08-30

> [decision] Repo memory log
>
> - `codexMemeory.md` is the durable memory log for Codex session notes, decisions, mistakes, commands, and verification results.
> - `pythonNotes.md` remains the main learning artifact.
> - The `pythonNotes.md` backup rule does not apply to `codexMemeory.md`.

> [decision] Windows and macOS repo arrangement
>
> - GitHub should store source code, notes, dependency files, lock files, tests, and portable editor settings.
> - GitHub should not store virtual environments, local secrets, downloaded datasets, caches, or machine-specific VS Code interpreter paths.
> - Each OS creates its own local `.venv` from the committed dependency recipe.
> - Shared commands should prefer `uv run ...` so Windows PowerShell and macOS `zsh` can use the same repo workflow.

> [execution] Platform prep checks
>
> - Command: `uv --version`
> - Result: failed because `uv` is not currently on PATH on this Mac.
> - Command: `python3 --version`
> - Result: `Python 3.14.3`
> - Command: `which python3`
> - Result: `/opt/homebrew/bin/python3`
> - Command: `which brew`
> - Result: `/opt/homebrew/bin/brew`
> - Next step: install `uv`, then use `uv` to install Python 3.11 for this repo.

> [execution] Git ignore update
>
> - File: `.gitignore`
> - Change: added explicit local virtual environment ignores for `.venv/`, `venv/`, and `env/`.
> - Check: `git ls-files | rg '(^|/)(\.venv|venv|env)(/|$)'`
> - Result: no tracked virtual environment folders found.

> [execution] Mac setup completed
>
> - Installed `uv 0.12.7` with Homebrew at `/opt/homebrew/bin/uv`.
> - Installed `CPython 3.11.16` with `uv`.
> - Created repo `.venv` with `uv venv --python 3.11 --prompt pythonCatchup`.
> - Synced dependencies with `uv sync --dev`.
> - Installed key packages: `pandas==3.0.5`, `pytest==9.1.1`, `ruff==0.16.4`, `numpy==2.4.6`.
> - Verified repo Python: `/Users/coder/Public/EngineGit/pythonCatchup/.venv/bin/python3`, version `Python 3.11.16`.
> - Verified pandas import: `3.0.5`.
> - Verified Ruff: `uv run ruff check .` passed; `uv run ruff format --check .` reported `7 files already formatted`.
> - Verified pytest tool runs, but current repo has `0` collected tests.
> - Removed Windows-only interpreter paths from `.vscode/settings.json` so committed VS Code settings are platform-neutral.

> [decision] Current environment state
>
> - Chapter 2 macOS setup is complete on this machine.
> - Use `uv run ...` from repo root for normal commands.
> - Do not activate `.venv` manually unless testing shell activation behavior.
> - `.venv` is local-only and should not be committed to GitHub.
> - Remaining setup gap: add real tests under `tests/` when reusable code is added, because pytest currently collects `0` tests.

> [decision] Chapter 3 platform split
>
> - Split Windows/macOS guidance where commands or paths differ: VS Code CLI extension checks, interpreter selection, Ruff/VS Code settings, and temporary environment variables.
> - Kept shared guidance where behavior is platform-independent: extension purpose, linting concept, PEP 8, code organization, and Section 3 closeout.
> - Committed VS Code settings should stay platform-neutral; interpreter paths are selected locally in each VS Code install.

> [decision] Chapter 3 detailed workflows
>
> - Expanded Chapter 3 so Windows and macOS workflows are separated where useful.
> - Windows-specific workflows use PowerShell, `Ctrl + Shift + P`, `.venv\Scripts\`, and Windows path examples.
> - macOS-specific workflows use `zsh`, `Cmd + Shift + P`, `.venv/bin/`, `which code`, and POSIX path examples.
> - Platform-independent sections stay shared, especially PEP 8 naming/style rules.

> [decision] Chapter 3.a macOS detail level
>
> - Expanded macOS VS Code extension setup so it is followable from the UI or from `zsh`.
> - macOS UI workflow now starts from opening the repo folder, opening Extensions with `Cmd + Shift + X`, installing exact extension IDs, and reloading VS Code if needed.
> - macOS terminal workflow now starts from opening the integrated `zsh` terminal, checking `pwd`, installing the `code` command in PATH if missing, installing extensions, and verifying Python/Ruff visibility.

> [execution] Chapter 3.a macOS VS Code extensions completed
>
> - `code` was initially missing from PATH.
> - VS Code app was found at `/Applications/Visual Studio Code.app`.
> - Created `/opt/homebrew/bin/code` symlink to the VS Code bundled CLI.
> - Verified `code --version`: VS Code `1.135.0`, commit `08d4889f9ec4a1685d257b9b95de036c8e1ce1e5`, arch `arm64`.
> - Verified installed extensions: `ms-python.python@2026.4.0`, `charliermarsh.ruff@2026.74.0`, and `ms-python.vscode-pylance@2026.3.1`.
> - Jupyter remains uninstalled because it is optional until notebook work is needed.

> [concept] VS Code extensions vs `.venv` packages
>
> - VS Code extensions are installed into VS Code's user extension area, not into repo `.venv`.
> - Python packages and command-line tools such as `pandas`, `pytest`, `ruff`, and `numpy` are installed into `/Users/coder/Public/EngineGit/pythonCatchup/.venv/`.
> - `charliermarsh.ruff` is the VS Code Ruff extension; `ruff` inside `.venv` is the project command-line tool.
> - Verify `.venv` tools with `uv run ruff --version`, `uv run pytest --version`, and `uv run python -c "import pandas as pd; print(pd.__version__)"`.
