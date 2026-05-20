# databricks-embed

Minimal demo: a static GitHub Pages site that iframe-embeds a published
Databricks AI/BI dashboard.

**Targets** (switchable via tab buttons; deep-linkable via `#cost`
or `#contracts` hash):

- `Cost Overview` (default) — flexion-may workspace cost/usage
  dashboard sourced from `system.billing.usage` and
  `system.billing.list_prices`.
- `Contract Intelligence Platform — v3` — federal contract
  analytics dashboard sourced from `contract_intelligence.gold.*`
  (USASpending awards data) on the trial400 workspace.

Both dashboards are published with `embed_credentials: true`. Both
workspaces have `wyms.github.io` on their approved-domains list.

## How it works

- The dashboard is published with `embed_credentials: true`, so queries
  run as the publisher (not the viewer). The viewer needs **no
  Databricks login**.
- The browser loads `index.html` from `wyms.github.io`. The `<iframe>`
  src points at the workspace's `/embed/dashboardsv3/<id>` route.
- The workspace has `wyms.github.io` on its **Approved domains** list
  (Workspace admin → Security → External access → Embed dashboards
  and Genie spaces).

## Live

https://wyms.github.io/databricks-embed/

## Notes

- `embed_credentials: true` means the dashboard's queries run with the
  publisher's data permissions, not the viewer's. The USASpending data
  is public federal contract data; the billing data is workspace-scoped
  operational metrics. Neither is PII.
- For the Genie chat / ad-hoc SQL path (which needs a service
  principal), see `public-embed/` in the parent
  [`wyms/dbxrebuild`](https://github.com/wyms/dbxrebuild) repo.
