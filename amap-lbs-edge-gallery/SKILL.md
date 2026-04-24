---
name: amap-lbs-edge-gallery
description: AMap keyword POI search skill with compact summaries.
metadata:
  require-secret: true
  require-secret-description: Enter AMap Web Service API Key
---

Call `run_js` with:
- script: `index.html`
- data: JSON string:
  - intent: `keyword_search`
  - params: object

Use `keyword_search` for place search.
`nearby_search` and `route_planning` are not enabled in this minimal build.

Do not include API keys in data. The key is provided as `secret`.
