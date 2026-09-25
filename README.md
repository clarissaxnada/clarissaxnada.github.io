# clarissaxnada.github.io

This repository is the source for my personal website which is a [Quarto](https://quarto.org) site with a Home, About, and Blog page, published via GitHub Pages.

**Live site:** [clarissaxnada.github.io](https://clarissaxnada.github.io)

## Prerequisites

Install these before building the site:

| Tool | Version used | Notes |
|---|---|---|
| [Quarto CLI](https://quarto.org/docs/get-started/) | `1.10.18` | check with `quarto --version` |
| [`uv`](https://docs.astral.sh/uv/getting-started/installation/) | `0.12.5` | check with `uv --version` |
| R | `4.6.1` | pinned in `renv.lock` |
| Python | `3.14` | pinned in `.python-version` / `pyproject.toml`. `uv` will fetch this Python version for you if you don't already have it |

`renv` itself does **not** need to be installed manually. The first time R touches this project, `renv/activate.R` activates `renv` automatically and then installs the pinned package versions.

## Build steps (clone → built site)

Run these in order.

```bash
# 1. Clone the repo: run anywhere in terminal
git clone https://github.com/clarissaxnada/clarissaxnada.github.io.git

# 2. Move into the repo: all remaining commands are run from here
cd clarissaxnada.github.io

# 3. Install/sync Python dependencies (pandas, palmerpenguins, jupyter, ipykernel)
#    Reads .python-version, pyproject.toml and uv.lock; creates a local .venv
uv sync
```

```r
# 4. Restore R dependencies: run in R or Rscript, from the repo root
#    This is what triggers the renv bootstrap described above, then
#    installs the exact package versions recorded in renv.lock
renv::restore()
```

```bash
# 5. Render the site: run from the repo root
#    `uv run` makes sure Quarto executes the Python code chunks with the
#    uv-managed virtual environment from step 3
uv run quarto render
```

## Where the built site lands

`_quarto.yml` sets `output-dir: docs`, so rendering writes static HTML into the `docs/` folder at the repo root (this is also the folder GitHub Pages serves from).

To view it locally after rendering, open `docs/index.html` directly in a browser, e.g.:

```bash
open docs/index.html        # macOS
# or
xdg-open docs/index.html    # Linux
```

Alternatively, skip the manual open step and use Quarto's live-reload dev server instead of `quarto render`:

```bash
uv run quarto preview
```

which serves the site locally (default `http://localhost:4000`) and rebuilds on save.

## Data & Citation

The `penguins-analysis-py` and `penguins-analysis-r` blog posts use the Palmer Penguins dataset via the `palmerpenguins` package (Python and R).

Data: [Palmer Penguins](https://allisonhorst.github.io/palmerpenguins/), Palmer Station Antarctica LTER.