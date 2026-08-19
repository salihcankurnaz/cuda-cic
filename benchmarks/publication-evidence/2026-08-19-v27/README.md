# CUDA-CIC benchmark evidence — 2026-08-19

This directory contains a reproducibility artifact for commit
`8a4e0c0b594e98aa9d3e615134a45c98ba8b0792` of `salihcankurnaz/cuda-cic`.

## What this artifact supports

- **Internal correctness:** 29/29 cases passed in the repository's
  encoded-term expected-type suite.
- **Kernel-only throughput:** at a batch size of 1,000,000 encoded proofs, 50 CUDA-event
  timing rounds produced a median of **7.833040 ms**, corresponding to
  **127.66 million proofs/s**.
- The 1,000,000-proof kernel timing distribution had p10 **7.803449 ms**,
  p90 **7.889408 ms**, and coefficient of variation **0.62%**.
- **End-to-end path:** at 100,000 encoded proofs, 20 wall-clock rounds produced a
  median of **443.448 ms**, corresponding to
  **225.5 thousand proofs/s**.

## Timing scopes

### Kernel-only

The kernel-only measurements time the CUDA checker after encoded tensors are already
allocated and transferred to the GPU. They therefore measure the CUDA checking stage,
not proof ingestion.

### End-to-end path

The end-to-end measurements include:

1. Python proof-list construction;
2. NumPy array construction;
3. host-to-device tensor creation/transfer;
4. CUDA checker execution;
5. synchronization; and
6. one-value device-to-host readback.

The large difference between kernel-only and end-to-end throughput indicates that the
current host-side representation/preparation path dominates total runtime.

## Reproducibility

The artifact is bound to the exact repository commit and source hashes in
[`source_hashes.json`](source_hashes.json). Environment/toolchain information is in
[`environment.json`](environment.json).

Raw timing rounds are included rather than only aggregate values:

- [`gpu_kernel_raw_rounds.csv`](gpu_kernel_raw_rounds.csv)
- [`gpu_end_to_end_raw_rounds.csv`](gpu_end_to_end_raw_rounds.csv)

Aggregate tables:

- [`gpu_kernel_summary.csv`](gpu_kernel_summary.csv)
- [`gpu_end_to_end_summary.csv`](gpu_end_to_end_summary.csv)

Internal correctness cases:

- [`internal_correctness_raw.csv`](internal_correctness_raw.csv)

Machine-readable claim-safe summary:

- [`CLAIM_SAFE_RESULTS.json`](CLAIM_SAFE_RESULTS.json)

## Explicit limitations

This artifact does **not** establish:

- full semantic equivalence with the Lean kernel;
- a Lean-versus-GPU speedup ratio;
- a world-first or prior-art claim; or
- universal performance across hardware, proof distributions, or workloads.

The correctness result is scoped to the repository's internal encoded-term expected-type
suite, and the performance results are scoped to the environment and workload recorded here.
