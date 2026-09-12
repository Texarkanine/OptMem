# Current Task: nap-drop-dates

**Complexity:** Level 1

## Fix

- **What broke:** `nap_prompt` quoted raw memories as `#<id> <date> <text>`. Agents copied the date into the summary; later naps then stacked it.
- **Why:** The date is log metadata. It already appears on wake/zoom/recall. Putting it next to the text in the compressor's source made it look like content.
- **What changed:** Raw branch of `nap_prompt` now prints `#<id> <text>`. `#N` stays as the list marker. Halves were already `#lo-hi <summary>`. No PR #5 prompt text.
- **Files:** `memo` (`nap_prompt`), `test.py` (catching checks + wake still dated).
