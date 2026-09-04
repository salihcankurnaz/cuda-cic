# CUDA-CIC V3.2 minimal exact differential milestone

Date: 2026-09-04

## Status

`V3_2_MINIMAL_CORE_EXACT_DIFFERENTIAL_PASS`

This milestone is intentionally narrow. It does **not** establish full Lean-kernel equivalence, full CIC correctness, external negative validation, historical priority, or any Lean-vs-GPU speedup claim.

## Frozen result

Result ZIP SHA-256:

`c9cc6f252bcc975f062b2eab2e6b090160922611344b628c5720f2a0d8ff5a61`

Result manifest: 8/8 payload files matched their recorded byte counts and SHA-256 hashes.

Environment:

- Python 3.11.9
- PyTorch 2.6.0+cu124
- CUDA available
- NVIDIA GeForce RTX 4070 Laptop GPU
- Lean 4.33.1

## Exact tested fragment

The V3.2 lane used only a deliberately small proposition/function fragment built from:

- `Sort 0 / Prop`
- `FORALL / Pi / implication`
- lambda abstraction
- de Bruijn bound variables
- application in the tested non-proof-dependent function positions

The five positive proof terms were accepted by Lean and exported from the same theorem environment.

## Differential result

Positive cases:

1. `v32_imp_id`
2. `v32_imp_const`
3. `v32_imp_apply`
4. `v32_imp_comp`
5. `v32_imp_flip`

All 5/5 were accepted by both the independent Python reference checker and the CUDA checker.

Five deterministic single-BVAR mutations of those same canonical objects were then tested as negative cases. All 5/5 were rejected by both implementations.

Across all 10 cases:

- Python matched the expected verdicts: yes
- CUDA matched the expected verdicts: yes
- Python/CUDA verdict agreement: 10/10
- Python/CUDA root-type outputs: 10/10 exact agreement
- Lean/Python/CUDA three-way agreement on the 5 positive proof objects: 5/5

## Claim boundary

The negative cases in V3.2 are repository-generated deterministic mutations, not independently maintained Lean-kernel negative cases. Therefore this milestone supports only a same-object exact differential result for this tiny tested fragment.

The next stage should introduce externally defined good/bad cases, preferably beginning with a frozen subset of the Lean Kernel Arena tutorial, before expanding toward Eq, universe handling, recursors, typeclasses, or broader Lean library proofs.
