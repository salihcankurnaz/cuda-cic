# Grand Assault V5 — Inductive Environment Frontier Review

## Frozen source result

- Original RESULT ZIP SHA-256: `9e2fec4c8564c0ce831639618d52efee8cc08dc9b197a4dd80d34f7807912bc5`
- Post-hoc deterministic review ZIP SHA-256: `43f5b076ccedb98130089134d052cedfa73e9c0c9a51220e95c72f8c0d05f7d7`
- Semantic checker SHA-256 remained: `c2255ac897af278aaa70fa0aebd4691f8d5883e724e42baecc3c3cdf4f4f8b05`

## Extraction frontier

V5 selected a fresh declaration sample excluding the entire V4 sample:

- Init-Prelude: 1,000
- Init: 7,000
- Std: 12,000
- total: 20,000
- V4 target overlap: 0

Expanded extraction produced:

- self-contained eligible slices: 10,803 / 20,000 = 54.015%
- bounded eligible (<=2 MB): 10,791
- oversized eligible: 12
- selected for sealed decision: 2,000
- selected with inductive wrappers: 1,997 / 2,000

This is a large extraction improvement over V4.0.1 (12/10,000 = 0.12% eligibility). This is an extractor result, not semantic checker coverage.

Remaining extraction blockers:

- `external_constant_dependency`: 7,476
- `resource_limit:max_nodes`: 1,721

## Referential integrity and Official oracle

All selected slices passed the raw-reference integrity gate:

- 2,000 / 2,000 names/levels/expressions closed
- 2,000 / 2,000 exact slice SHA/byte records matched the oracle-free input manifest
- Official kernel: 2,000 ACCEPT / 0 REJECT

Decision seal:

- sealed decision SHA-256: `a7d5f4bf9b50e6a421df1b99c3be123cbfdf542a67e3e454d8656df712390c42`
- oracle-free input SHA-256: `e6019261d92a285ee878bb07ff7418363c870e6bc0e64ea11a081f470b111dff`
- case count: 2,000
- oracle labels read by decision process: false
- test-name special casing: false

## CUDA-CIC result

On the 2,000 sealed valid library slices:

- ACCEPT: 3
- REJECT: 39
- UNSUPPORTED: 1,958
- REVIEW_REQUIRED: 0
- decided: 42 / 2,000 = 2.1%
- Official ACCEPT: 2,000 / 2,000
- matched decided objects: 3
- mismatched decided objects: 39
- false accepts: 0
- false rejects: 39

The three fresh correct ACCEPTs were real Init/Std declaration slices. The result is nevertheless **REVIEW_REQUIRED** because 39 valid Official-ACCEPT slices were rejected.

## False-reject root cause

The 39 false rejects cluster cleanly:

- 38: `inductive_structural + positivity + recursor_metadata`
- 1: `field_universe`

The dominant valid imported inductive dependency was `Lean.Syntax` (36 cases), with:

- recursive family
- 4 constructors
- 3 recursors

Two additional cases involved valid `Lean.Parser.Tactic.MRefinePat` with 5 constructors and 2 recursors.

The remaining single false reject involved valid `Std.BundledIterM` under the bounded `field_universe` heuristic.

These checks originated as bounded Tutorial-family descriptors. V5 demonstrates that they are not universal necessary conditions for arbitrary real Lean library environments. They therefore must not retain generic external-library reject authority.

## Interpretation

V5 is a genuine extraction milestone but not a clean semantic-checker PASS.

Valid conclusions:

1. expanded real-library extraction is working and increased eligibility from 0.12% to 54.015% on fresh target samples;
2. 2,000/2,000 selected extracted slices were well-formed and Official ACCEPT;
3. 3 fresh real-library CUDA-CIC ACCEPT decisions matched Official;
4. no false accept was observed;
5. bounded inductive/recursor/field-universe reject heuristics over-reject valid large environments and must be demoted or replaced before another fresh holdout.

Invalid conclusions:

- full Init/Std verification;
- general inductive semantic support;
- full Arena support;
- general Lean-kernel equivalence.

## Next gate

Freeze V5 as REVIEW_REQUIRED. For the next implementation:

- keep the successful V5 extractor;
- demote the bounded `inductive_structural`, `positivity`, `recursor_metadata`, and `field_universe` external-library checks from reject authority to diagnostics unless replaced by genuinely universal environment invariants;
- keep exact-AST ACCEPT rules unchanged;
- keep `name_integrity`, safety, and declaration-reachable projection checks as scoped necessary conditions;
- select a new declaration sample excluding both V4 and V5 targets;
- seal the corrected implementation before the new sample and Official oracle;
- require zero false accepts and zero false rejects on the fresh real-library slice holdout.
