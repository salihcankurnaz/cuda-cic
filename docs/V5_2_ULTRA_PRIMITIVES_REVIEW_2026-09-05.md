# CUDA-CIC V5.2 — Primitive Lanes Review

Result archive:

`CUDA_CIC_V5_2_ULTRA_PRIMITIVES_RESULT_20260905_063013.zip`

SHA-256:

`d34c03a3c4488c1315f022340cd1aafbf134524e0a58669e39470871a9438f96`

## Integrity

The result manifest lists 153 payload files. Independent verification found:

- 153/153 listed payloads present;
- exact byte sizes for every payload;
- exact SHA-256 for every payload;
- no unlisted payload files.

## Semantic lanes

These gates passed completely:

- Python vs expected: 28/28;
- CUDA vs expected: 28/28;
- Python vs CUDA: 28/28;
- deterministic negative mutations rejected by Python: 10/10;
- deterministic negative mutations rejected by CUDA: 10/10;
- CUDA runtime status: PASS;
- frozen raw-object hashes: 74/74 exact.

Lane breakdown:

- recursor metadata: 10/10 Python and CUDA;
- projection-static: 7/7 Python and CUDA;
- rule-K: 3/3 Python and CUDA;
- Nat-literal: 2/2 Python and CUDA;
- proof-irrelevance eligibility: 3/3 Python and CUDA;
- unit-eta eligibility: 3/3 Python and CUDA.

These remain bounded host-parsed descriptor lanes, not full Lean-kernel semantic implementations.

## Why the final V5.2 status is REVIEW_REQUIRED

Two orchestration bugs were found.

### 1. Official-checker wrapper name shadowing

The runner first binds the official checker directory to a Python variable named `official`, then defines a helper function with the same name. Inside that helper, `cwd=official` therefore receives the function object instead of the filesystem path.

Every official replay invocation consequently raises:

`TypeError: expected str, bytes or os.PathLike object, not function`

This makes every official result appear as rejection. Hence the reported 24/74 frozen official agreement merely counts the 24 bad-directory objects and is not a semantic result.

### 2. Frozen tutorial test-count assumption

V5.2 assumed that test IDs 110 through 149 existed. The exact frozen Tutorial build log at Arena commit `abc55357aee17c59dfdbf39c8a2e19739e23dd10` emits exactly 142 consecutive cases, IDs 001 through 142. There are no 143–149 objects at this revision.

Therefore the 33/40 discovery count is exactly the available 110–142 suffix, not a discovery failure.

## Correct interpretation

V5.2 establishes clean 28-case Python/CUDA bounded-lane agreement, 10/10 mutation rejection, and 74/74 exact raw provenance replay. The official-kernel replay counters in this result are invalid because of the wrapper bug, and the 114-case corpus target was impossible at the frozen Arena revision because the tutorial ends at ID 142.

The next hotfix should keep the semantic lanes unchanged, fix the official checker path binding, derive the tutorial test range from the actual export, and replay/capture all 142 frozen Tutorial objects in one run.

## Claim boundary

Do not treat this review result as official 74-case differential validation. Do not claim full recursor, projection, rule-K, literal, proof-irrelevance, unit-eta, full Arena, or full Lean-kernel equivalence from V5.2.
