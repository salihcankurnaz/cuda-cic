# CUDA-CIC Grand Assault V5.1 — Certificate-Scope Library Holdout Review

## Frozen artifact

Original V5.1 RESULT SHA-256:

`637544e28ddca8b8824baaa42656a1b892a6c454573f8e381353c0d1cf9972ec`

Post-hoc deterministic review artifact SHA-256:

`c761a2b1aade58c576ee1b3b1396021fb0203be1a63cf8adeb0e048afb428b4a`

Arena revision:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

## Result

V5.1 correctly removed the invalid external reject authority of the bounded Tutorial-family inductive descriptors. The six revealed development witnesses all passed: the three V5 false-reject witnesses became `UNSUPPORTED`, while the three V5 exact `ACCEPT` witnesses remained `ACCEPT`.

A new oracle-free declaration sample excluded all V4 and V5 selected targets:

- sampled declarations: 30,100;
- extractable self-contained slices: 15,571 / 30,100 = 51.730897%;
- bounded eligible slices: 15,550;
- selected for sealed decision: 2,000;
- prior-target overlap: 0.

All selected slices passed raw referential integrity and all 2,000 exact slices were accepted by the Official kernel.

CUDA-CIC result on the fresh selected surface:

- ACCEPT: 0;
- REJECT: 0;
- UNSUPPORTED: 2,000;
- REVIEW_REQUIRED: 0;
- false accepts: 0;
- false rejects: 0.

Therefore V5.1 is **not** a fresh-ACCEPT PASS. It is a clean correction milestone with zero fresh decided coverage.

## Dominant semantic frontier

Every one of the 2,000 selected slices contained at least one inductive wrapper and every exact target slice was blocked by `inductive_constant_dependency`. Additional blockers were:

- `inductive_constant_dependency + natVal + proj`: 998;
- `inductive_constant_dependency + proj`: 410;
- `inductive_constant_dependency` only: 390;
- `inductive_constant_dependency + natVal + proj + strVal`: 160;
- `inductive_constant_dependency + natVal`: 21;
- `inductive_constant_dependency + proj + strVal`: 11;
- `inductive_constant_dependency + strVal`: 10.

This establishes that the next semantic work should not restore heuristic rejection. The corrected fail-closed authority should be preserved, while fresh ACCEPT measurement is stratified so the narrow exact fragment is not drowned out by the much larger inductive environment stratum. A bounded inductive family should be promoted only after its own explicit specification and differential validation.

## Claim boundary

This milestone does not establish full Init/Std support, generic inductive checking, full Arena support, or general Lean-kernel semantic equivalence.
