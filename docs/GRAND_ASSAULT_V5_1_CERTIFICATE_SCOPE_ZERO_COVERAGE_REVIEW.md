# CUDA-CIC Grand Assault V5.1 — Certificate-Scope Library Holdout Review

Date: 2026-09-10

## Frozen result

Original RESULT ZIP SHA-256:

`637544e28ddca8b8824baaa42656a1b892a6c454573f8e381353c0d1cf9972ec`

Post-hoc finalized review ZIP SHA-256:

`2bcd2055ad2e0992419c4a4df206ff46f4ff63964238c9dd4f649307e0e0044e`

Status:

`V5_1_CERTIFICATE_SCOPE_LIBRARY_HOLDOUT_ZERO_COVERAGE_REVIEW`

## Revealed correction regression

The six revealed V5 regression witnesses passed 6/6:

- three previously false-rejected valid library slices are no longer rejected; they are now fail-closed `UNSUPPORTED`;
- all three previous exact ACCEPT witnesses remain `ACCEPT`.

This validates the authority correction: the bounded `inductive_structural`, `positivity`, `field_universe`, and `recursor_metadata` descriptors are diagnostic-only for arbitrary external library environments.

## Fresh declaration sample

Fresh sample after excluding all V4 and V5 selected targets:

- Init-Prelude: 100
- Init: 12,000
- Std: 18,000
- total: 30,100
- prior-target overlap: 0

Extraction:

- self-contained eligible slices: 15,571 / 30,100 = 51.7309%
- bounded eligible <=2 MB: 15,550
- oversized eligible: 21
- selected for sealed decision: 2,000
- referential-integrity: 2,000 / 2,000 PASS
- Official exact-slice result: 2,000 / 2,000 ACCEPT

## CUDA-CIC fresh result

- ACCEPT: 0
- REJECT: 0
- UNSUPPORTED: 2,000
- REVIEW_REQUIRED: 0
- decided coverage: 0 / 2,000
- false accepts: 0
- false rejects: 0
- mismatches: 0

The decision and oracle-free input hashes match the recorded decision seal exactly.

## Why coverage became zero

Every selected slice hits `inductive_constant_dependency` in the existing exact target-slice route. Additional selected-surface feature incidence:

- `proj`: 1,650 / 2,000
- `natVal`: 1,312 / 2,000
- `letE`: 1,089 / 2,000
- `strVal`: 210 / 2,000

There are 390 selected cases whose internal exact-route blocker is only `inductive_constant_dependency`; 285 of those use only the current core expression vocabulary `Sort/BVar/Forall/Lam/App/Const`.

Therefore V5.1 is not a clean PASS: the reject-scope bug is fixed, but the fresh real-library sample has zero positive semantic coverage.

## Next frontier

Do not restore the bounded inductive heuristics as reject authority. The next semantic expansion should add a positive-only, conservatively admitted inductive-environment route and exact target checking, with a fresh declaration sample and oracle hidden until the CUDA decision seal.

Claim boundaries remain:

- no full Init/Std support;
- no general inductive semantics claim;
- no full Arena support;
- no general Lean-kernel semantic equivalence.
