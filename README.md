# Tire System Calculator

This project compares road tire pairings using a SILCA-derived pressure model,
Bicycle Rolling Resistance anchors, mounted-width estimates, road surface and
published wind-tunnel evidence. It clearly labels its own derived inputs rather
than presenting them as direct test measurements.

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
untested tire-rim combinations are labeled as estimates. Route weather supplies
air density and reports apparent-wind yaw. The present catalog uses one aero
baseline per tire, not a complete tire-and-rim curve at every yaw angle.

## Sources

- [SILCA Professional Tire Pressure Calculator](https://silca.cc/pages/pro-tire-pressure-calculator)
- [Bicycle Rolling Resistance](https://www.bicyclerollingresistance.com/)
- [Parcours 2026 yaw-resolved tire wind-tunnel testing](https://www.parcours.cc/blogs/news/aero-testing-race-tyres-2026-update)
- [Cyclingnews UCI-legal wheel test and GP5000 mounted widths](https://www.cyclingnews.com/cycling-tech-components/wheels-tyres/what-are-the-fastest-uci-legal-road-wheels-wind-tunnel-testing-the-big-name-brands-and-chinese-contenders/)
- [Cyclingnews AERO 111 yaw and rolling-resistance test](https://www.cyclingnews.com/cycling-tech-components/wheels-tyres/aero-tyre-focus/)
- [FHWA HPMS 2024 spatial data](https://data.transportation.gov/Roadways-and-Bridges/HPMS-Spatial-All-Sections-2024/42um-tgh5)
- [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)
- [Pyodide](https://pyodide.org/)
- [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
