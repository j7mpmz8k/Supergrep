# Supergrep

A fast, search-engine style CLI search tool for Bash with multi-term Boolean matching, exclusions, and clean grouped syntax highlighting.

---

## Installation

Add to your `~/.bashrc`:

```bash
source /path/to/Supergrep/supergrep.bash
```

*Requires: `bash`, GNU `grep` (with `-P` support), and `perl`.*

---

## Usage

```bash
supergrep [OPTIONS] <lines> <word1> [-exclude_word2] [+ word3] ...
```

### Options

| Option | Description |
| :--- | :--- |
| `-a`, `--all` | Search all files, including hidden dotfiles and default ignored folders. |
| `-c`, `--case-sensitive` | Case-sensitive search (case-insensitive by default). |
| `-w`, `--word` | Match whole words only. |
| `-l`, `--list` | Print only matching file paths. |
| `-e`, `--ext <exts>` | Filter by extension, comma-separated (e.g. `-e py,js`). |
| `-d`, `--dir <path>` | Directory to search (defaults to `.`). |

*By default, common build folders (`node_modules`, `venv`, `target`, `build`, `dist`, `__pycache__`) and hidden files are skipped.*

---

## Query Syntax & Examples

- **AND (multiple words on the same line):**
  ```bash
  supergrep 0 error database
  ```
- **Context lines (`<lines>`):**
  ```bash
  supergrep 3 function handleClick   # 3 lines of context before and after
  ```
- **NOT (prefix term with `-`):**
  ```bash
  supergrep 0 error -database        # 'error' but NOT 'database'
  ```
- **OR (use `+` or `OR`):**
  ```bash
  supergrep 0 cherry + fig           # 'cherry' OR 'fig'
  supergrep 2 error -db + warn alert # ('error' without 'db') OR ('warn' AND 'alert')
  ```
- **Whole-word match & target directory:**
  ```bash
  supergrep -w -d /var/log 0 failed
  ```
- **Extension filter & list filenames only:**
  ```bash
  supergrep -e py,sh 0 def main      # Search only .py and .sh files
  supergrep -l 0 TODO                # List filenames containing 'TODO'
  ```
