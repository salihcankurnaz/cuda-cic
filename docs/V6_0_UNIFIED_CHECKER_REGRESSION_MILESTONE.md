# CUDA-CIC V6.0 — Unified Checker Regression Milestone

## Frozen result

Result archive:

`CUDA_CIC_V6_0_UNIFIED_CHECKER_RESULT_20260905_082220.zip`

SHA-256:

`54a2ce0330b6c7ede648b5d7b51e268521de9fe4a435669a00131df41098eae1`

Status:

`V6_0_UNIFIED_REGRESSION_PASS_129_SUPPORTED_13_UNSUPPORTED`

Manifest verification: 152/152 listed payloads match exact byte lengths and SHA-256 values with no missing or unlisted payload files.

## Frozen provenance

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Tutorial blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

Both provenance checks are true.

## Full corpus regression

- frozen raw SHA replay: 142/142
- official Lean expected replay: 142/142
- raw corpus recaptured: 142/142

## Unified CUDA-CIC surface

Exact AST semantic engines:

- Python: 35/35
- CUDA: 35/35

Bounded semantic descriptor engines:

- Python: 94/94
- CUDA: 94/94

Supported Python/CUDA agreement:

- 129/129

Supported total:

- 129/142 = 90.8451%

Explicit unsupported total:

- 13/142

Unsupported IDs:

`45, 55, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72`

Unexplained false accepts:

- 0

## Important interpretation

V6.0 is the first single user-facing CUDA-CIC regression surface spanning the previously frozen exact AST semantic cores and bounded descriptor engines.

It is not yet one monolithic CUDA kernel. The 129 supported objects are routed through previously validated semantic engines under one dispatcher. The remaining 13 objects are explicitly reported as `UNSUPPORTED`; the checker does not guess their verdicts.

## Claim boundary

V6.0 does not establish:

- full Lean-kernel semantic equivalence;
- full Lean Kernel Arena support beyond this exact frozen Tutorial corpus;
- one monolithic CUDA kernel;
- general semantics for bounded descriptor families;
- any Lean-vs-CUDA speedup.

## Next stage

V6.1 should target the 13 explicit unsupported objects through real semantic-core support rather than descriptor-only shortcuts, while beginning internal IR/kernel consolidation. Same-object performance benchmarking should wait until the semantic consolidation boundary is stable.
