# Project Brief

## User Story

As an operator on native Windows, I want OptMem-Split's project scoping to resolve to a store under the data directory so that install-and-run behaves like Unix: one project memory, not a crash or a store inside the project.

## Use-Case(s)

### Use-Case 1

A directory with no git remote (or no git) records into a path-local store under `$XDG_DATA_HOME/optmem/path/…`, including when cwd is `C:\Users\…` or another drive such as `S:\`.

### Use-Case 2

A checkout whose `origin` is a Windows filesystem path (`C:\…` or `C:/…`) records into `optmem/repo/…`, not a drive-absolute location that discarded the optmem prefix.

## Requirements

1. Path-local fallback encodes an absolute Windows path as relative parts under `optmem/path/` using `os.path` (`splitdrive`, `join` of relative components, `normcase`).
2. Git origin URLs that are Windows paths do not `join` an absolute component that throws away `optmem`.
3. Unix behavior for POSIX paths and `owner/repo` remotes stays the same.
4. Existing POSIX `test.py` keeps proving the Unix cases; add host-independent coverage of the Windows strings. No Windows GitHub runner unless that is the only way to prove the fix.

## Constraints

1. Fix OptMem-Split's additions (scoping). Do not rework upstream flock/`msvcrt` locking.
2. Tests may stay POSIX/Ubuntu.
3. Do not add a Windows GitHub Actions runner unless there is no other way to prove the fix.
4. Do not expand into installer/shebang/`python3` packaging unless scoping cannot work without it.

## Acceptance Criteria

1. `C:\Users\…` and `S:\Users\…` path-local slugs nest under the data dir with no colon in a directory name.
2. A backslash `origin` path does not resolve to a store outside `optmem`.
3. `python3 test.py` on POSIX still passes, including new Windows-string cases that do not need a Windows runner.
