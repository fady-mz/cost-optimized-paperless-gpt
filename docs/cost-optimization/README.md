# Metadata grouping benchmark evidence

These immutable records describe the September 13, 2026 experiment at upstream commit `72ddde765709544823a0f5452575a070fdaac3b4`. They do not describe a new live evaluation of current main. The publishing branch was adapted to `7e736115b567ae2a95afbe6022e553a6ec2ab33a`, preserving its system-tag filtering and correspondent candidate limit.

The first fixed baseline/candidate pair used one synthetic invoice, real `generateSingleDocumentSuggestion` code and fake external model/Paperless boundaries. Title was generated first; the other four standard fields were eligible for grouping. The complete returned suggestions matched. Baseline and candidate used the same frozen pair harness.

| Metric | Baseline | Candidate |
| --- | ---: | ---: |
| Application calls | 5 | 2 |
| Prompt UTF-8 bytes | 4,986 | 2,347 |
| Actual paid provider calls | 0 | 0 |

Calls decreased 60%; prompt bytes decreased `1 - 2347/4986 = 52.928%`. Bytes are not tokens. Canned responses establish wiring and parsing only. Live acceptance, provider tokens/charges, retry frequency and live latency are unknown. The local timings are one fake-provider sample per arm and should not be used as a speed claim.

The 23 historical boundary records include excluded configurations, malformed/null/incomplete fields, unavailable values, invalid dates, provider failures and fallback. Failed grouping plus successful fallback uses six application calls; failure during fallback returns an error without partial suggestions. Provider-wrapper retries were outside the recorded boundary.

## Files

- `baseline.json`, `candidate.json`: raw prompts, canned responses, output suggestions and errors.
- `comparison.json`: calculated request/byte reductions, adverse fallback and explicit unknowns.
- `boundaries.json`, `boundary-lock.json`: historical boundary results and frozen expectations.
- `pair-lock.json`, `candidate-lock.json`: source/harness hashes for the original measured pair.
- `acceptance.json`: original experiment scope and acceptance contract.
- `finops_pair_test.go.txt`: original pair harness, retained as evidence rather than compiled into this release's regression suite.

The original baseline source is available at the pinned upstream commit. The candidate source and original boundary test are preserved under `measured-source/` and can be checked against the locks. `app` prefixes in old lock records refer to the original experiment layout; the files have been copied here without changing their content. Historical Go and module files carry a `.txt` suffix so they are not compiled into this release. The baseline application file is under `baseline-source/`; candidate files are under `measured-source/`.

## Financial scenario

The README's 10–20% whole-document saving is modeled as a **50% metadata cost share multiplied by a hypothetical 20–40% reduction in metadata spend**, at unchanged acceptance and before added engineering burden. Neither percentage is a measured financial input. This scenario can overstate savings when OCR dominates, cache credits already reduce input charges, or grouping produces more rejections/retries. No financial savings range has been empirically established.
