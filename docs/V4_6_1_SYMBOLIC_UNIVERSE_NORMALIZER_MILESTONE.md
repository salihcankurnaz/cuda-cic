# CUDA-CIC V4.6.1 — Symbolic Universe Normalizer Milestone

## Frozen result

Result ZIP SHA-256:

`eff5f1ca3e58fd0c68380a0091571e48934cd870517ced2fa30755376d5cfb40`

Frozen Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Frozen `tutorial/Tutorial.lean` Git blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

## External corpus

| Arena object | Raw NDJSON SHA-256 | Official Lean | Python | CUDA |
|---|---|---:|---:|---:|
| `020_levelComp4` | `39dced2925dcce7f66539f47f408d276b48d57638b4bfefc47860eed2f710a58` | accept | accept | accept |
| `021_levelComp5` | `31910166228cf46f68dbaa876d1c155734475b0f3f7a15c2a82f5535e8c150f8` | accept | accept | accept |
| `022_imax1` | `8fe3d41b913c8717847bc4a544e6b947bb5a1b616d80dbe19859d465ff225d57` | accept | accept | accept |
| `023_imax2` | `9d7fdab95e9ac1f87e19055e3133b98173f90d94c641870dc49cff6db2d1061f` | accept | accept | accept |
| `024_levelMaxComm` | `8a2ed8095cf9f69fcebb1e8b695944599cd524b42334cd6ff3051a5deebe7134` | accept | accept | accept |
| `025_levelMaxAssoc` | `2e97e820cfffa0f890ea70f7c3ea7f7e1636568196f3fc738868249644f9f229` | accept | accept | accept |
| `026_levelMaxIdem` | `1ee0d884c19ef76feb4ba77f5448507da2f8d983a688f4e8711d61784f50e571` | accept | accept | accept |
| `027_levelMaxAbsorb` | `87fab97e0b524a64e21ebe2adbadb407b381d1bee45cd2060e4a24055d554b11` | accept | accept | accept |

Aggregate:

- official Lean vs expected: **8/8**
- Python vs official Lean: **8/8**
- CUDA vs official Lean: **8/8**
- Python vs CUDA: **8/8**
- CUDA runtime: **PASS**

## Supplemental negative mutations

Two deterministic compiled-level mutations were rejected by both implementations:

1. `levelMaxComm_MUT_comm_drop_v`
2. `levelMaxAssoc_MUT_assoc_drop_w`

Aggregate mutation rejection:

- Python: **2/2**
- CUDA: **2/2**

## Supported level boundary

The raw external level fragment exercised here contains:

- zero
- symbolic parameters
- successor
- symbolic `max`

The independent Python and CUDA normalizers use a canonical max-of-atoms representation sufficient for the tested external identities:

- commutativity
- associativity
- idempotence
- absorption
- successor offsets over symbolic max terms

Source-level `imax` examples `levelComp4/5` and `imax1/2` were already simplified by the frozen exporter before NDJSON emission. Therefore this milestone **does not establish general symbolic `imax` equivalence**.

## Explicit non-claims

This milestone does not establish:

- general Lean universe equivalence;
- arbitrary symbolic `imax` normalization;
- full Lean Kernel Arena support;
- general Lean-kernel semantic equivalence;
- historical priority.

Status:

`V4_6_1_SYMBOLIC_UNIVERSE_NORMALIZER_PASS`
