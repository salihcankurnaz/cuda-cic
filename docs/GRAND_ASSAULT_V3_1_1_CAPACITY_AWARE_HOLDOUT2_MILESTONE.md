# CUDA-CIC Grand Assault V3.1.1 — Capacity-Aware Fresh Holdout II

Date: 2026-09-07

## Frozen result

Result ZIP SHA-256:

`a211e7753e8b772e254e7c48558d9508a8d6b43a9942e670e5348a39a6e0affd`

Status:

`V3_1_1_CAPACITY_AWARE_HOLDOUT2_PASS`

## Integrity and seals

- RESULT manifest: 97/97 payloads exact; 0 missing, 0 extra, 0 hash/byte mismatch.
- Fresh Holdout II input manifest: 10,000 cases; no test name / YAML / expected / mutation mode / Official verdict fields.
- Fresh decision SHA-256: `66689c87e7108b17bcde47b7ecc963e587c0b15eee0d345e05596582343fd665`.
- Fresh input-manifest SHA-256: `2db0ab9886442c7459f96cde38811be007cf79f98ce46b3ea30e1e04b1ab441c`.
- Decision seal independently matches both hashes.
- Checker SHA-256: `c2255ac897af278aaa70fa0aebd4691f8d5883e724e42baecc3c3cdf4f4f8b05`.
- Holdout II contains 10,000 unique mutation SHA-256 values.
- Overlap with all unique V3 holdout mutation SHA values: 0.

## Development/regression surface

External DEV56:

- decided: 9/56 (16.07%)
- ACCEPT: 2
- REJECT: 7
- UNSUPPORTED: 47
- REVIEW_REQUIRED: 0
- matched: 9/9
- false accepts: 0
- false rejects: 0
- all 9 V2 decided cases preserved
- V3 `perf/grind-ring-5` over-rejection fixed; it now fails closed as UNSUPPORTED
- dependency-slicer RecursionError count: 0

## Fresh Holdout II

10,000 new oracle-hidden mutations:

- decided: 1,275/10,000 (12.75%)
- ACCEPT: 0
- REJECT: 1,275
- UNSUPPORTED: 8,725
- REVIEW_REQUIRED: 0
- matched decided objects: 1,275/1,275
- false accepts: 0
- false rejects: 0
- Official ACCEPT: 15
- Official REJECT: 9,985

All 15 Official-ACCEPT holdout mutations remained fail-closed UNSUPPORTED; none were falsely rejected.

## Capacity-aware generation

Actual Holdout II mode distribution:

- drop_last: 24
- duplicate_last: 27
- bump_expr_index: 6,862
- bump_level_index: 177
- bump_name_index: 2,448
- inductive_num_params: 159
- recursor_num_minors: 151
- constructor_num_params: 152

No fallback index-offset family was required: the original eight primitive families supplied all 10,000 unique fresh objects.

## Interpretation

This is a clean fresh mutation-generalization PASS for the current fail-closed external semantic frontier. It materially strengthens reject-side evidence: 1,275 new oracle-hidden objects were independently rejected and all 1,275 matched the Official kernel.

However, fresh ACCEPT generalization remains unestablished: the Holdout II checker emitted zero ACCEPT decisions. The next research priority is therefore not another mutation campaign. It is real-library declaration holdout work over Init/Std (and later CSLib when practical), with conservative declaration-target slicing that can produce ACCEPT-capable exact-AST routes.

## Claim boundary

Do not claim:

- full Arena support;
- Init/Std/CSLib CUDA-CIC verification;
- Mathlib support;
- general Lean-kernel semantic equivalence;
- that mutation holdout equals an independent external repository corpus;
- universal speedup.

Defensible current claim: CUDA-CIC has a sealed, fail-closed external semantic frontier with 9/9 correct decided external Arena objects and a second fresh 10,000-case mutation holdout with 1,275/1,275 correct decided objects, zero false accepts and zero false rejects.