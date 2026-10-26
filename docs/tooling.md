# Tools and libraries

## Current phase: source feasibility review

This phase is a research/design scaffold; it has not estimated any market response.

- Primary-source documentation was reviewed through the web browser.
- The public World Bank GEM Excel bundle was downloaded and its stock-market workbook inspected locally to confirm the available annual and monthly tabs.
- PowerShell was used for source retrieval and file inspection; Python with `openpyxl` was used to inspect the workbook structure.
- Git will record the project history. No analysis code, notebook, or empirical output is included yet.

## Planned analysis stack (not yet used for findings)

After the daily market source set and data rights are confirmed, the likely stack is:

- Python for data acquisition and analysis.
- `pandas` and `numpy` for tabular transformations and return calculations.
- `scipy` and `statsmodels` for statistical inference and regression/event-study estimates.
- `matplotlib` for static, publication-ready figures.
- `openpyxl` and `pyarrow` where source workbooks and Parquet outputs require them.
- Jupyter notebooks for exploratory work only; the final pipeline should also run from documented scripts with a locked environment.

These are proposed tools, not a record of completed analysis. Exact versions, operating system, commands, source hashes, and environment lock file will be added when the pipeline is implemented. Dependencies will be selected based on the confirmed source formats and maintained within this repository.

