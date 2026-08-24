# CUDA-CIC: Experimental GPU Type Checking for a Lean4/CIC Fragment

> **Research status:** experimental CUDA backend for a selected Lean4/CIC fragment. It is not a replacement for Lean's trusted kernel, and correctness/performance claims apply only to the explicitly tested representation, fragment, fixtures, and benchmark setup.

CUDA-CIC explores whether selected Calculus of Inductive Constructions (CIC) operations can be represented and evaluated in batches on CUDA for AI-assisted theorem-proving workloads.

## Scope

The repository currently experiments with GPU implementations of selected operations including:

- **Type checking:** Sort hierarchy, Pi, Lambda, Application, Let, selected constants and inductive encodings;
- **WHNF reduction:** bounded beta/delta/zeta reduction and selected NatLit computation;
- **Definitional equality:** evaluation/comparison for the supported encoded fragment;
- **De Bruijn substitution:** bounded iterative substitution on the GPU representation;
- **Universe levels:** selected `zero` / `succ` / `max` / `imax` handling, with parameter handling still limited;
- **Lean4 export integration:** conversion of selected exported Lean expression trees into the repository's flat representation.

This is **not** a complete implementation of Lean4's kernel or all of CIC. Passing the repository tests does not establish semantic equivalence with Lean's trusted kernel outside the tested fixtures and supported fragment.

## Representation

Each encoded expression node uses seven integer fields:

```text
[node_type, child1, child2, child3, aux1, aux2, level]
```

The experimental kernels then operate over flat arrays of these nodes. This representation enables batch-oriented GPU evaluation but also imposes bounded-resource and feature-coverage limits that differ from Lean's kernel.

## Implemented experimental components

### WHNF

The CUDA path uses bounded iterative reduction rather than general recursive evaluation. The current implementation includes selected:

- beta reduction;
- delta unfolding;
- zeta reduction;
- Nat literal computation.

### De Bruijn substitution

The repository contains a bounded iterative substitution engine with a private per-thread work stack. This is designed to cover the repository's current fixtures; it should not be read as a proof of unrestricted substitution support.

### Universe-level evaluation

The project contains experimental handling for concrete universe-level expressions such as `zero`, `succ`, `max`, and `imax`. Parameter substitution remains limited/work-in-progress.

### Constant environment

`lean4/env_builder.py` builds the encoded constant environment used by the test and export pipeline. The environment is intentionally much smaller than the full Lean ecosystem.

## Tested fixtures

The repository includes exported/test fixtures involving examples such as:

- `Nat.add_comm`
- `Nat.add_zero`
- `Nat.zero_add`
- `Nat.add_assoc`
- `Nat.succ_add`
- `Nat.mul_comm`

A successful result on these fixtures means the repository's current encoded pipeline produced the expected result for those cases. It does **not** establish that arbitrary Lean theorems or complete libraries can be checked correctly by CUDA-CIC.

## Reproducible benchmark evidence

Publication-oriented benchmark evidence is committed under:

[`benchmarks/publication-evidence/2026-08-19-v27/`](benchmarks/publication-evidence/2026-08-19-v27/)

That artifact records the tested source revision, environment, raw measurements, and claim limitations. Benchmark results should be cited from that evidence rather than generalized to other GPUs, term distributions, or unsupported Lean/CIC features.

## Continuous integration

GitHub Actions performs **CPU-safe validation only**:

- Python source compilation for CPU-visible project code;
- JSON/CSV parsing of committed publication-evidence files.

The CI workflow intentionally does **not** execute CUDA extension compilation, GPU correctness tests, or GPU benchmarks on standard GitHub-hosted CPU runners. GPU-dependent tests still require an appropriate NVIDIA/CUDA environment.

## Requirements for GPU experiments

- NVIDIA GPU
- CUDA Toolkit compatible with the installed PyTorch build
- PyTorch with CUDA support
- Python 3.10+
- a compatible C++/CUDA compiler toolchain
- Lean4 only for workflows that export Lean expressions

## Quick start

```bash
git clone https://github.com/salihcankurnaz/cuda-cic.git
cd cuda-cic

# Environment/substitution test with CPU-visible logic
python tests/test_subst_env.py

# GPU-dependent experiments (require CUDA)
python tests/test_type_check.py
python tests/test_whnf.py
python tests/test_defeq.py
python tests/test_engine.py
python tests/benchmark.py
```

## Project structure

```text
cuda-cic/
  kernels/            # experimental CUDA kernels
  lean4/              # export fixtures and encoded environment tooling
  tests/              # CPU-visible and CUDA-dependent tests/benchmarks
  benchmarks/         # committed publication evidence
  cuda_prover.py      # experimental proof-generation/verification tooling
  lean4_to_gpu.py     # Lean export -> encoded GPU pipeline experiments
```

## Current limitations

- only a selected CIC/Lean4 fragment is represented;
- reduction/substitution paths use explicit bounds;
- universe-parameter support is incomplete;
- iota/general-inductive handling is limited;
- no mutual/nested-inductive completeness claim;
- no formal proof that the CUDA implementation is semantically equivalent to Lean's trusted kernel;
- no claim that arbitrary Lean libraries can be batch-verified by the current implementation.

These limitations define the current research scope.

## Potential research directions

- differential testing against an independent trusted/reference evaluator;
- larger sets of semantic correspondence fixtures;
- expanded Lean export coverage;
- GPU throughput studies under explicitly defined term distributions;
- proof-search pipelines that use the GPU path as an experimental filter while retaining trusted Lean verification.

## Citation

If you use this repository in research, cite the software and the exact benchmark/evidence revision used:

```bibtex
@software{cuda_cic,
  title={CUDA-CIC: Experimental GPU Type Checking for a Lean4/CIC Fragment},
  author={Salih Can Kurnaz},
  year={2026},
  url={https://github.com/salihcankurnaz/cuda-cic}
}
```

## License

MIT. See [`LICENSE`](LICENSE).
