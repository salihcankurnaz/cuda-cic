# CUDA-CIC Scientific Audit — 2026-09-04

## Decision

`ADVANCE_DIFFERENTIAL_VALIDATION`

CUDA-CIC has a real experimental GPU execution core and a reproducible throughput artifact, but the current evidence does **not** yet establish semantic correspondence with Lean's trusted kernel for exported proof terms. The highest-value next experiment is therefore an external, accept/reject differential-validation campaign rather than another throughput-only benchmark.

## Frozen evidence already supported

The V27 publication artifact records:

- 29/29 internal encoded-term expected-type cases passed;
- 1,000,000-input kernel-only median: 7.833040 ms across 50 CUDA-event rounds;
- corresponding benchmark throughput: about 127.66 million encoded inputs/s;
- 100,000-input end-to-end median: 443.448 ms across 20 wall-clock rounds;
- corresponding end-to-end throughput: about 225.5 thousand encoded inputs/s.

The artifact explicitly excludes full Lean-kernel semantic equivalence, Lean-vs-GPU speedup ratios, world-first claims, and universal performance claims.

## Adversarial source findings

### 1. Real-Lean path checks types, not proof terms

`lean4/export_trees.lean` exports theorem types and theorem proof terms. `lean4_to_gpu.py` parses both into `entry['type']` and `entry['proof']`.

However, the current `main()` builds its GPU workload from:

```python
theorems = {name: e['type'] for name, e in entries.items() if e.get('type')}
```

The proof term is not selected for the batch. Therefore the present path cannot be cited as evidence that exported Lean proof terms themselves are accepted or rejected correctly.

### 2. Historical CPU/GPU benchmark is not an identical-corpus comparison

The historical benchmark creates CUDA inputs with a repository-authored encoded-term generator. Its Lean CPU path separately writes Lean theorem declarations such as `rfl` and `native_decide` examples.

Because the CPU and GPU paths do not consume the exact same proof object/serialization, the historical ratio is not a valid semantic-equivalence benchmark and should not be reported as a Lean-kernel speedup.

### 3. Internal expected-type checks are not independent validation

The 29/29 result is useful regression evidence, but the expected outputs and the tested representation are repository-controlled. A checker can pass such a suite while still accepting malformed objects, rejecting valid objects, or mishandling unsupported Lean features.

The next campaign must therefore include an independently maintained good/bad corpus.

## Current external landscape

### Lean proof validation and independent checkers

Lean's current proof-validation documentation recommends stronger cross-checking for high-risk proof validation and identifies the official kernel plus independent external checkers such as `nanoda` as the high-confidence route:

- <https://lean-lang.org/doc/reference/latest/ValidatingProofs/>

The Lean Kernel Arena provides a public suite of accepted, rejected, corner-case, and performance exports across many independent Lean checkers:

- <https://arena.lean-lang.org/>

This is the strongest immediate benchmark design reference for CUDA-CIC. The goal should not initially be to support every Arena test. It should be to declare a precise supported subset and obtain zero unexplained accept/reject disagreements inside that subset.

Lean 4.33.0 also documents recent kernel soundness fixes, reinforcing why negative/rejection tests and implementation diversity matter:

- <https://lean-lang.org/doc/reference/latest/releases/v4.33.0/>

### Related GPU/formal work found in the targeted search

The following are relevant but do not, from the reviewed public descriptions, establish the same claim as CUDA-CIC:

- **TorchLean CUDA** uses CUDA for selected tensor/runtime operations while explicitly keeping CUDA machine code outside Lean's trusted kernel boundary: <https://lean-dojo.github.io/TorchLean/cuda/>
- **Lean Copilot** uses local/cloud LLM inference, optionally on GPUs, for proof automation; this is GPU model inference rather than a GPU Lean kernel checker: <https://github.com/lean-dojo/LeanCopilot>
- **Argument Computer `ix`** is a Lean proof-carrying-code platform with GPU proving through SP1/CUDA paths; its public description is a different proof-system architecture, not evidence of CUDA-CIC semantic equivalence: <https://github.com/argumentcomputer/ix>
- **Kuiper** uses dependent types/separation logic to verify GPU programs and generate CUDA; it addresses correctness of GPU programs rather than moving a Lean/CIC checker onto the GPU: <https://github.com/FStarLang/kuiper>
- **VerifiedGPU** and **Hesper** similarly study verified GPU programming or verified GPU kernels from Lean-side specifications rather than the exact CUDA-CIC checker problem.

A targeted search did **not** find a directly matching published system that clearly claims the same combination of a GPU-batched checker for a Lean/CIC fragment plus semantic differential validation against Lean. This is **not** a historical-priority proof and must not be phrased as “first,” “world first,” or “no prior work exists.”

## Exact next experiment

### V1 — External Differential Validation Preflight

The first validation package should:

1. hash-bind the current CUDA-CIC repository revision;
2. enumerate the syntax/features actually supported by the exporter, flattener, environment, and CUDA kernel;
3. import a frozen subset of Lean Kernel Arena tutorial good/bad tests or another independently maintained export corpus;
4. classify each case as `SUPPORTED`, `UNSUPPORTED`, or `AMBIGUOUS` **before** observing CUDA-CIC outcomes;
5. run the official/reference outcome and CUDA-CIC on the same semantic object where the current representation permits it;
6. report TP/TN/FP/FN and unsupported counts;
7. fail the promotion gate on any false accept, false reject, silent truncation, unknown-node fallback, or representation mismatch;
8. preserve raw per-case traces and exact input/output hashes;
9. benchmark throughput only on the exact cases that passed the correspondence gate.

### Required negative classes

At minimum, the supported-fragment campaign should attempt to cover:

- unbound de Bruijn variables;
- function application with wrong argument type;
- malformed universe-level use;
- invalid constant/environment references;
- bad recursor/constructor use where supported;
- definitional-equality mismatches;
- free-variable/closed-term violations relevant to the encoded contract;
- resource-bound overflow/truncation cases.

## Promotion rule

A future statement such as “CUDA-CIC correctly checks a selected Lean/CIC fragment” should require:

- a written fragment specification;
- exact same-object differential validation;
- accepted **and** rejected external cases;
- zero unexplained false accepts in the declared supported corpus;
- explicit handling of unsupported features;
- preserved provenance and independently recomputable summaries.

Performance claims remain secondary until this correctness gate is closed.
