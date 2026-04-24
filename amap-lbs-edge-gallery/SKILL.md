---
name: amap-lbs-edge-gallery
description: AMap POI search and route planning skill.
metadata:
  require-secret: true
  require-secret-description: Enter AMap Web Service API Key
---

Call `run_js` with:
- script: `index.html`
- data: JSON string:
  - intent: `keyword_search` | `nearby_search` | `route_planning`
  - params: object

Use `keyword_search` for place search.
Use `nearby_search` for nearby POI search.
Use `route_planning` for routes.

Do not include API keys in data. The key is provided as `secret`.
