# CUDA-CIC Grand Assault V1.3 — Platinum Milestone

Date: 2026-09-06

## Frozen result

- RESULT ZIP SHA-256: `9ed18c2f8657664b34e997a73849f0dedf67b67ffc459dac6de77b7f9af9681d`
- RESULT manifest: 16/16 listed payloads byte/hash exact; no missing/extra payloads.
- Master medal: **PLATINUM**.

## Frozen Tutorial regression

- V6.2.1 baseline status: `V6_2_1_EXACT_CONSOLIDATION_SAME_OBJECT_BENCHMARK_PASS`
- Supported Python/CUDA: 142/142
- Coverage: 142/142 (100.00%)
- Same-object benchmark: PASS

This remains a finite frozen Tutorial result, not a claim of general Lean-kernel equivalence.

## External Arena corpus

Frozen Lean Kernel Arena revision:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Corpus inventory:

- total tests: 63
- dev: 23
- validation: 5
- blind: 12
- challenge: 5
- perf: 18
- blind oracle commitment: `af243225c2b55ef7a90db54f997ba9cb28102fa0a701247ae437cf5cfd85734e`

External light/corner/perf gate (Tutorial excluded because Stage01 replays exact frozen Tutorial 142):

- cases: 56
- built with NDJSON: 56/56
- Official expected agreement: 56/56
- build failures: 0
- oracle mismatches: 0

Expected outcome composition across the 56 cases:

- accept: 19
- reject: 24
- either: 13

Observed Official verdicts:

- accept: 26
- reject: 30

No CUDA-CIC external semantic verdict is claimed for these 56 objects yet.

## Common IR frontier

- objects summarized: 56
- parse_ok: 56/56
- largest observed feature family: recursor metadata (51 objects)
- constructor metadata: 49
- inductive environments: 51
- symbolic max: 21
- symbolic imax: 5
- projections: 24
- let/zeta: 10
- nat literals: 19
- very-large raw environments: 1

The Common IR layer is an inventory/migration surface; semantic checker migration is not yet complete.

## Adversarial / metamorphic campaign

Official-oracle adversarial mutations:

- requested: 50,000
- completed: 50,000
- bases: 55
- Official accept: 6,039
- Official reject: 43,961
- timeout: 0
- workers: 8

Representation-preserving metamorphic variants:

- requested: 3,000
- stable: 3,000
- mismatches: 0
- errors: 0

These stages build an official-oracle adversarial corpus; they are not CUDA-CIC 50k correctness claims.

## Library-scale exports and Official validation

PASS:

### Init-Prelude
- NDJSON bytes: 3,714,854
- rows: 63,723
- Official: ACCEPT / expected match

### Init
- NDJSON bytes: 324,561,407
- rows: 6,058,389
- declarations: 13,906 defs; 38,269 thms; 319 opaque; 7 axioms
- inductive types: 588
- constructors: 792
- recursors: 590
- Official: ACCEPT / expected match

### Std
- NDJSON bytes: 551,674,936
- rows: 10,023,185
- declarations: 23,607 defs; 65,792 thms; 460 opaque; 7 axioms
- inductive types: 908
- constructors: 1,359
- recursors: 912
- Official: ACCEPT / expected match

### CSLib
- NDJSON bytes: 2,145,661,820
- rows: 37,534,733
- declarations: 119,122 defs; 244,500 thms; 2,970 opaque; 7 axioms
- inductive types: 4,367
- constructors: 6,696
- recursors: 4,488
- Official: ACCEPT / expected match

Aggregate across the four PASS library exports:

- bytes: 3,025,613,017
- rows: 53,680,030
- declarations: 158,114 defs; 348,717 thms; 3,759 opaque; 23 axioms
- inductive types: 5,989
- constructors: 9,001
- recursors: 6,118

Cedar remains REVIEW_REQUIRED because its repository/toolchain layout is not Windows-compatible in the frozen Arena harness (`cedar-lean/lean-toolchain` is interpreted as an invalid toolchain name). This is an orchestration/host-platform blocker, not a semantic rejection.

Mathlib was not attempted because only ~1.86 GiB free space remained while the safety guard requires 80 GiB. No negative Mathlib semantic conclusion is supported.

## CUDA replicated-corpus scaling

Frozen 142-object corpus repeated for scaling only:

| Objects | Median ms | Throughput objects/s |
|---:|---:|---:|
| 142 | 158.4863 | 895.98 |
| 284 | 162.7004 | 1,745.54 |
| 568 | 162.1430 | 3,503.08 |
| 1,136 | 163.5911 | 6,944.14 |
| 2,272 | 166.0809 | 13,680.08 |
| 4,544 | 164.2672 | 27,662.25 |
| 9,088 | 162.6671 | 55,868.72 |
| 18,176 | 161.1222 | 112,808.79 |

This demonstrates replicated batch scaling on already-supported semantics; it is not 18,176 diverse Lean proofs and not a general Lean throughput claim.

## IR-level candidate simulation

- candidates: 1,000,000
- median: 11.3846499 ms
- throughput: 87,837,571.53 candidates/s

This is a supported-lane IR-level gate simulation, not raw Lean proof end-to-end verification.

## Claim boundary / next research frontier

Still **not** established:

- general CUDA-CIC external semantic agreement
- full Arena CUDA-CIC support
- Init/Std/CSLib CUDA-CIC verification
- Mathlib CUDA-CIC verification
- general Lean kernel semantic equivalence
- universal or fair Lean-vs-CUDA speedup

The next scientifically useful stage is external semantic generalization against the already frozen 56-object Arena corpus and its 12-object blind split, using generic AST/schema rules with no test-name special casing. Cedar and Mathlib are infrastructure/disk side quests and should not block that semantic stage.