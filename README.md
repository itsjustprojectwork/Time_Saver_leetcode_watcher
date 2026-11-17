# lc-watcher

Fetch a LeetCode problem straight into a Jupyter notebook — problem statement, examples, and constraints as cell 0. No browser copy-paste.

Built for people who grind LeetCode inside VS Code + Jupyter instead of the web editor.

## Requirements

- Python 3.10+
- Jupyter extension in VS Code (or any Jupyter setup)
- `code` command on PATH for auto-open (optional — see below)

## Install

```bash
pip install git+https://github.com/YOURNAME/lc_watcher.git
```

## Usage

```bash
new_problem 303
```

First run asks where to save notebooks (default `~/leetcode_problems`) and remembers it. After that:

```bash
new_problem 42
```

You get:

1. The problem preview in your terminal (statement, examples, constraints).
2. A `Save to notebook? [y/N]` prompt.
3. On `y` → `leetcode(42).ipynb` is created with the problem as cell 0, and opened in VS Code if `code` is on PATH.

Nothing is written unless you confirm. No background process runs between invocations.

## First run

```
$ new_problem 303
[first run] Where should LeetCode notebooks live? [~/leetcode_problems]:
[info] created ~/leetcode_problems
[info] saved config to ~/.config/lc_watcher/config.json
...
Save to notebook? [y/N]: y
[done] ~/leetcode_problems/leetcode(303).ipynb
[done] opened in VS Code
```

The folder is created if it doesn't exist. Existing folders are used as-is.

## Change the save folder

```bash
new_problem --set-folder
```

Or set it permanently in one shot while fetching a problem:

```bash
new_problem 42 --dir ~/code/leetcode
```

## Already solved it?

```bash
$ new_problem 42
leetcode(42).ipynb already exists. Open it? [y/N]:
```

No re-fetch, no overwrite.

## Optional: auto-open in VS Code

`new_problem` runs `code <notebook>` after a successful save. If `code` isn't on PATH, it silently skips. To enable it, open VS Code → Command Palette → **Shell Command: Install 'code' command in PATH**.

## Config

Stored at:

- macOS/Linux: `~/.config/lc_watcher/config.json`
- Windows: `%APPDATA%\lc_watcher\config.json`

```json
{
  "watch_dir": "/Users/you/leetcode_problems"
}
```

Editable by hand if you prefer.

## Troubleshooting

**`[error] could not fetch problem`** — LeetCode's API occasionally blocks automated requests. The tool falls back to scraping automatically. If both fail, wait a bit and retry; this is a LeetCode-side issue, not an lc-watcher bug.

**`new_problem: command not found` after install** — your Python `Scripts`/`bin` directory isn't on PATH. Reinstall in a virtualenv, or add the directory `pip show -f lc-watcher` reports to your PATH.

**`ModuleNotFoundError: No module named 'lc_watcher'`** — you're probably running a stale `watcher.py`. Uninstall the old one and reinstall: `pip uninstall lc-watcher && pip install ...`

## License

MIT — see [LICENSE](LICENSE).