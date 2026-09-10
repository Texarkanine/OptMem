# Current Task: windows-split-scope

**Complexity:** Level 1

## Build

- [x] Path-local fallback: `"path" + cwd` left a `:` in the directory name on Windows (`pathC:\…`). `path_slug` uses `splitdrive` then `join` of relative parts (`C:\foo` → `path\c\foo`).
- [x] Windows-path `origin`: split only on `[:/]` then `join` dropped the optmem prefix. `repo_slug` also splits on `\\`.
- [x] POSIX `test.py`: ntpath proves both encodings without a Windows runner; existing owner/repo expectation was `OptMem` (typo) now `OptMem-Split`.
- Files: `memo`, `test.py`
