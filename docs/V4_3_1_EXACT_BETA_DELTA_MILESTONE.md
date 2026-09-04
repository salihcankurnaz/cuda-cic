# CUDA-CIC V4.3.1 — Exact beta/delta reducer milestone

Date: 2026-09-04

Frozen RESULT ZIP SHA-256:

`05aac1e70f6b1c059be5cf8644a1033516728cb210f7d31f60167ab42295d5d5`

Status:

`V4_3_1_EXACT_BETA_DELTA_REDUCER_PASS`

## External corpus

Nine exact Lean Kernel Arena NDJSON objects from frozen commit `abc55357aee17c59dfdbf39c8a2e19739e23dd10` were checked:

- 001_basicDef — accept
- 002_badDef — reject
- 003_arrowType — accept
- 004_dependentType — accept
- 005_constType — accept
- 006_betaReduction — accept
- 007_betaReduction2 — accept
- 012_nonPropThm — reject
- 028_inferVar — accept

Frozen `tutorial/Tutorial.lean` blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

## Differential result

- Arena official Lean kernel vs expected labels: 9/9
- Python checker vs official Lean kernel: 9/9
- CUDA checker vs official Lean kernel: 9/9
- Python vs CUDA: 9/9
- beta/delta-specific deterministic negative mutations rejected by Python: 2/2
- beta/delta-specific deterministic negative mutations rejected by CUDA: 2/2

The new tested external semantics include:

- constant lookup to earlier definitions in the same exported environment;
- application type inference;
- delta unfolding;
- beta reduction using closure environments;
- de Bruijn-variable handling across the reduction path.

The two beta/delta Arena objects have raw SHA-256 values:

- 006_betaReduction: `3320f6f67cd55b2bae9112ea9b0d002f231e88ec4fb3c3f3c8fd4e750b13ce78`
- 007_betaReduction2: `fb85e6eb84319dce9fed8acacb08cab2c5a54b67960112bc9de3eac22fc5a909`

## Claim boundary

This is a finite differential result for a deliberately small Lean/CIC fragment. It does not establish full Lean-kernel equivalence, full CIC correctness, full Lean Kernel Arena support, historical priority, or a Lean-vs-GPU speedup claim.

Next scientific step: measure the next unsupported Arena fragment before extending semantics further.
