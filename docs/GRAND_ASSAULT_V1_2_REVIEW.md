# CUDA-CIC Grand Assault V1.2 Review

Date: 2026-09-06

## Frozen result

- RESULT ZIP SHA-256: `57516a0342d4443a40667e83986dfad5fbabe29cc0b753d99d1f3afa7ea4f392`
- RESULT top-level manifest: 16/16 exact, no missing/extra/hash/byte mismatches.
- Highest cumulative medal: `BRONZE`.

## Preserved baseline

- Frozen V6.2.1 regression: PASS.
- `supported_python_cuda = 142/142`.
- frozen Tutorial coverage = 142/142 (100%).
- same-object benchmark status = PASS.

## Arena/global corpus

- Exact Arena revision: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`.
- Global test inventory: 63 tests.
- Split: dev 23, validation 5, blind 12, challenge 5, perf 18.
- Source kinds: generated 48, module 3, direct NDJSON 12.
- Blind oracle commitment: `af243225c2b55ef7a90db54f997ba9cb28102fa0a701247ae437cf5cfd85734e`.
- Direct committed NDJSON official agreement: 12/12.

## Adversarial evidence

- Official-oracle mutations: 50,000/50,000 completed.
- Official verdicts: 5,207 accept; 44,793 reject.
- Oracle workers: 8.
- Metamorphic representation variants: 3,000/3,000 stable; 0 mismatch; 0 errors.

These are official-oracle corpus-generation/representation-invariance results. They are not claims that CUDA-CIC checked all 50k mutations.

## Performance evidence

Replicated frozen-142 batch scaling remains PASS. At 18,176 repeated objects the V1.2 run reports approximately 122k objects/s. This is replicated-corpus scaling, not 18,176 distinct Lean proofs.

IR-level supported-lane candidate simulation:

- candidates: 1,000,000
- median: about 0.601 ms
- throughput: about 1.663 billion candidates/s

This is an IR-level gate simulation, not raw Lean proof end-to-end verification.

## Remaining orchestration blocker discovered in V1.2

UTF-8 and Python-runtime issues were fixed. The remaining generated Arena/library failures are Windows harness incompatibilities rather than semantic failures:

1. Frozen `lka.py` expects a suffixless `.../bin/lean4export`, while Windows builds `lean4export.exe`.
2. Frozen test names are derived via `str(Path(...))`, so nested names use backslashes on Windows, while the Grand Assault canonical inventory used forward slashes. This caused `No tests found matching pattern` for nested `corner-cases/...` and `perf/...` entries.
3. The `tutorial` runmultiple entry is redundant with the already-frozen exact 142-object Stage01 baseline and should not be counted as an external-light case.

Init/Std/CSLib also reached the same `lean4export.exe` path blocker. Cedar has an additional Windows/toolchain-layout issue. Mathlib was not attempted because the free-disk safety threshold was not met; no semantic conclusion is drawn from that.

## Claim boundary

V1.2 does not establish full Arena CUDA-CIC support, Mathlib CUDA-CIC support, general Lean semantic equivalence, or a universal speedup claim.

## Next step

V1.3 patches only the checked-out Arena host harness after exact commit verification:

- resolve `lean4export.exe` on Windows;
- invoke nested `build-test` names using OS-native separators;
- remove Tutorial from the external-light stage because Stage01 already covers the exact frozen Tutorial 142 corpus.

No CUDA-CIC semantic rule is changed by this hotfix.
