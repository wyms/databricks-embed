# databricks-embed

Minimal demo: a static GitHub Pages site with three switchable tabs,
all backed by the `trial400` Databricks workspace.

**Targets** (deep-linkable via `#cost`, `#tracker`, `#contracts`):

- `Cost Overview` (default) — Lakeview AI/BI dashboard published with
  `embed_credentials: true`. Renders anonymously (no Databricks login
  required) provided `wyms.github.io` is on the workspace's
  approved-domains list. Sourced from `system.billing.usage` and
  `system.billing.list_prices`.
- `Tracker GCC` — Databricks App (Node + Express + React/Cesium SPA).
  **Requires login** to the trial400 workspace; each app subdomain
  has its own auth cookie.
- `Contract Intelligence` — Databricks App (Streamlit). **Requires
  login**. Queries `contract_intelligence.gold.*` (USASpending awards).

## How it works

- The browser loads `index.html` from `wyms.github.io`. The `<iframe>`
  src points at the trial400 workspace (Lakeview embed URL for Cost,
  app subdomains for Tracker and Contract Intelligence).
- For the **Cost** tab, `embed_credentials: true` means dashboard
  queries run with the publisher's data permissions, not the viewer's.
- For the **App** tabs, viewers must first log into the trial400
  workspace. Because each app runs on its own subdomain, you may need
  to visit each app URL once directly to establish a session before
  the iframe can render it.

## Live

https://wyms.github.io/databricks-embed/

## Notes

- For an anonymous Genie chat + ad-hoc SQL flow via a service
  principal token, see `public-embed/` in the parent
  [`wyms/dbxrebuild`](https://github.com/wyms/dbxrebuild) repo.
