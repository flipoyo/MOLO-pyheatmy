# pyheatmy

Direct model of heat and water transport through a 1D riverbed sediment column, part of the MOLONARI project.

`pyheatmy` is built around the `Column` class (`pyheatmy/core.py`): a column of sediment layers between the river
and the aquifer, with the pressure and temperature measurements of a MOLONARI device. It computes the transient
head and temperature profiles. A `Layer` holds the physical parameters of a layer (`IntrinK` in m2, `n`,
`lambda_s`, `rhos_cs`, `q_s`).

`Column.simulate` is the direct model as a function of the layer parameters: it takes one mapping of parameter
names to values per layer, leaves the column unchanged and returns the temperatures at the inner sensors
(`"sensors"`, comparable with `Column.get_measured_temperatures()`) and the temperatures and specific flows of
every cell (`"temperatures"`, `"flows"`). An estimation of the parameters uses it as its model: the MCMC of
[MOLO-bayesian](https://github.com/flipoyo/MOLO-bayesian) does, without
`pyheatmy` and `bayesian_inversion` importing each other.

## Installation and tests

With [pixi](https://pixi.sh), in this repository:

```sh
pixi install       # Python, the dependencies and pyheatmy in editable mode
pixi run test      # the tests of pyheatmy
```

`pixi run -e py310 test` and `pixi run -e py313 test` run them with the oldest and the newest Python supported, as
GitHub Actions does at every push. Within the [MOLONARI-computo](https://github.com/flipoyo/MOLONARI-computo) tree,
`pixi install` at the root of the tree installs `pyheatmy` together with the other packages, and `pixi run test-all`
runs all their tests.

## Tutorials

The tutorials (generation of synthetic data, inversion) are in
[MOLO-tuto-cmpt](https://github.com/flipoyo/MOLO-tuto-cmpt).

## Versioning

The version follows [SemVer](https://semver.org). `[workspace] version` in `pixi.toml` is the reference;
`scripts/bump_version.py`, the same in every repository of the MOLONARI-computo tree, writes it into every file that
mirrors it (`pyproject.toml`, `pyheatmy/__init__.py`):

```sh
pixi run bump-version minor --dry-run   # print the plan, write nothing
pixi run bump-version patch             # or minor, major; --stage rc adds a pre-release label
pixi run check-version                  # every mirror holds the version of pixi.toml (checked by GitHub Actions)
```

## LLM assistance

Parts of this repository (its pixi environment and this README) were written with the help of large language
models, mainly Claude (Anthropic) with Claude Code, used as a paid service under the direction of the project
manager, Nicolas Flipo. They are acknowledged here rather than credited as co-authors.
