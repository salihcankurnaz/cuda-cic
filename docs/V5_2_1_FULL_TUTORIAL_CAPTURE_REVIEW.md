# CUDA-CIC V5.2.1 — Full Tutorial Capture Review

## Result archive

`CUDA_CIC_V5_2_1_ULTRA_FULL_TUTORIAL_RESULT_20260905_072037.zip`

SHA-256:

`f012ed92ec4b441374d130c58532f959ef928fda4b558710a878398b727baa8b`

Manifest verification: 88/88 listed payloads exact, no missing or extra payloads.

## Clean semantic / replay gates

- Arena exact commit: true
- Tutorial blob match: true
- frozen raw SHA replay: 74/74
- corrected frozen official replay: 74/74
- Python bounded semantic lanes: 28/28
- CUDA bounded semantic lanes: 28/28
- Python/CUDA agreement: 28/28
- Python mutation rejection: 10/10
- CUDA mutation rejection: 10/10
- CUDA runtime: PASS

## Why the final status is REVIEW_REQUIRED

The full-Tutorial capture loop used the raw Python regex:

`r"^(\\d{3})_(.+)\\.ndjson$"`

which matches literal backslashes rather than digit/dot regex tokens. Therefore every generated file such as `001_basicDef.ndjson` was skipped and the result reported `tutorial_export_count=0`.

This is a capture/orchestration bug only. It does not affect the 74/74 frozen replay, 28/28 Python/CUDA lane results, or 10/10 mutation results.

## Independent evidence from the same run

`tutorial_build.log` contains exactly 142 `Writing ... .ndjson` records, with numeric test IDs 001 through 142 consecutive and no gaps. Therefore the exact frozen Arena revision does generate the expected complete 142-object Tutorial corpus.

## Next action

V5.2.2 removes regex-based ID recognition entirely and parses the three-digit test prefix from `Path.stem` using `isdigit()`. The semantic-lane logic remains unchanged. The next strongest gate is complete official replay and raw capture of all 142 Tutorial objects in one RESULT ZIP.

## Claim boundary

No full CUDA semantic equivalence is claimed for all 142 Tutorial objects. The 142-object run is a provenance/official regression corpus; CUDA semantic claims remain limited to explicitly implemented and differentially validated lanes.
