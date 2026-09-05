# CUDA-CIC V6.1.1 Full Coverage Milestone

Date: 2026-09-05

Frozen RESULT ZIP SHA-256:

`0e09ed73eed5f5fb956a5c0343c9d0bfa87c7a879c7c4965841fb8477183fabd`

Status:

`V6_1_1_FULL_FROZEN_TUTORIAL_COVERAGE_PASS_142_142`

## Exact frozen evidence

- Arena commit: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`
- Tutorial blob: `782a81685f76f4917b9189d49a7e8f5679a376dc`
- raw SHA replay: 142/142
- official Lean expected replay: 142/142
- exact AST Python: 35/35
- exact AST CUDA: 35/35
- bounded descriptor Python: 94/94
- bounded descriptor CUDA: 94/94
- normalized-AST closure Python: 13/13
- normalized-AST closure CUDA: 13/13
- closure mutations: Python 8/8 reject, CUDA 8/8 reject
- unified supported Python/CUDA agreement: 142/142
- unsupported: 0
- zero unexplained false accepts: true
- unified classifications: 93 supported accepts, 49 supported rejects
- frozen Tutorial coverage: 142/142 = 100.00%

## Architecture at this milestone

This is one user-facing regression/checker surface but not one monolithic CUDA kernel.

Semantic routing remains split among:

- 35 exact AST objects routed through six frozen exact CUDA cores;
- 94 bounded semantic objects routed through one consolidated descriptor CUDA extension;
- 13 normalized-AST closure objects routed through the V6.1 closure core.

The descriptor CUDA extension count was reduced from four to one. Total CUDA extension count was reduced from ten to eight.

## Claim boundaries

This milestone does **not** establish:

- general Lean-kernel semantic equivalence;
- full Lean Kernel Arena support beyond this exact frozen Tutorial corpus;
- one monolithic CUDA kernel;
- a valid Lean-vs-CUDA speedup claim;
- general semantics for every bounded descriptor family.

The defensible claim is complete semantic routing and differential agreement on this exact frozen 142-object Tutorial corpus with zero unsupported objects and zero unexplained false accepts.

## Reporting cleanup noted

The RESULT archive still contains `V6_1_RESULT.json` as the result filename despite the V6.1.1 status string, and `UNIFIED_COVERAGE_LEDGER.json` retains stale `next_if_pass` text mentioning the former 13 unsupported objects. These are reporting artifacts only; the unified matrix and final result show 142 supported objects and zero unsupported.

## Next stage

Do not add more coverage micro-versions. Move to:

1. deeper common-IR / exact-kernel consolidation;
2. a frozen same-object benchmark protocol that clearly separates preprocessing, transfer, kernel-only, and end-to-end measurements;
3. performance claims only after correctness gates remain 142/142 under the consolidated path.
