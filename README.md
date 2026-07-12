# CUDA-CIC

An experimental GPU-accelerated type-checking prototype for a practical subset of Lean 4 expression trees.

The project explores whether batches of proof terms can be flattened into GPU-friendly integer arrays and checked in parallel. It is intended as a research prototype for AI-assisted proof search and batch verification experiments, not as a replacement for Lean's trusted kernel.

## What is implemented

- Flat integer encoding for Lean-style expression nodes
- CUDA kernels for level-by-level type propagation
- Experimental handling of sorts, variables, constants, applications, lambdas, Pi types, lets, natural-number terms, and reflexivity
- Iterative WHNF-oriented reductions for selected beta, delta, and zeta cases
- De Bruijn substitution with bounded GPU work stacks
- Universe-level evaluation for a supported subset
- Python/PyTorch integration and Lean-side export utilities

## Current scope

The implementation is intentionally bounded and incomplete. Some rules use simplified encodings or precomputed metadata, and the project does not yet cover the full Lean 4 kernel semantics.

Known limitations include:

- No claim of kernel equivalence or production-grade soundness
- Bounded substitution and reduction depth
- Partial support for universe parameters and inductive computation
- Simplified handling of selected Pi, let, recursor, and equality cases
- No complete support for mutual or nested inductive types

See the source and tests for the exact supported behavior.

## Architecture

```text
Lean 4 export
    -> parser and environment builder
    -> flat node arrays
    -> CUDA kernels
    -> validity and inferred-type results
```

Each expression node is represented by a fixed-width integer record so that batches can be processed without recursive host-side traversal in the hot path.

## Repository structure

```text
kernels/
  cic_type_check.cu
  cic_whnf.cu
  cic_defeq.cu
  cic_full.cu
  cic_subst.cu
  cic_universe.cu
lean4/
  export_trees.lean
  env_builder.py
tests/
  test_type_check.py
  test_whnf.py
  test_defeq.py
  test_subst_env.py
cuda_prover.py
lean4_to_gpu.py
```

## Requirements

- NVIDIA GPU with CUDA support
- CUDA Toolkit 12+
- PyTorch 2+
- Python 3.10+
- Lean 4 for exporting expressions
- A compatible C++/CUDA toolchain

## Quick start

```bash
git clone https://github.com/salihcankurnaz/cuda-cic.git
cd cuda-cic

python tests/test_type_check.py
python tests/test_whnf.py
python tests/test_defeq.py
python tests/test_subst_env.py
python tests/benchmark.py
```

To test the Lean export pipeline:

```bash
python lean4_to_gpu.py
```

## Research direction

The main question is whether candidate proofs produced by theorem-proving systems can be filtered efficiently through GPU-parallel structural checks before complete trusted verification in Lean.

Promising next steps include broader expression coverage, stronger differential testing against Lean, explicit soundness boundaries, and reproducible benchmark reporting.

## License

MIT
