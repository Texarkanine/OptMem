# Progress

Stop nap source lines from putting the log date next to memory text, so agents do not copy it into summaries.

**Complexity:** Level 1

## 2026-09-12 - COMPLEXITY-ANALYSIS - COMPLETE

* Work completed
    - Restated intent: drop dates from nap quotes, keep `#N`, leave wake/zoom/recall and upstream PR #5 prompt text alone.
    - Classified Level 1: one component (`nap_prompt` raw format string).
* Decisions made
    - Keep `#N` as list anchors; the date was the token that stacked.
    - Do not take upstream PR #5's "never include a date" wording.
* Insights
    - Half-block lines are already `#lo-hi <summary>`; contamination there is leftover text from an earlier dated raw nap.

## 2026-09-12 - BUILD - COMPLETE

* Work completed
    - Catching tests in `test.py` for `#id text` nap quotes and dated wake lines.
    - One format-string change in `nap_prompt` raw branch.
    - Full suite: 109123 passed, 0 failed.
* Decisions made
    - Halves unchanged; they never interpolated a date.
* Insights
    - The fake compressor still collects `  #` lines; keeping `#N` avoided rewriting that loop.
