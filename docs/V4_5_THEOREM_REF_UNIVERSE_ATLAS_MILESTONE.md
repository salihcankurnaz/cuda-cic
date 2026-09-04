# CUDA-CIC V4.5 theorem-reference / universe atlas milestone

Frozen external source:

- Lean Kernel Arena commit: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`
- `tutorial/Tutorial.lean` Git blob: `782a81685f76f4917b9189d49a7e8f5679a376dc`

Frozen V4.5 RESULT ZIP SHA-256:

`710bc4fbfe96f7a9107399dea873eb4bb2f93425db680135570b25d7e8c40ea0`

## Atlas result

Status: `V4_5_THEOREM_REF_UNIVERSE_ATLAS_COMPLETE`

- manifest: 23/23 exact payloads
- Arena exact commit: true
- tutorial blob match: true
- unique target discovery: true
- expected good/bad subdirectories: true
- official Lean-kernel agreement with expected labels: 7/7
- no additional expression kind appeared in this target set

Exact target set:

- `013_thmProof` — official ACCEPT
- `014_selfProof` — official REJECT
- `015_levelComp1` — official ACCEPT
- `016_levelComp2` — official ACCEPT
- `017_levelComp3` — official ACCEPT
- `018_levelParams` — official ACCEPT
- `019_tut06_bad01` — official REJECT

## Measured next-fragment requirements

The atlas isolates the following requirements for the next semantic core:

- declaration-order enforcement;
- earlier theorem constant references;
- theorem opacity (theorem values are not delta-unfolded);
- rejection of a reference to the declaration currently being checked;
- concrete `imax` universe normalization;
- polymorphic definition universe instantiation;
- symbolic single-parameter propagation;
- rejection of duplicate universe parameters.

Notably, `thmProof` contains a backward reference to the earlier theorem `pImpliesP`, while `selfProof` contains a self reference to `selfProof`. `levelComp1..3` use only concrete `imax` expressions. `levelParams` uses one symbolic parameter and a concrete instantiation. `tut06_bad01` isolates duplicate level parameters.

## Claim boundary

This is a structural/provenance atlas. It does **not** establish a new semantic-equivalence result by itself, full Lean-kernel equivalence, full Arena support, general symbolic `max/imax` normalization, or historical priority.

The next planned correctness gate is `CUDA_CIC_V4_5_1_THEOREM_REF_UNIVERSE_CORE`.
