# databricks-embed

Minimal demo: a static GitHub Pages site that iframe-embeds two
Databricks Apps running on the `trial400` workspace.

**Targets** (switchable via tab buttons; deep-linkable via `#contracts`
or `#tracker` hash):

- `Contract Intelligence` (default) — Streamlit app at
  `contract-intelligence-7474645551322247.aws.databricksapps.com`.
  Queries `contract_intelligence.gold.*` (USASpending awards) via the
  app's service principal.
- `Tracker GCC` — React + Cesium + Express app at
  `tracker-gcc-app-7474645551322247.aws.databricksapps.com`.
  Queries `gcc.gold.*` via the SQL warehouse; includes Genie/Ask-AI.

## How it works

- Both are Databricks Apps (not Lakeview dashboards). Each runs on its
  own compute and authenticates as its own service principal against
  the warehouse.
- The browser loads `index.html` from `wyms.github.io`. The `<iframe>`
  src points at the app's hosted URL.
- **Viewers must be logged into the `trial400` workspace** for the
  iframe to load — Databricks Apps require workspace auth. This demo
  is intended for internal use only.

## Live

https://wyms.github.io/databricks-embed/

## Notes

- For an embed pattern that works without a Databricks login (Genie
  chat + ad-hoc SQL via service principal token), see `public-embed/`
  in the parent [`wyms/dbxrebuild`](https://github.com/wyms/dbxrebuild)
  repo.
- Lakeview-dashboard embedding was tried initially but had reliability
  issues on trial400 (widget rendering returned "No data" despite
  queries succeeding). The Apps path is more robust.
