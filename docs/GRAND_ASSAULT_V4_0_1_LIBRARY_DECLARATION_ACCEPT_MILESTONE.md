# CUDA-CIC Grand Assault V4.0.1 — Real Library Declaration ACCEPT Milestone

## Frozen source evidence

Original V4.0.1 RESULT ZIP SHA-256:

`e43086ba110c98b2ba8980a20ae4c1a4a147fe5069faaf6cc5eacca452bd384b`

Post-hoc finalized evidence ZIP SHA-256:

`98f4f34fd405d276a901cd890a744b7f0ccbed0f6341eb0047134eb5a966c3cf`

The post-hoc finalization changed no semantic decision, Official verdict, target selection, or extracted slice. It only joined the already present sealed evidence into the missing score/matrix/master/manifest outputs.

## Library provenance

Exact Arena revision:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Official full-library provenance:

- Init-Prelude: PASS
- Init: PASS
- Std: PASS

Raw exported environments:

- Init-Prelude: 3,714,854 bytes; 63,723 rows; 1,647 declarations
- Init: 324,561,407 bytes; 6,058,389 rows; 52,501 declarations
- Std: 551,674,936 bytes; 10,023,185 rows; 89,866 declarations

## Target/sample frontier

Oracle-free deterministic declaration sample:

- Init-Prelude: 500
- Init: 3,000
- Std: 6,500
- Total: 10,000

Conservative self-contained exact-slice eligibility:

- Init-Prelude: 6
- Init: 4
- Std: 2
- Total: 12 / 10,000 = 0.12%

All 12 selected slices passed the V4.0.1 raw-name referential-integrity gate.

## Sealed CUDA-CIC decisions

Decision SHA-256:

`e40cfd5112117253d852f9b7f906dc2fb59df8c45fd0a9b94c23dfe37154f7f1`

Oracle-free input SHA-256:

`ed3f36fbbbf8dbbd0ea09ad3c40e5c9b358ebb104207d7769fba9688a87edb79`

Checker SHA-256:

`c2255ac897af278aaa70fa0aebd4691f8d5883e724e42baecc3c3cdf4f4f8b05`

Decision input exposed no library name, target name index, expected label, or Official verdict.

CUDA-CIC distribution on the 12 real-library slices:

- ACCEPT: 5
- REJECT: 0
- UNSUPPORTED: 6
- REVIEW_REQUIRED: 1
- decided: 5 / 12 = 41.67%

Official exact-slice verdicts:

- ACCEPT: 12
- REJECT: 0

Correctness of decided CUDA-CIC objects:

- matched: 5 / 5
- mismatched: 0
- false accepts: 0
- false rejects: 0

Per library:

- Init-Prelude: 2 CUDA-CIC ACCEPT / 6 slices
- Init: 2 CUDA-CIC ACCEPT / 4 slices, 1 REVIEW_REQUIRED
- Std: 1 CUDA-CIC ACCEPT / 2 slices

Representative fresh ACCEPT targets include `semiOutParam`, `id`, `wfParam`, `imp_intro`, and `nestedProof`.

## Scientific interpretation

This is the first frozen milestone in the project showing sealed CUDA-CIC ACCEPT decisions that are subsequently accepted by the Official Lean checker on self-contained dependency slices extracted from real Init/Std environments.

The result is deliberately not reported as full Init/Std coverage. The measured declaration-slice eligibility frontier is only 12 / 10,000 = 0.12%, and that denominator must remain visible.

The largest extraction blockers are dominated by:

1. inductive constant dependencies;
2. `natVal`;
3. projections;
4. external constants;
5. `strVal`;
6. resource-limit closures.

## Claim boundary

This milestone does **not** establish:

- full Init or Std CUDA-CIC verification;
- full Arena support;
- CSLib or Mathlib support;
- general Lean-kernel semantic equivalence;
- universal performance superiority.

It establishes only the explicit sealed 12-slice library-declaration frontier and its 5/5 correct decided ACCEPT cases, plus the reported 0.12% slice-eligibility denominator.
