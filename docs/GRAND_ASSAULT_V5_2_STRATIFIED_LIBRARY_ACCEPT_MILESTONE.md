# CUDA-CIC Grand Assault V5.2 — Stratified Library ACCEPT Milestone

## Frozen result

Result ZIP SHA-256:

`200fdefeccae7029c3f9e44fc812612ab7e67670e08d8b37ea5b3238ba3078b5`

Final status:

`V5_2_STRATIFIED_LIBRARY_ACCEPT_PASS`

The RESULT manifest is exact (81/81 listed payloads, no missing/extra/hash/byte mismatches). The sealed narrow decision SHA-256 and oracle-free input SHA-256 recompute exactly from the RESULT.

## Track A — fresh narrow exact-fragment library holdout

A fresh declaration population was selected after excluding all targets previously selected by V4, V5 and V5.1:

- Init-Prelude: 40 requested targets
- Init: 20,000
- Std: 30,000
- Total fresh targets: 50,040

The deliberately narrow existing exact fragment produced 42 self-contained eligible slices (0.0839328537% of the fresh declaration sample). All 42 slice payloads match the sealed oracle-free input manifest by byte count and SHA-256.

Official exact-slice results:

- ACCEPT: 42 / 42
- REJECT: 0

CUDA-CIC results:

- ACCEPT: 26
- REJECT: 0
- UNSUPPORTED: 14
- REVIEW_REQUIRED: 2
- Decided coverage: 26 / 42 = 61.9047619%
- Matched decided objects: 26 / 26
- False accepts: 0
- False rejects: 0
- Mismatches: 0

By library:

- Init-Prelude: 1 ACCEPT / 1 slice
- Init: 14 ACCEPT / 25 slices; 10 UNSUPPORTED; 1 REVIEW_REQUIRED
- Std: 11 ACCEPT / 16 slices; 4 UNSUPPORTED; 1 REVIEW_REQUIRED

The two REVIEW_REQUIRED objects were retained fail-closed because historical exact engines disagreed on the same target shape (`Subrelation`).

The semantic checker was byte-exact unchanged from V5.1:

`20dd548f3cd268bd270442743a7b2454fa2a2fa536038eca30617727a7d649dd`

Therefore V5.2 restores fresh real-library ACCEPT evidence after the V5.1 reject-authority correction without adding new checker semantics.

## Track B — broad inductive qualification atlas

A separate fresh broad sample was used only for qualification; it had no ACCEPT authority.

- Sampled targets: 7,999
- Broad extractable: 4,010
- Bounded broad eligible: 3,999
- Broad eligible oversized: 11
- Has inductive wrapper(s): 3,987
- Inductive-only: 602
- Has natVal: 2,688
- Has proj: 3,347
- Has strVal: 431
- Simple nonrecursive zero-index: 274
- Simple nonrecursive zero-index **and inductive-only**: 153

The 153-member `simple_nonrecursive_noindex_inductive_only` population is the recommended next bounded semantic family for explicit specification and differential validation. This is qualification evidence only and is not yet CUDA-CIC semantic support.

## Scientific interpretation

V5.2 resolves the measurement problem exposed by V5.1:

1. The existing exact fragment is measured separately and continues to produce fresh, correct sealed ACCEPT decisions on real Init/Std declarations.
2. The broad real-library environment is measured as a semantic frontier rather than being mislabeled as checker coverage.
3. A concrete bounded inductive family now has a measurable real-library population large enough to justify a dedicated implementation.

V5.2 does **not** establish full Init/Std support, general inductive semantics, literal/projection semantics, full Arena support or general Lean-kernel equivalence.

## Next gate

Do not grant inductive ACCEPT authority directly from this atlas. First define and test an explicit bounded fragment centered on single-family, nonrecursive, zero-index inductives with no natVal/strVal/proj/mdata dependency, including targeted negative mutations and Python/CUDA differential checks. Promotion should require zero false accepts and zero unexplained Python/CUDA disagreements on a fresh holdout.
