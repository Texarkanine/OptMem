# Project Brief

## User Story

As an agent using OptMem, I want nap source lines to omit the log date so I do not copy that date into summaries (and then into later summaries).

## Use-Case(s)

### Use-Case 1

An agent is asked to compress memories `#24-31`. Each quoted line is `#24 <text>`, not `#24 2026-09-12 <text>`. The header and `Run:` line still name the range.

### Use-Case 2

Wake, zoom, and recall still show `#N YYYY-MM-DD <text>` so the date remains readable metadata, not something the compressor is asked to rewrite.

## Requirements

1. Raw nap source lines are `#<id> <text>` (keep the number, drop the date).
2. Half-block nap lines stay `#<lo>-<hi> <summary>` (they never had a date of their own).
3. Wake, zoom, and recall stay `#<id> <date> <text>`.
4. Do not take [upstream OptMem PR #5](https://github.com/VictorTaelin/OptMem/pull/5) prompt text (`Never include a date or timestamp…`) in README, `init` template, or the nap instruction sentence.

## Constraints

1. SumMem-style: fix the quoted body, not the agent instructions.
2. Keep `#N` on nap source lines as visual anchors.
3. One-file tool: change `nap_prompt` in `memo`; tests in `test.py`.

## Acceptance Criteria

1. A nap of raw memories does not put `YYYY-MM-DD` between `#<id>` and the text.
2. After that nap is settled, wake still prints the log date on those memories.
3. `python3 test.py` passes.
