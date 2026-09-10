---
task_id: windows-split-scope
complexity_level: 1
date: 2026-09-09
status: completed
---

# TASK ARCHIVE: windows-split-scope

## SUMMARY

OptMem-Split project scoping on native Windows now nests path-local and Windows-path-origin stores under the data dir. `"path" + cwd` left a colon (`pathC:\…`); `join` of a backslash origin discarded the optmem prefix. Draft PR: https://github.com/Texarkanine/OptMem-Split/pull/1 (`split-windows-support` → `main.split`).

## REQUIREMENTS

- Path-local fallback: `splitdrive` then `join` of relative parts (`normcase`); `C:\` and `S:\` nest under `optmem/path/` with no colon.
- Windows-path `origin` must not `join` an absolute component that leaves `optmem`.
- Unix `owner/repo` and POSIX path-local behavior unchanged.
- POSIX `test.py` covers Windows strings via `ntpath`; no Windows GitHub runner.

Constraints: scoping only (not flock/`msvcrt`); no installer/shebang/`python3` packaging.

## IMPLEMENTATION

`path_slug` and `repo_slug` in `memo`; `scope_dir` delegates. Test seam is `path=ntpath` on those helpers. Niko memory-bank bootstrap (`AGENTS.md`, `CLAUDE.md`, `memory-bank/`) shipped on the same branch.

## TESTING

Catching tests: `C:\`, `C:/`, `S:\` via `ntpath`; Windows-path origin must stay under `optmem`. `python3 test.py`: 109118 passed, 0 failed (build and QA re-run). `/niko-qa` (Kimi): PASS. Advisories (keep): UNC branch in `path_slug` avoids merging distinct shares; owner-less `C:\widget.git` becomes `repo/c/widget` but still under optmem.

No Level 1 reflection file existed; this archive inlines brief, progress, and QA instead.

## LESSONS LEARNED

- `os.sep` is only `/` vs `\`. `C:` is not a separator. `os.path.relpath` raises across drives (`S:` vs `C:`).
- On POSIX, a backslash origin can still "start with optmem/repo" while keeping `\\` in the slug; `ntpath.join` is the proof of prefix-discard.
- Do not `join("path", abs_windows_path)`: later absolute wins and the store lands in the project.

## PROCESS IMPROVEMENTS

Level 1 has no `/niko-archive` mapping; this run used the Level 2 archive format because the operator invoked `/niko-archive` anyway.

## TECHNICAL IMPROVEMENTS

Installer, shebang, and `python3` vs `python` remain POSIX. `pretty()` home-fold is still case-sensitive. Tests (`chmod 0`, `PATH=/usr/bin`, `"Not a directory"`) still cannot prove native Windows.

## NEXT STEPS

- Review/merge https://github.com/Texarkanine/OptMem-Split/pull/1
- Optional later: Windows invocation (`python memo` vs shebang) if agents cannot exec extensionless `memo`
