# CUDA-CIC V5.1 ULTRA — Multi-Family Milestone

## Frozen result

Archive:

`CUDA_CIC_V5_1_ULTRA_MULTI_FAMILY_RESULT_20260905_061333.zip`

SHA-256:

`07f70056275edeef7d2d6e48de2a9df0f595f579becc06ada76e78fcf93d6358`

Status:

`V5_1_ULTRA_MULTI_FAMILY_PASS_WITH_74_CASE_CORPUS`

Independent RESULT manifest verification: 123/123 listed payloads match exact byte lengths and SHA-256 values, with no missing or extra payloads.

## Provenance

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

`tutorial/Tutorial.lean` blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

Both checks are true.

## Frozen regression and descriptor lanes

- Baseline frozen hashes: 37/37
- Baseline official-vs-expected: 37/37
- Structural Python lane: 17/17
- Structural CUDA lane: 17/17
- Positivity Python lane: 3/3
- Positivity CUDA lane: 3/3
- Constructor-field universe Python lane: 4/4
- Constructor-field universe CUDA lane: 4/4
- Mutation rejection, Python: 8/8
- Mutation rejection, CUDA: 8/8
- CUDA runtime: PASS

The descriptor lanes remain deliberately narrower than a general Lean inductive checker.

## New captured external corpus

The same run discovered and replayed 37 additional exact Tutorial objects with official expected agreement 37/37.

The additional corpus spans:

- recursor metadata/type/reduction examples;
- projections and projection rejection cases;
- rule-K examples;
- Nat literal typing/reduction;
- proof irrelevance;
- unit eta.

All baseline and new objects were copied into the RESULT archive, yielding 74/74 raw NDJSON objects captured.

## Reporting hotfix note

`NEXT_PLAN.json` is empty in this frozen result because successful rows written to `FUTURE_MATRIX.json` omitted a `found: true` field, while the next-plan loop filtered on `r.get("found")`. This is a reporting-only bug: the final result independently records `future_discovered=37/37`, `future_official_expected=37/37`, and `raw_corpus_captured=74/74`, and the raw files are present in the archive. It does not affect any semantic agreement or mutation gate.

## Claim boundary

This milestone does not establish:

- a full Lean inductive checker;
- general positivity correctness;
- general recursor type derivation or recursor reduction;
- projection semantics;
- proof irrelevance semantics;
- full Arena support;
- full Lean-kernel semantic equivalence.

It establishes exact frozen external corpus expansion plus bounded Python/CUDA descriptor validation on the declared lanes.
