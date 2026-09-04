# CUDA-CIC V4 Arena external pair bridge milestone

Date: 2026-09-04

## Status

`V4_ARENA_EXTERNAL_PAIR_BRIDGE_PASS`

This milestone extends the V3.2 tiny-fragment differential result with an externally sourced Lean Kernel Arena accept/reject boundary. It remains deliberately narrow and does **not** establish full Arena support, full Lean-kernel equivalence, full CIC correctness, historical priority, or any Lean-vs-GPU speedup claim.

## Frozen V4 result

Result ZIP SHA-256:

`17b3492b1d36966816e8f904f87607e6a2c4476e962ec717757b0a41dbf269b2`

Result manifest: 8/8 payload files matched recorded byte counts and SHA-256 hashes.

Environment:

- Python 3.11.9
- PyTorch 2.6.0+cu124
- CUDA available
- NVIDIA GeForce RTX 4070 Laptop GPU
- Lean executable from local elan installation

## Frozen external provenance

Lean Kernel Arena repository commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

`tutorial/Tutorial.lean` Git blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

Both exact provenance gates passed in the V4 run.

## Selected external cases

- `028_inferVar` — expected accept; structurally close to the V3.2 `Prop / Pi / lambda / BVAR` lane.
- `012_nonPropThm` — expected reject; tests the rule that a theorem's declared type must itself be a proposition.

The frozen Arena source contains both cases.

## V4 results

Positive bridge:

- local Lean theorem with the same core `inferVar` shape: accepted and exported;
- Python reference: accepted;
- CUDA positive lane: accepted.

External negative rule bridge:

- Lean rejected the local reproduction with: `type of theorem ... is not a proposition`;
- Python theorem-target guard rejected the corresponding rule;
- CUDA theorem-target guard rejected the corresponding rule;
- CUDA accepted a valid theorem-target control.

## Claim boundary

V4 is an **external-source rule-concordance** result, not yet an external same-object negative result. The Arena-generated `lean4export` NDJSON object itself was not yet fed through CUDA-CIC.

The next stage is V4.1: generate the frozen Arena tutorial NDJSON files through Arena's own `OUT/good|bad/<id>_<name>.ndjson` path, run the Arena official checker on those exact files, and feed the same parsed external objects into Python/CUDA micro-checkers.
