# Tire System Calculator

This project compares road tire pairings using a SILCA-derived pressure model,
Bicycle Rolling Resistance test data, mounted-width estimates, road surface and
published wind-tunnel deltas.

The source is a numbered Jupyter notebook managed with `uv`. The notebook builds
a static app in `docs/` for GitHub Pages. Pyodide runs the dependency-free
Python model in the visitor's browser because GitHub Pages does not execute
server-side Python.

## Build the calculator

```bash
uv sync
uv run jupyter nbconvert \
  --execute \
  --to notebook \
  --inplace \
  analysis/0_build.ipynb
```

The executed notebook writes `docs/index.html`. A second numbered notebook runs
the deployed app in Chromium and verifies model loading, ranking output and
recalculation.

## Work in the notebook

```bash
uv run jupyter lab
```

Open `analysis/0_build.ipynb`.

## Publish

Push `main` to GitHub. The Pages workflow uploads `docs/`, publishes the static
app and then executes `analysis/1_test_pages.ipynb` against the live URL in
Chromium.

## Model boundaries

The calculator is a comparison model rather than a wind tunnel. Puncture risk,
grip, tire wear and product availability are excluded. Surface impedance and
untested tire-rim combinations are labeled as estimates.

## Sources

- [SILCA Professional Tire Pressure Calculator](https://silca.cc/pages/pro-tire-pressure-calculator)
- [Bicycle Rolling Resistance](https://www.bicyclerollingresistance.com/)
- [Parcours AERO 111 wind-tunnel testing](https://www.parcours.cc/blogs/news/continental-aero-111-wind-tunnel-testing)
- [Cyclingnews tire-width wind-tunnel testing](https://www.cyclingnews.com/features/what-is-the-fastest-tyre-width-for-road-cycling/)
- [Pyodide](https://pyodide.org/)
- [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
