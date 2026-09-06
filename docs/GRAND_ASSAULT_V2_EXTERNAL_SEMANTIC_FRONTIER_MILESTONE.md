# CUDA-CIC Grand Assault V2 — External Semantic Frontier Milestone

Date: 2026-09-06

## Frozen result

- RESULT ZIP SHA-256: `be6536a947bec535a3fb34f6cf3f6d50e98fea6a52c5569396bc4bc9f693bd63`
- Status: `V2_EXTERNAL_SEMANTIC_FRONTIER_PASS`
- Frozen predecessor V1.3 RESULT SHA-256: `9ed18c2f8657664b34e997a73849f0dedf67b67ffc459dac6de77b7f9af9681d`
- Arena commit: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`

## Integrity

- RESULT entries: 81 total
- RESULT manifest payloads: 80
- Manifest missing: 0
- Manifest extra: 0
- Hash/byte mismatches: 0
- External raw cases: 56/56 SHA/byte exact

## Oracle isolation / sealing

- `SEALED_EXTERNAL_DECISIONS.json` SHA-256: `c22c7996aadf538110c10f0dba180cf3d3a3d36f854d8865f750a42126cf5289`
- `ORACLE_FREE_INPUT_MANIFEST.json` SHA-256: `972f345fc880c8b60914258b9e54bdc458e45a6c9641398fe8ce016e991e06f6`
- Seal hashes independently recomputed exact
- Oracle-free decision manifest contains no test names, YAML outcomes, or expected labels
- Blind oracle commitment exact: `af243225c2b55ef7a90db54f997ba9cb28102fa0a701247ae437cf5cfd85734e`

## External semantic frontier

Across 56 external light/corner/perf Arena objects:

- Decided: 9/56 = 16.0714%
- ACCEPT: 2
- REJECT: 7
- UNSUPPORTED: 37
- REVIEW_REQUIRED: 10
- Matched decided objects: 9/9
- Mismatched decided objects: 0
- False accepts: 0
- False rejects: 0

Blind subset contained in this 56-object surface:

- Total: 10
- Decided: 2/10 = 20%
- ACCEPT: 0
- REJECT: 2
- UNSUPPORTED: 8
- REVIEW_REQUIRED: 0
- Matched: 2/2
- False accepts: 0
- False rejects: 0

## Decided objects

ACCEPT through complete exact-AST target-slice routes:

- `level-index-out-of-order`
- `sparse-name-index`

REJECT through generic necessary-condition certificates:

- `ctor-num-fields`
- `extra-rec`
- `nested-nonuniform-param` (`outcome: either`, Official-compatible)
- `nested-unused-param`
- `orphan-ctor`
- `orphan-rec`
- `proj-non-structure`

## Route evidence

Successful exact routes:

- v481: 2
- v451: 2
- v441: 2

Reject certificate counts:

- projection_static: 3
- name_integrity: 4
- inductive_structural: 5
- recursor_metadata: 4

Decision-reason distribution:

- no complete exact route and no reject certificate: 37
- exact AST unanimous: 2
- necessary-certificate rejects: 7
- case-local extraction error: 10

The 10 REVIEW_REQUIRED cases are all perf cases where the recursive target dependency slicer hit Python `RecursionError`; they are not semantic mismatches.

## Library-scale predecessor evidence preserved

V1.3 official-accepted exports remain frozen as frontier corpora, not CUDA-CIC-verified libraries:

- Init-Prelude: 3,714,854 bytes
- Init: 324,561,407 bytes
- Std: 551,674,936 bytes
- CSLib: 2,145,661,820 bytes

Cedar remains host-platform blocked. Mathlib was not tested due disk guard.

## Scientific claim boundary

This milestone supports only the measured external frontier above. It does **not** establish:

- general Lean kernel semantic equivalence;
- full Arena support;
- Init/Std/CSLib CUDA-CIC verification;
- Mathlib CUDA-CIC support;
- one monolithic CUDA kernel;
- universal performance superiority.

ACCEPT is emitted only from a complete exact target slice with Python/CUDA agreement. Generic certificates are reject-only. Everything else remains fail-closed as UNSUPPORTED or REVIEW_REQUIRED.

## Next direction

Do not optimize on the already revealed external oracle and then call the same surface blind. The next scientific stage should:

1. remove target-slicer recursion limits with an iterative dependency walk;
2. use the now-revealed 56-object corpus as development/regression only;
3. increase generic semantic coverage without test-name special casing;
4. freeze the implementation before creating a fresh blind holdout;
5. score that fresh holdout only after sealing CUDA-CIC decisions.
