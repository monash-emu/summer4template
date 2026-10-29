# summer4template

A small pixi template for [summer4](https://github.com/monash-emu/summer4) projects.

`notebooks/01-Example.ipynb` builds an age-stratified SIR model, runs it, makes
synthetic weekly observations from it, and calibrates the two parameters with NUTS.

```bash
pixi install
```

Then open the notebook with the `default` environment's kernel
(`.pixi/envs/default/bin/python`).

summer4 is pinned to a commit in `pixi.toml` (currently `v0.2.0a6`). To move to a
newer summer4, change `rev` there and run `pixi update summer4`.

Put your own code in `src/example_project` (installed in editable mode), and
rename it to suit.
