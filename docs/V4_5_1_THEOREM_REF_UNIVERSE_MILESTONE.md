# CUDA-CIC V4.5.1 — theorem-reference / universe milestone

Status: `V4_5_1_THEOREM_REF_UNIVERSE_CORE_PASS`

Frozen result ZIP SHA-256:

`f6361ed2b6ea5ed1c81f6221c17605c8c12f389ed9610e7f2bd99c357b9faf43`

Result manifest verification: 23/23 payload files matched exact byte lengths and SHA-256 values.

Frozen external source:

- Lean Kernel Arena commit: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`
- `tutorial/Tutorial.lean` Git blob: `782a81685f76f4917b9189d49a7e8f5679a376dc`

## Differential result

Seven exact external Arena NDJSON objects were checked by the Arena official Lean kernel, the CUDA-CIC Python checker, and the CUDA-CIC CUDA checker.

- official Lean vs expected label: 7/7
- Python vs official Lean: 7/7
- CUDA vs official Lean: 7/7
- Python vs CUDA: 7/7
- CUDA runtime status: PASS

Raw external object hashes:

- `013_thmProof`: `5e4664a6d4f05afbeff4e0af19681e88b2817c48787a9a281c4ba95d80483333`
- `014_selfProof`: `f39b1bba5099649997a6c7cd49c870f91dfc86432979eafae58692d236142499`
- `015_levelComp1`: `2e6b6016ac241c9e1dd01ee86782f21adabd928bca24880b60619de453bec0c3`
- `016_levelComp2`: `aa971f4ba7603e183ebcf90a8ac92241f5fa2a96fbc6659e45380f52de3ffd6e`
- `017_levelComp3`: `e11ecbb09540778e2d2d0084d7759ce1c1483ca7f02168b87e1ec8bd1bf2c5cd`
- `018_levelParams`: `d78d458ea81bb210c80d3915976a03536f1b267879207f3604745b777014a167`
- `019_tut06_bad01`: `9c5c0329065ef0b470c7b43a365c30a0098697dbeb8d69f2c2bea2e345ab9533`

Key official rejection loci:

- `014_selfProof`: `(kernel) unknown constant 'selfProof'`
- `019_tut06_bad01`: duplicate universe level parameter `u`

## Supported incremental fragment

Relative to the earlier frozen milestones, this result adds finite external evidence for:

- references to earlier theorem declarations;
- theorem opacity (theorem values are not delta-unfolded);
- rejection of current/self declaration references;
- concrete `max` / `imax` normalization used by the selected cases;
- one symbolic universe parameter propagated through a polymorphic definition and concretely instantiated at use sites;
- duplicate universe-parameter rejection.

## Claim boundary

This is a finite seven-object external differential result for the implemented fragment. It does not establish full Lean-kernel semantic equivalence, full Lean Kernel Arena support, arbitrary symbolic `max`/`imax` normalization, full CIC correctness, historical priority, or a Lean-vs-GPU speedup claim.
