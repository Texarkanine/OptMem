# Progress

Make OptMem-Split project scoping work on native Windows: path-local stores nest under the data dir, Windows-path origins do not discard the optmem prefix. Tests stay POSIX.

**Complexity:** Level 1

## 2026-09-09 - COMPLEXITY-ANALYSIS - COMPLETE

* Work completed
    - Restated intent; operator approved
    - Determined Level 1 (bug in `scope_dir` only)
* Decisions made
    - `splitdrive` then `join` of relative parts, not regex and not `os.sep` glued onto an absolute path
    - No Windows GitHub runner unless the fix cannot be proven on POSIX
    - Installer/shebang packaging out of scope
* Insights
    - `os.path.relpath` raises across drives; Austin's machine uses `C:`, `S:`, `V:`
