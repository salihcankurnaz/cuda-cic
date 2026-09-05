# CUDA-CIC V4.9 — Inductive Frontier Atlas Milestone

## Frozen result

Result archive:

`CUDA_CIC_V4_9_INDUCTIVE_FRONTIER_ATLAS_RESULT_20260905_053431.zip`

SHA-256:

`cd631f688d3e39108b973b4c0c0f0f309f0364688086d399b77b19d283d55ca9`

Status:

`V4_9_INDUCTIVE_FRONTIER_ATLAS_COMPLETE`

Manifest verification: 21/21 listed payloads have exact byte lengths and SHA-256 values, with no missing or extra payload files.

## Frozen external provenance

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

`tutorial/Tutorial.lean` blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

Both provenance checks are true in the result.

## Exact external objects

- `036_empty` — ACCEPT — `030852937308e66cb90de3b8de7cd336f3d825e81c87c5be5cc1fe33c6d54356`
- `037_boolType` — ACCEPT — `02053d077abf5a63594d1025f9ef2f90dfff65f331503aa3b7486bbbb997b3e8`
- `038_twoBool` — ACCEPT — `91a1f7379e22ebbec710ce6b43b7e0750be258ace8fc22d0b889fb76b57010de`
- `046_inductBadNonSort` — REJECT — `372f6a167433b45749fa38f14ad3a2e8ca4e0dae8762812c0b9f288e9f68499f`
- `047_inductBadNonSort2` — REJECT — `95836e7bee5fbd00d1d16d88cea2defa8dfb2387fc0e400d200b59715716a0d9`
- `048_inductLevelParam` — REJECT — `732e2fc946ab308a819366bc5395865a69235098e1a401ec1a059d05d89ef06e`

Official Lean vs expected agreement: 6/6.

## Exact raw inductive schema

The relevant lean4export wrapper is:

`{"inductive": {"types": [...], "ctors": [...], "recs": [...]}}`

Observed inductive-type record fields include:

- `name`
- `levelParams`
- `type`
- `numParams`
- `numIndices`
- `all`
- `ctors`
- `numNested`
- `isRec`
- `isUnsafe`
- `isReflexive`

Observed constructor record fields include:

- `name`
- `levelParams`
- `type`
- `numParams`
- `induct`
- `cidx`
- `numFields`
- `isUnsafe`

Observed recursor records include their own type, level parameters, motive/minor/index counts and rule records.

## First measured semantic split

The three initial good objects use manifest inductive type roots whose type expression is a direct `Sort`.

The two non-sort negative objects use an inductive type root whose type expression is a `Const`, and the official kernel rejects them.

The duplicate-universe negative object contains duplicate level parameters in the inductive type record (`[u,u]`) and is rejected by the official kernel.

The good objects also contain constructor and recursor metadata, so this atlas does not justify a general inductive checker claim merely from the manifest type-root observations.

## Claim boundary

V4.9 is an atlas only. It establishes the exact external schema and six official verdicts. It does not establish inductive checking, constructor correctness, recursor correctness, positivity, recursive/indexed inductive support, or full Lean-kernel semantic equivalence.

## Next execution model

The next package will use a fail-closed, multi-stage pipeline rather than serial one-stage versions. It may continue automatically through schema validation, a deliberately narrow manifest-simple inductive lane, Python/CUDA differential checks, mutations, broader inductive frontier discovery and next-stage classification, but it must stop or classify unsupported structures instead of silently accepting them.
