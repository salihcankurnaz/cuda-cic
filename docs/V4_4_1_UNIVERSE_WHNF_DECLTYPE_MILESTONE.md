# CUDA-CIC V4.4.1 — Universe / WHNF / Declaration-Type Milestone

Frozen result ZIP SHA-256:

`6aed49c00fbf9b3e4dc034deb05debf7db2d872a7c0b1d4914f78cb746c648a7`

Status:

`V4_4_1_UNIVERSE_WHNF_DECLTYPE_CORE_PASS`

## Frozen external Arena corpus

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Cases:

- `008_forallSortWhnf` — official Lean ACCEPT; Python ACCEPT; CUDA ACCEPT
- `009_forallSortBad` — official Lean REJECT; Python REJECT; CUDA REJECT
- `010_nonTypeType` — official Lean REJECT; Python REJECT; CUDA REJECT
- `011_nonTypeAxiom` — official Lean REJECT; Python REJECT; CUDA REJECT

Agreement:

- official vs expected: 4/4
- Python vs official: 4/4
- CUDA vs official: 4/4
- Python vs CUDA: 4/4

The result manifest was independently recomputed and matched all 17 payload files exactly by byte length and SHA-256.

## Supported milestone boundary

This finite result exercises the measured mini-fragment additions:

- one symbolic universe parameter identity;
- concrete universe instantiation at constant use (`id.{2}` in the tested corpus);
- binder-domain WHNF before the `ForallE` sort check;
- declaration-type well-formedness;
- axiom type checking;
- previously frozen `Sort / BVar / ForallE / Lam / App / Const / beta / delta` behavior.

The positive `forallSortWhnf` object was accepted by all three lanes. The malformed binder-domain, malformed definition type, and malformed axiom type objects were rejected by all three lanes at the expected declaration boundary.

## Explicit exclusions

This milestone does **not** establish:

- general Lean universe normalization;
- arbitrary symbolic `max/imax` support;
- full Lean Kernel Arena support;
- full Lean-kernel semantic equivalence;
- full CIC correctness;
- any historical-priority or world-first claim.

Next gate: measure theorem references/self-reference and broader universe-normalization requirements before expanding the semantic checker again.
