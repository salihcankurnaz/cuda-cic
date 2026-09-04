# CUDA-CIC V4.2.1 — External Mini-Corpus Generic AST Milestone

Date: 2026-09-04

## Frozen result

- RESULT ZIP SHA-256: `7ad40e689a09e2b94c598ead6839489d99ef8951178290f174c1cd876cdb5876`
- Status: `V4_2_1_EXTERNAL_MINI_CORPUS_GENERIC_AST_PASS`
- Manifest integrity: 23/23 listed payloads recomputed exactly by byte length and SHA-256.

## Frozen external corpus

Lean Kernel Arena revision:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

`tutorial/Tutorial.lean` Git blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

The seven exact generated lean4export 3.1.0 objects were:

1. `good/001_basicDef.ndjson`
2. `bad/002_badDef.ndjson`
3. `good/003_arrowType.ndjson`
4. `good/004_dependentType.ndjson`
5. `good/005_constType.ndjson`
6. `bad/012_nonPropThm.ndjson`
7. `good/028_inferVar.ndjson`

## Differential result

- Arena official Lean kernel vs Arena labels: **7/7 agreement**
- Python generic AST checker vs official Lean kernel: **7/7 agreement**
- CUDA generic AST checker vs official Lean kernel: **7/7 agreement**
- Python vs CUDA: **7/7 agreement**
- Symbolic universe levels in selected corpus: **none**

The CUDA implementation used the same flattened generic AST lane for all seven objects with support for ground `Sort`, `BVar`, `ForallE`, `Lam`, definition checking, and the theorem-target-is-Prop rule.

V4.2.1 also repaired the V4.2 CUDA runtime failure by reducing the per-thread recursive context and setting an explicit device stack limit. The scientific corpus and verdict rules were unchanged by that hotfix.

## Claim boundary

This milestone supports only the finite seven-object external corpus and the declared mini-fragment above.

It does **not** establish:

- full Lean-kernel semantic equivalence;
- full CIC correctness;
- full Lean Kernel Arena support;
- `Const`, `App`, beta/delta reduction, recursors, inductives, typeclasses, quotient, proof irrelevance, projections, or symbolic universe parameter support;
- any historical-priority or world-first claim;
- any Lean-vs-GPU speedup claim.

## Next scientific gate

`CUDA_CIC_V4_3_BETA_CONST_APP_FRAGMENT`

Add `Const` and `App` plus exact beta/delta reduction on a predeclared external mini-corpus before measuring throughput.
