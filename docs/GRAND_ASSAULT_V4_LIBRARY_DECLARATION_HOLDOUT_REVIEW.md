# CUDA-CIC Grand Assault V4 — Library Declaration Holdout Review

Date: 2026-09-07

## Status

REVIEW / PARTIAL EVIDENCE — not a PASS milestone.

Partial V4 RESULT SHA-256:

`6de6a42ff0b1bf55e0da12d945466f51868d0e8b4938256f8420bc8f1be8e209`

## What completed successfully

- Exact frozen Arena checkout: PASS.
- Official kernel build: PASS.
- Init-Prelude full export: PASS / Official ACCEPT.
- Init full export: PASS / Official ACCEPT.
- Std full export: PASS / Official ACCEPT.
- SQLite streaming indexes built for all three libraries.
- 10,000 declaration targets selected after implementation seal, without oracle labels.
- Conservative extractor produced 14 exact-slice candidates.
- CUDA-CIC decision subprocess sealed successfully on all 14 candidates.
- CUDA-CIC decisions: 2 ACCEPT, 12 UNSUPPORTED.

## Why V4 is not a scientific PASS

The Official kernel rejected all 14 extracted slices. Therefore the two CUDA-CIC ACCEPT decisions cannot be counted as valid library ACCEPT generalization; relative to the exact extracted objects they are false accepts.

Independent inspection of the slices identified a serialization / referential-integrity defect in the extractor rather than a new CUDA semantic rule failure:

1. binder name indices referenced by `forallE`, `lam`, and `letE` were omitted from the serialized slice;
2. universe parameter and declaration level-parameter name indices were not closed into the slice;
3. the SQLite name index parsed `pre` as a top-level field, while Lean4Export name constructors carry the parent inside nested `str` / numeric constructor payloads.

Every one of the 14 extracted slices contained referenced name indices without corresponding `in` name nodes.

The semantic checker itself remained frozen at SHA-256:

`c2255ac897af278aaa70fa0aebd4691f8d5883e724e42baecc3c3cdf4f4f8b05`

## Measured extraction frontier

10,000 sampled library declarations produced only 14 conservative exact-slice candidates (0.14% eligibility) before the name-closure fix.

Main extraction blockers among the remaining targets included:

- inductive constant dependencies;
- `natVal` and projection expression dependencies;
- external constant dependencies;
- `strVal` dependencies;
- resource-limit hits for very large dependency closures.

This eligibility rate must not be confused with checker coverage or full-library support.

## Next step

V4.0.1 fixes only slice serialization / name closure and adds a mandatory pre-oracle raw-name referential-integrity gate. No CUDA-CIC ACCEPT/REJECT semantic rule changes.

The corrected experiment must rebuild the same real library surfaces, reselect targets under the sealed implementation, emit name-closed slices, seal CUDA-CIC decisions, and only then evaluate the exact same slices with the Official kernel.

## Claim boundary

This V4 run does not establish:

- valid Init/Std CUDA-CIC ACCEPT generalization;
- full Init or Std verification;
- full Arena support;
- Mathlib support;
- general Lean-kernel equivalence.
