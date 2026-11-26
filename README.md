# summer4template

A small pixi template for [summer4](https://github.com/monash-emu/summer4) projects.

`notebooks/01-Example.ipynb` builds an age-stratified SIR model, runs it, makes
synthetic weekly observations from it, and calibrates the two parameters with NUTS.

To install the pixi environment exactly as specified and tested;
```bash
pixi install --locked
```

Or to use the latest (valid) package versions
```bash
pixi install
```

Then open the notebook with the `default` environment's kernel
(`.pixi/envs/default/bin/python` on macOS and Linux, `.pixi\envs\default\python.exe` on
Windows). Works on macOS (Apple silicon), Linux and Windows (x86_64, CPU only; JAX's
Windows wheels are labelled experimental, and WSL2 is the route if you need a GPU).
CI runs `pixi run check` on all three.

| Command | What it does |
|---|---|
| `pixi run check` | run the tests, then every notebook headless |
| `pixi run api NAME` | show the installed summer4's documentation for `NAME` (`pixi run api` lists everything) |
| `pixi run clear-notebooks` | clear notebook outputs before committing |

[`docs/summer4-guide.md`](docs/summer4-guide.md) is a tested, version-specific guide to
summer4: compartments, flows, infection, results and calibration, plus the common
pitfalls and a summer2/summer3 translation table.

summer4 is pinned to a release tag in `pixi.toml` (currently `v0.3.0a6`). To move to a
newer summer4, change `tag` there, run `pixi update summer4`, update the guide, and run
`pixi run check`.

### JAX version

JAX is pinned to the 0.6 series in `pixi.toml` (`jax` and `jaxlib` `>=0.6,<0.7`, with
`diffrax` `>=0.7.2,<0.8` and `numpyro` `>=0.18,<0.19`). These are the same constraints as
summer4's own CI environment (the `jax06` feature of its `pixi.toml`), the series summer4
develops and tests on. `pixi.lock` is committed, so every new project installs the same,
tested set of packages. summer4 itself only asks for `jax>=0.6.0`, so without the pin
pixi would pick the newest JAX, which summer4 has not been tested against (JAX 0.12, for
example, breaks NUTS with `chain_method="parallel"` and a diffrax solver such as
`solver="tsit5"`). To move JAX, change the `jax`, `jaxlib`, `diffrax` and `numpyro` pins
in `pixi.toml`, run `pixi update jax jaxlib diffrax numpyro`, then `pixi run check`.

Put your own code in `src/example_project` (installed in editable mode), and
rename it to suit.

## Coding agents

The project is set up for coding agents that have never seen summer4.
[`AGENTS.md`](AGENTS.md) is the entry point (read natively by Codex, Cursor, Copilot,
Jules and others; `CLAUDE.md`, `GEMINI.md` and `.github/copilot-instructions.md` point to
it). It sends agents to the guide, to `pixi run api` for anything else, and to
`pixi run check` to verify their work. Claude Code also gets a `summer4-model` skill
(`.claude/skills/`) with a step-by-step checklist for model work.
