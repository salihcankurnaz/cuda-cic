# CUDA-CIC v2 — Historical Status and Current Claim Boundary

> **Status correction (2026-09-04):** this file originally contained development-era claims such as “100% correctness,” a large Lean-vs-GPU speedup ratio, world-first/superlative language, and wording suggesting broad Lean-kernel capability. Those claims are **not supported by the current publication evidence** and are withdrawn. The repository README and the frozen publication-evidence artifact define the public claim boundary.

## What is implemented

CUDA-CIC is an experimental CUDA backend for a selected encoded Lean/CIC fragment. The repository contains experimental support for:

- Sort/Pi/Lambda/Application/Let forms;
- selected constants and constructor encodings;
- bounded WHNF reduction;
- bounded substitution and de Bruijn handling;
- selected definitional-equality paths;
- selected universe-level operations;
- Lean-expression export/parsing experiments;
- batch-oriented CUDA execution.

This is not a complete Lean 4 kernel and is not a drop-in trusted checker.

## Frozen evidence currently supported

The publication artifact under `benchmarks/publication-evidence/2026-08-19-v27/` supports only the following scoped statements:

- **29/29** cases passed in the repository's internal encoded-term expected-type suite.
- At a batch size of **1,000,000 encoded inputs**, 50 CUDA-event rounds gave a median kernel-only time of **7.833040 ms**, or about **127.66 million encoded inputs/s** in that exact benchmark.
- At **100,000 encoded inputs**, the recorded end-to-end Python/NumPy/H2D/kernel/sync/readback path had a median of **443.448 ms**, or about **225.5 thousand inputs/s**.

These measurements are environment- and workload-specific. They do **not** establish semantic equivalence with Lean's trusted kernel, a Lean-vs-GPU speedup ratio, or universal performance.

## Scientific audit correction

A 2026-09-04 source audit identified two important boundaries that must be resolved before stronger correctness claims:

1. `lean4_to_gpu.py` parses both theorem types and proof terms, but its current `main()` constructs the GPU batch from the parsed theorem **type** (`entry['type']`), not the proof term (`entry['proof']`). Therefore the current “real Lean4 theorems” path does not by itself demonstrate proof-term checking.
2. The historical benchmark generates its CUDA inputs manually and creates a separate set of Lean CPU theorems. The two paths are not an identical-corpus differential checker test, so the historical CPU-vs-GPU ratio is not a scientifically valid kernel-equivalence or speedup result.

See `docs/SCIENTIFIC_AUDIT_2026-09-04.md` for the current research decision.

## Next scientific gate

The next priority is **correctness before throughput**:

1. create an explicit supported-fragment contract;
2. feed the same exported proof objects to the reference checker and CUDA-CIC;
3. include both accepted and deliberately rejected cases;
4. record an exact accept/reject confusion matrix and failure classes;
5. prefer an external corpus such as the supported subset of Lean Kernel Arena rather than only repository-authored fixtures;
6. independently re-run accepted cases with Lean's official kernel and, where practical, an external checker such as `nanoda`;
7. make performance comparisons only after semantic correspondence is established for the declared corpus.

Until that gate passes, CUDA-CIC should be described as an **experimental GPU batch evaluator/type checker for a selected encoded Lean/CIC fragment**.
