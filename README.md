# makefun-sitegen-fast

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/oraybora-source/makefun-sitegen-fast/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/oraybora-source/makefun-sitegen-fast/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0: `solve.js` answers
exactly as makefun-site does on every case — the same output tree, byte for
byte — with less CPU time. Written from scratch in this session from the
kit's reference code as the behaviour specification.

## Run it

```sh
node main.ts
```

`main.ts` (Node 22) reads every case from `/input/cases.json` (or
`$MAKEFUN_INPUT_DIR`), answers each one alone with `run()` from `solve.js`,
and writes `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR`). No
dependencies, no network, no clock, no randomness: the output is a function
of the input alone.

## How it is faster

- Markdown renders in one pass over each source's lines: no token array, no
  second split of the body, and blocks are classified by their first
  character instead of a battery of regexes.
- Inline rendering scans for the next special character with one regular
  expression, so plain runs are copied whole instead of escaped one
  character at a time.
- `slugify` takes an ASCII fast path (NFKD is the identity on ASCII); the
  slow path is the reference's own.
- Word counting and template rendering avoid per-element closures and
  per-character regex calls.

---

<sub>Entered on [make.fun](https://make.fun/?ref=oraybora-source&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
