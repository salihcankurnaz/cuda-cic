# CUDA-CIC V4.7.1 — Term DefEq / Multi-Def Delta-Beta Milestone

## Frozen result

Result archive:

`CUDA_CIC_V4_7_1_TERM_DEFEQ_DELTA_BETA_RESULT_20260905_042329.zip`

SHA-256:

`7502d6d076bab58b0a8ad564c9b15a83007ced7e4623febc116b362810bc53b3`

Result status:

`V4_7_1_TERM_DEFEQ_DELTA_BETA_CORE_PASS`

## Frozen external provenance

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

`tutorial/Tutorial.lean` blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

The result reports both provenance checks as true.

Exact raw external objects:

- `029_defEqLambda` — `7a28d11e2a035c2d0d97c75d5cb0bb12e16be1c5502b9975aa08775e1928ba92`
- `030_peano1` — `fe92f67341850f0c222c43cd99e9f17904cdb003654f394890f49df431ceaf7d`
- `031_peano2` — `63c8aec3c8457d2f4e76476b1d503647fb58d998b0dc2176cacc5efd814586e0`
- `032_peano3` — `e731f91828d3bb6186205233ba8ba94dd54bdf21e7b9a06e020f789be70ad55d`

## Exact differential gate

All four external objects were accepted by the official Arena checker, Python checker, and CUDA checker:

- official Lean vs expected: `4/4`
- Python vs official Lean: `4/4`
- CUDA vs official Lean: `4/4`
- Python vs CUDA: `4/4`
- CUDA status: `PASS`

Official checker replay counts:

- `029_defEqLambda`: `Accepted 1 declarations.`
- `030_peano1`: `Accepted 7 declarations.`
- `031_peano2`: `Accepted 8 declarations.`
- `032_peano3`: `Accepted 10 declarations.`

The CUDA checker reports `cuda_fail_decl = -1` for every accepted external case.

## Supplemental mutation gate

Two deterministic compiled-object mutations were also checked:

1. `peano2`: substitute `PN.lit0` where the proof path previously used `PN.lit1`.
2. `peano3`: substitute `PN.lit1` where the proof path previously used `PN.lit2`.

Results:

- Python mutation rejection: `2/2`
- CUDA mutation rejection: `2/2`

Failure loci:

- `peano2` mutation: CUDA failed declaration index `7` (the target theorem)
- `peano3` mutation: CUDA failed declaration index `9` (the target theorem)

Python likewise reaches the target theorem after accepting all preceding definitions, then rejects with `value_type_mismatch`.

## Supported finite fragment demonstrated here

This milestone extends the prior external same-object line to a deeper declaration environment while staying inside the measured term vocabulary:

- `Sort`
- `BVar`
- `ForallE`
- `Lam`
- `App`
- `Const`
- declaration-ordered constant lookup
- definition-only delta unfolding
- beta reduction via closure environments
- higher-order definitional equality under binders
- theorem target proposition checking
- one alpha-normalized symbolic universe parameter
- direct pass-through universe instantiation in the selected Peano dependencies

Measured environment sizes reach:

- 10 declarations
- maximum expression id 58
- higher-order application and repeated multi-definition delta/beta normalization

## Environment

- Python 3.11.9
- Windows 10.0.26200
- torch 2.6.0+cu124
- CUDA 12.4
- NVIDIA GeForce RTX 4070 Laptop GPU

## Claim boundary

This milestone supports the narrow statement that, on these four frozen raw Lean Kernel Arena objects, the CUDA checker agrees with the official Lean checker and the independent Python checker, while also rejecting two targeted Peano mutations.

It does **not** establish:

- full Lean-kernel semantic equivalence;
- full CIC correctness;
- full Arena support;
- general universe equivalence;
- arbitrary universe substitution;
- historical priority or a world-first claim;
- any Lean-vs-GPU speedup claim.

The result explicitly records:

- `general_universe_equivalence = false`
- `full_arena_support = false`
- `general_lean_semantic_equivalence = false`
- `historical_priority_established = false`

## Next measured boundary

The result selects:

`CUDA_CIC_V4_8_LET_FRAGMENT_ATLAS`

The next stage should measure the exact raw Arena representation and semantics of `letType`, `letTypeDep`, and `letRed` before implementing any `LetE` support.
