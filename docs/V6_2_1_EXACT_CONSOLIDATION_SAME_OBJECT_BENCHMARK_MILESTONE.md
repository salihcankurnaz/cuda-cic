# CUDA-CIC V6.2.1 Exact Consolidation + Same-Object Benchmark Milestone

Frozen RESULT ZIP SHA-256:

`7abd813aab6087f5a2ed934e127c1086464fb41db0bf022aa969cb24c6e53348`

Status:

`V6_2_1_EXACT_CONSOLIDATION_SAME_OBJECT_BENCHMARK_PASS`

## Integrity

Independent RESULT manifest verification:

- 155 listed payloads
- 155/155 exact SHA-256 and byte-size matches
- 0 missing
- 0 extra

## Frozen provenance and correctness

Arena revision: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Tutorial blob: `782a81685f76f4917b9189d49a7e8f5679a376dc`

- raw SHA replay: 142/142
- official expected replay: 142/142
- exact AST Python: 35/35
- exact AST CUDA: 35/35
- bounded descriptor Python: 94/94
- bounded descriptor CUDA: 94/94
- normalized-AST closure Python: 13/13
- normalized-AST closure CUDA: 13/13
- closure mutations Python: 8/8 rejected
- closure mutations CUDA: 8/8 rejected
- supported Python/CUDA agreement: 142/142
- zero unexplained false accepts: true
- unsupported: 0
- frozen Tutorial coverage: 142/142

Unified classification:

- SUPPORTED_ACCEPT: 93
- SUPPORTED_REJECT: 49
- disagreements: 0

## Architecture consolidation

- exact CUDA extensions: 6 -> 1
- descriptor CUDA extensions: 4 -> 1 (from earlier V6.1 consolidation)
- normalized-AST closure extension: 1
- total runtime CUDA extensions: 8 -> 3
- single user-facing regression surface: true
- single monolithic CUDA kernel: false

## Same-object benchmark

Hardware/environment:

- Windows 10 build 26200
- Python 3.11.9
- PyTorch 2.6.0+cu124
- CUDA 12.4
- NVIDIA GeForce RTX 4070 Laptop GPU

All timing boundaries use the same frozen 142 raw Tutorial objects.

### Resident-input CUDA checker path

100 rounds:

- median: 163.415250 ms
- min: 151.308300 ms
- max: 175.225800 ms
- p10: 157.248400 ms
- p90: 168.117900 ms
- median throughput: 868.951949 objects/s

This is not pure kernel time. Legacy exact CUDA wrappers internally synchronize.

### Prepacked H2D + CUDA checker path

50 rounds:

- median: 165.692500 ms
- min: 155.618100 ms
- max: 175.049300 ms
- p10: 158.763100 ms
- p90: 172.003000 ms
- median throughput: 857.009219 objects/s

### Raw-object -> CUDA-CIC verdict wall-clock

7 rounds:

- median: 243.099300 ms
- min: 227.543600 ms
- max: 271.149400 ms
- p10: 235.190600 ms
- p90: 249.034300 ms
- median throughput: 584.123443 objects/s

### Official checker process baseline

Three rounds of 142 separate process invocations:

- median: 8114.825500 ms
- min: 8062.792400 ms
- max: 8444.893500 ms
- median throughput: 17.498836 objects/s

Do not interpret the ratio against the in-process CUDA-CIC paths as a Lean-vs-CUDA speedup. The official baseline contains one process launch per object and therefore has a materially different execution boundary.

## Claim boundary

This milestone supports complete semantic routing only for this exact frozen 142-object Tutorial corpus. It does not establish full Lean-kernel semantic equivalence, full Arena support, pure-kernel timing, universal GPU speedup, or one monolithic CUDA kernel.

## Next direction

Do not resume descriptor micro-versioning. The next high-value work is external blind-corpus expansion beyond the frozen Tutorial, while preserving the 142/142 regression and the consolidated 3-extension architecture. Performance work should use explicitly comparable in-process boundaries before any speedup claim is considered.
