# Infectious disease discussion meeting 13.09.24

## Next release
- [ ] Read up on release cycle
Blast vs DFS (IP - immunogenicity includes distances from self).

Fast DFS implementation.
What can we run.

Normalize binding affinity from 0 to 1.
We now have 0-255k (nanomolar concentration).
Alex has a function to normalize the binding score already.
Add a columnt to all_predictions with normalized binding score.
Meet with Alex. Add a jira task to the ID-294 to this as a sub issue.
Alex wants to add it somewhere other than all predictions.
- Look at good_binder, we have a condition for determining if a thing is belo 400 or 500 nM. Add extra columns.
- [] Set up meeting with Alex
- [ ] Add columns with normalized binding scores

Neural GK is missing.
- [ ] Talk with Youness why is he missing neural GK in his output?
- [ ] Research if RESERT is included, I think it is in the next model release


Tools where we have to think like population coverage estimator.
Or vaccine element set selector.
We need to subset the elements before. 
Then it is a tool.

Population coverage estimator uses representative sequence.
Program with Hanna. Update in status meeting.


## reporting module
A notebook with the plot and code to plot.
You can generate individual plots.
Or the full report.

NGSA and NIP have report modules, look at them.

A high level explanation of the files and modules that have been run.

A streamlit notebook where you can explore the result for all sequences?
A pdf to.

## Benchmarking indit
Youness' report is useful for benchmarking indit. 
We can use this work during model upgrades.
And we can have this as a benchmarking module that runs with indit to tell how indit performs
on some tasks.

## Local docker images
Hanna does not want to re-pull the docker images because it is slower.


## uv in indit
- add compatibility with old requiremetns.txt flow
- test with linux sub system for windows

uv sells themselves wi
uv highlights:
https://docs.astral.sh/uv/
```
Highlights
🚀 A single tool to replace pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more.
⚡️ 10-100x faster than pip.
🐍 Installs and manages Python versions.
🛠️ Runs and installs Python applications.
❇️ Runs scripts, with support for inline dependency metadata.
🗂️ Provides comprehensive project management, with a universal lockfile.
🔩 Includes a pip-compatible interface for a performance boost with a familiar CLI.
🏢 Supports Cargo-style workspaces for scalable projects.
💾 Disk-space efficient, with a global cache for dependency deduplication.
⏬ Installable without Rust or Python via curl or pip.
🖥️ Supports macOS, Linux, and Windows.
uv is backed by Astral, the creators of Ruff.
```

Install should be a one liner `curl -LsSf https://astral.sh/uv/install.sh | sh`

Uv creates virtual environment by default.

After that we can use:
* `uv add package-name` to add a depedency
* `uv run indit` easiest is to prefix python commands with uv
* `source .venv/bin/activate && indit --help` but the venv can be activated and use like we do now too
* `make install`, `make dev`, `make test` will still work
* `make update-requirements` becomes obsolete, but will still work if you prefer adding dependencies by editing `pyproject.toml` manually

Breaking changes
* Requires indit users install uv
* `/indit/venv` will move to `/indit/.venv`
* lockfiles move from `requirements.txt` and `requirements-dev.txt` to a single `uv.lock`

## Local docker images
We could have an option in the settings to use your own image tag?
Now we specify a docker image url in the constants
```python
class DockerImage(Enum):
    PEPTIDE_SCORER_IMAGE = "gcr.io/genuine-sector-223709/covid-mutant:0.0.5"
    PEPTIDE_SCORE_AGGREGATOR_IMAGE = "gcr.io/genuine-sector-223709/covid-mutant:0.0.5"
    HOTSPOT_DETECTOR_IMAGE = "gcr.io/genuine-sector-223709/peak-calling:0.1.6"
    HOTSPOT_CLUSTERER_IMAGE = "gcr.io/genuine-sector-223709/hotspot-clustering:v0.1.1"
    HOTSPOT_EPITOPES_SCORER_IMAGE = "score-epitopes:local"
    HLA_POPULATION_SIMULATOR_IMAGE = (
        "gcr.io/genuine-sector-223709/hla-population-modeling:1.4.1"
    )
    POPULATION_COVERAGE_ESTIMATOR_IMAGE = (
        "gcr.io/genuine-sector-223709/population-coverage-estimator:v0.0.1"
    )
    RNN_IMAGE = "gcr.io/genuine-sector-223709/neunethlabind:v1.1.2"
    AMB_IMAGE = "gcr.io/genuine-sector-223709/antigen-prediction:v1.6.0.dev2"
```