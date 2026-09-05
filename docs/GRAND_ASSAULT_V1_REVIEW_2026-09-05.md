# CUDA-CIC Grand Assault V1 Review — 2026-09-05

RESULT ZIP SHA-256: `cf11cbd6e9972bc0387bbe529dd08023e4352ef5a30587935b92c36da506ac50`

## What held

- Frozen V6.2.1 baseline re-established: 142/142, benchmark PASS.
- Frozen Arena commit exact.
- Arena corpus inventory: 63 tests = 23 dev, 5 validation, 12 blind, 5 challenge, 18 perf.
- Common IR inventory parsed 12/12 committed raw external NDJSON cases.
- Replicated CUDA scaling completed: 142 objects ~164.353 ms / ~864 obj/s; 18,176 objects ~153.336 ms / ~118,537 obj/s. This is replicated-corpus scaling, not proof-corpus diversity and not a Lean-vs-CUDA speedup claim.
- 1M supported-lane IR candidate gate: median ~0.799 ms / ~1.252B candidates/s. This is IR-level only, not raw Lean end-to-end verification.

## Root cause of blocked external stages

Frozen Arena `lka.py` was invoked with Python 3.11, but that revision uses Python >=3.12 f-string syntax. Exact error:

`SyntaxError: f-string expression part cannot include a backslash`

This blocked official Arena build through `lka.py`, generated/light tests, fuzz/metamorphic official-oracle execution, and Init/Std/Cedar/CSLib probes. It is an orchestration/runtime-version failure, not a CUDA-CIC semantic mismatch.

Mathlib was separately not attempted because free disk was ~18.3 GiB while the safety guard required 80 GiB.

## V1.1 hotfix

V1.1 is orchestration-only:

1. Torch/CUDA checker remains on Python 3.11.
2. Arena `lka.py` uses a separately discovered Python 3.14/3.13/3.12.
3. Committed raw NDJSON tests bypass `lka.py` entirely.
4. Official checker gets direct `lake build` fallback.
5. Work root automatically selects the local drive with most free space, with `GA_WORK_ROOT` override.
6. Fuzz/metamorphic official-oracle calls use concurrent workers (`GA_ORACLE_WORKERS=8` default).

No CUDA-CIC semantic rule is intentionally changed.

## Claim boundary

Grand Assault V1 does not establish full Arena CUDA-CIC support, Mathlib CUDA-CIC support, general Lean semantic equivalence, or universal GPU speedup.
