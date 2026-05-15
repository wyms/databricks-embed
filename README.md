# databricks-embed

Minimal demo: a static GitHub Pages site that iframe-embeds a published
Databricks AI/BI dashboard (`Contract Intelligence Platform — v3`).

## How it works

- The dashboard is published with `embed_credentials: true`, so queries
  run as the publisher (not the viewer). The viewer needs **no Databricks
  login**.
- The browser loads `index.html` from `wyms.github.io`. The `<iframe>`
  src points directly at the workspace's `/embed/dashboardsv3/<id>` route.
- For the iframe to render, this Pages origin must be on the workspace's
  **Allowed domains** allowlist (Settings → Security → Embedded content).

## Live

https://wyms.github.io/databricks-embed/

## Limits

- Embed-credentials mode means the dashboard data is whatever the
  publisher account can see. The gold tables here are aggregate / no PII.
- Genie chat and ad-hoc query are **not** in this demo — those require a
  service-principal proxy. See `public-embed/` in the parent
  `dbxrebuilt` repo for that scaffold.
