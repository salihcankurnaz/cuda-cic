# CUDA-CIC V4.4 — Next Fragment Atlas Milestone

Frozen result ZIP SHA-256:

`ffcc8a71a5f3e80330e1337d0443a9440d587f90db38091aa322eccaf239bb6c`

Status:

`V4_4_NEXT_FRAGMENT_ATLAS_COMPLETE`

## Frozen external provenance

Lean Kernel Arena commit:

`abc55357aee17c59dfdbf39c8a2e19739e23dd10`

Frozen `tutorial/Tutorial.lean` Git blob:

`782a81685f76f4917b9189d49a7e8f5679a376dc`

The RESULT package manifest was independently recomputed: 17/17 payload files matched exact byte length and SHA-256, with no missing or extra payload files.

## Four measured Arena objects

- `good/008_forallSortWhnf.ndjson` — official Lean kernel ACCEPT — raw SHA-256 `b4af42800421f4ac5ec7e699a706bdd82f9f1324a5d2d49769fb340bf36e6a48`
- `bad/009_forallSortBad.ndjson` — official Lean kernel REJECT — raw SHA-256 `36eef2fa43e86af2d031a9cb9ec8fbd452dd7e50d3444997fe71003cc7295051`
- `bad/010_nonTypeType.ndjson` — official Lean kernel REJECT — raw SHA-256 `18cba14f24723f0325721cdd1a5699e45b61bcce7ed94f2bded0f42c848ba4c4`
- `bad/011_nonTypeAxiom.ndjson` — official Lean kernel REJECT — raw SHA-256 `687a8966b2727b26143b3340e8bead862b9057e5b4ec1ee7fc51a2a6e7211dc6`

Official expected-label agreement: **4/4**.

## Measured semantic boundary

`008_forallSortWhnf` and `009_forallSortBad` introduce the first symbolic universe parameter in the current external lane through polymorphic `id.{u}`. The actual use is `id` instantiated with concrete universe level 2, and the dependency declaration itself contains symbolic level `u`.

The exact measured requirements are:

- declaration-type well-formedness;
- polymorphic constant lookup for `id`;
- universe instantiation;
- delta/reducibility support for `id`;
- WHNF of a `ForallE` binder domain before requiring that domain to be a sort.

`010_nonTypeType` and `011_nonTypeAxiom` do not need symbolic universe support. They isolate declaration-type checking:

- a definition whose declared type is `constType` must be rejected because the declared type is not itself a type;
- an axiom with the same malformed declared type must also be rejected.

`011_nonTypeAxiom` therefore additionally requires axiom declaration support and axiom-type well-formedness checking.

There were no other unsupported expression-node kinds in this four-object atlas.

## Official checker diagnostics

- `008_forallSortWhnf`: `Accepted 2 declarations.`
- `009_forallSortBad`: kernel error `type expected` at `x`.
- `010_nonTypeType`: kernel error `type expected` at `constType`.
- `011_nonTypeAxiom`: kernel error `type expected` at `constType`.

## Claim boundary

V4.4 is a structural/provenance atlas only. It does **not** add CUDA-CIC semantic support and does not establish a new Lean-equivalence result.

Next scientific stage:

`CUDA_CIC_V4_4_1_UNIVERSE_WHNF_DECLTYPE_CORE`

The next checker should add only the measured universe-instantiation, WHNF-before-sort-check, declaration-type well-formedness, and axiom rules while preserving the previous external regression corpus.
