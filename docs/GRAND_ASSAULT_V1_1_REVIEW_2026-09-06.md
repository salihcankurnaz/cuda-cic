# CUDA-CIC Grand Assault V1.1 — Review Evidence (2026-09-06)

Grand Assault V1.1 RESULT ZIP SHA-256:

`30e729e314ec52bba448b8336935b29f0c449ade68b330d476aeec177d5bbbc6`

## Frozen baseline

- V6.2.1 predecessor evidence exact: PASS
- Frozen Tutorial regression: 142/142
- CUDA/Official/Python frozen routing remains fully aligned on the 142-object corpus
- V6.2.1 benchmark rerun: PASS

## External Arena infrastructure

- Arena revision: `abc55357aee17c59dfdbf39c8a2e19739e23dd10`
- Exact checkout: PASS
- Official checker recovered through direct `lake build` fallback: PASS
- Global Arena corpus inventory: 63 tests
- Deterministic splits: dev 23, validation 5, blind 12, challenge 5, perf 18
- Direct committed raw external NDJSON tests: 12
- Direct raw tests official expected agreement: 12/12
- Blind oracle commitment: `af243225c2b55ef7a90db54f997ba9cb28102fa0a701247ae437cf5cfd85734e`

## Adversarial / metamorphic evidence

- Adversarial mutations requested/completed: 50,000/50,000
- Official oracle outcomes: 5,207 accept; 44,793 reject
- CUDA-CIC external verdict was not emitted for these mutations
- JSON-representation metamorphic tests: 3,000/3,000 stable
- Metamorphic mismatches: 0
- Metamorphic errors: 0

## Batch scaling evidence

Replicated frozen 142-object corpus, 20 timing rounds per multiplier:

- 142 objects: median 149.084 ms, ~952.48 objects/s
- 284 objects: median 145.831 ms, ~1,947.47 objects/s
- 568 objects: median 145.597 ms, ~3,901.17 objects/s
- 1,136 objects: median 146.488 ms, ~7,754.91 objects/s
- 2,272 objects: median 146.556 ms, ~15,502.63 objects/s
- 4,544 objects: median 147.285 ms, ~30,851.70 objects/s
- 9,088 objects: median 147.728 ms, ~61,518.49 objects/s
- 18,176 objects: median 148.932 ms, ~122,042.64 objects/s

This is replicated-corpus scaling, not evidence over 18,176 distinct Lean objects.

## IR candidate simulation

- 1,000,000 supported-lane IR candidates
- median 6.5735 ms
- ~152,125,952 candidates/s

This is an IR-level supported-lane CUDA gate simulation, not raw Lean proof end-to-end verification.

## Remaining orchestration blockers

Generated Arena tests and Init/Std/Cedar/CSLib were not successfully built because frozen `lka.py` opened UTF-8 YAML files using the Turkish Windows `cp1254` locale, causing `UnicodeDecodeError` before generation. Stage 04 also ended with an independent aggregation bug (`sum(bool and path_string)`), after all 57 rows had already been attempted.

Mathlib was not attempted because free disk (~17 GiB) was below the 80 GiB safety threshold. This is not a semantic failure.

## Claim boundary

Grand Assault V1.1 does **not** establish:

- general external CUDA-CIC semantic equivalence,
- full Arena support,
- Mathlib CUDA-CIC support,
- full Lean-kernel equivalence,
- a universal Lean-vs-CUDA speedup.

The next package is an orchestration-only V1.2 hotfix: UTF-8 mode for Arena subprocesses, correct `outcome: either` handling, and Stage 04 aggregation repair. No CUDA-CIC semantic rule is changed.
