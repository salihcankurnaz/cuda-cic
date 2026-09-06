# Grand Assault V3 — Fresh Holdout Review

Result artifact SHA-256: `551f21f295588db7346880b59decb952da464286e3de549df851bb3095a03c2d`

Final status: `V3_FRESH_HOLDOUT_GENERALIZATION_REVIEW_REQUIRED`.

## Preserved strengths

- V2 predecessor evidence exact.
- Implementation seal created before holdout generation.
- V2's 9 previously decided external objects preserved their decisions and remained Official-matched.
- Iterative dependency slicing removed all 10 prior perf `RecursionError` blockers.
- Fresh holdout decision seal exact; oracle was revealed only after decision sealing.
- Fresh holdout: 5,000 cases, 1,795 decided (35.9% coverage), 116 ACCEPT, 1,679 REJECT.
- False accepts: 0.

## Review-required findings

Development 56:
- 10 decided / 56 (17.86%).
- 1 false reject: `perf/grind-ring-5`.
- Cause: the external use of the historical `name_integrity` lane treated `rec_names_ok=False` as a necessary global condition. This heuristic is too strong for a large valid environment.

Fresh 5,000 mutation holdout:
- 1,795 decided / 5,000 (35.9%).
- 1,772 matched Official.
- 23 false rejects, 0 false accepts.
- All 23 false rejects are the same structural pattern: `drop_last` mutations of the `proj-non-structure` base.
- Official accepts these mutated objects because removing the final bad declaration leaves the bad projection expression unreachable. The current external `projection_static` certificate scans the whole raw expression pool and rejects the now-orphan projection anyway.

## Scientific interpretation

V3 did not pass because reject-only certificates were applied over a scope broader than Official declaration reachability. This is not a CUDA/Python disagreement and does not create false accepts; it is a fail-closed over-rejection bug.

The correction should be principled:

1. External `name_integrity` must not use historical `rec_names_ok` as a universal necessary condition; duplicate/reserved-name conflicts remain relevant.
2. `projection_static` rejection must be declaration-reachability scoped. Unreferenced raw expression rows are not sufficient grounds for rejection.
3. The revealed 5,000-case holdout is now development/regression data and must not be reused as a blind benchmark.
4. After correction, freeze the implementation and generate a new oracle-hidden holdout.

Claim boundaries remain unchanged: no full Arena support, no library CUDA-CIC verification, no general Lean semantic equivalence.
