# AGENTS.md

## Repo Purpose

This repo is a Python and Qlib catch-up workspace. The main learning artifact is `pythonNotes.md`.

## Key Rules

- Only modify the specific requested section, session, file, or task.
- Do not make unrelated edits, cleanup, refactors, formatting passes, dependency changes, or structural changes unless explicitly asked.
- Keep the study notes in one Markdown file: `pythonNotes.md`.
- Do not split notes into multiple files unless explicitly requested.
- Preserve the user's wording and rough notes unless the request is specifically to rewrite them.
- For pasted images in Markdown, keep only live/relevant images that are still referenced by the current note. Remove stale, unused, or duplicate pasted images when editing the affected section.

## Backup Rule

- Before Codex edits `pythonNotes.md`, create a backup using a numeric Unix timestamp as the filename postfix, with no slashes or punctuation.
- Backup format: `pythonNotes.<unix_timestamp>.bak.md`.
- Delete the previous `pythonNotes.md` backup after creating the new one.
- Keep only the latest `pythonNotes.md` backup.
- This backup rule applies only to `pythonNotes.md`, not to `AGENTS.md`, `README.md`, or other Markdown files.

## Memory Log Rule

- Use `codexMemeory.md` as the repo memory log for durable session notes, decisions, mistakes, commands, and verification results.
- Add or update memory log entries only when the current task creates useful context for future sessions.
- Keep memory log entries short, concrete, and organized by date or task.
- Do not log private secrets, credentials, API keys, access tokens, or machine-specific paths that should not be reused.
- When Codex runs live commands that create useful future context, record the command, observed result, and next verification step in `codexMemeory.md`.
- The `pythonNotes.md` backup rule does not apply to `codexMemeory.md`.

## Editing Rules

- Keep Python examples small and runnable.
- Put reusable code in `src/catchup/`.
- Put runnable demos in `scripts/`.
- Put tests in `tests/`.
- Keep large Qlib datasets and market data out of Git.

## Code Style

- Use Python 3.10+.
- Prefer clear Python over clever abstractions.
- Use `ruff` for linting and formatting once dependencies are added.
- Avoid hardcoded local machine paths.
- Add tests for reusable functions in `src/catchup/`.

## Documentation Style

- Write notes for an engineer catching up quickly.
- Keep note-taking minimalist: short bullets, concrete commands, runnable examples, mistakes, decisions, and open questions. Avoid filler explanations.
- Use quoted note blocks for structure:
  - `> [concept]` for definitions or mental models.
  - `> [workflow]` for complete step-by-step instructions that can be executed end to end.
  - `> [decision]` for chosen conventions, tools, defaults, and tradeoffs.
  - `> [execution]` for exact commands run, checks performed, output observed, and next verification steps.
  - `> [note]` for contextual reminders, caveats, gotchas, or short non-executable observations.
  - `> [new filetype]` for file format purpose, syntax, and where that file type is used in the repo.
  - `> [example]` for compact code, config, command, or data examples that illustrate a concept without becoming a full workflow.
  - `> [convention]` for naming, style, layout, or team-agreed coding/documentation conventions.
  - `> [function]` for function purpose, input/output behavior, and minimal call example.
- Use nested quotes inside a workflow for syntax details or short explanations.
- Use nested `> > [example]` blocks when an example belongs inside another tag such as `> [new filetype]`.
- Annotate examples with short inline comments when the syntax may be unfamiliar, especially config formats like TOML.
- When adding code examples for a new or non-obvious concept, include concise comments inside the code to explain the key lines. Keep comments useful, not noisy; prioritize OOP, imports, exceptions, decorators, config files, and data transformations.
- Keep `[new filetype]` examples focused on file contents or syntax. Put commands that act on the file in `[workflow]` or `[execution]`, not inside the filetype example.
- Treat tags as independent building blocks. Tags may be nested recursively when useful, but nesting is optional and should clarify rather than create rigid hierarchy.
- Add a `> [concept]` definition where an important term first appears. Later sections may refer back to it instead of redefining it.
- Make concept notes load-bearing: explain what the thing is, where it lives, what owns or calls it, what state it changes, what it is not, and how to verify it in this repo when applicable.
- For every important concept, include the critical use and why in one direct line: what problem it solves, why we care, and when to use it.
- When explaining a tool with multiple forms, separate them explicitly: executable, module/package, config file, editor extension, runtime, syntax, or UI surface.
- Treat a live session as the current Codex-user interaction where commands are actually run against the local repo or machine.
- Every time Codex executes a live command for a documented workflow during the live session, add or update a nearby `> [execution]` summary in `pythonNotes.md`.
- Prefer concrete examples over long explanations.
- Include common mistakes where useful.
- Keep Obsidian-compatible Markdown.

## Workflow Rule

- Every `> [workflow]` block must be complete enough to execute end to end.
- Include verification steps and expected results.
- Annotate each step with the impacted system and relevant path when applicable.
- Number workflow steps as `Step 1`, `Step 2`, `Step 3`, etc.
- Prefer this compact shape:
  - `Step N`: action to take.
    - `System`: impacted tool, shell, filesystem, Python runtime, editor, repo, or package manager.
    - `Path`: relevant file, directory, executable, environment variable, or command path.
    - `Verify`: command, visible result, or state check.
- In Markdown workflow quotes, write the fields as indented nested bullets:
  - `> - Step 1: action.`
  - `>   - System: ...`
  - `>   - Path: ...`
  - `>   - Verify: ...`
- Add a blank quoted line `>` between workflow steps for readability.
