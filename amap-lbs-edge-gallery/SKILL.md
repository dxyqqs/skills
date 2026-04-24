---
name: amap-lbs-edge-gallery
description: Use this skill to call AMap (Gaode) Web Service APIs from Google AI Edge Gallery via run_js in a WebView sandbox. Supports keyword_search, nearby_search, route_planning, and heatmap generation without Node.js dependencies.
metadata:
  require-secret: true
  require-secret-description: 请输入高德 Web Service API Key
---

# AMap LBS Skill for AI Edge Gallery

## Goal
Execute AMap LBS capabilities in AI Edge Gallery's JavaScript runtime (hidden WebView) through `run_js`.

## Runtime constraints
- Do not use Node.js APIs (`require`, `fs`, `process`, `child_process`).
- Use browser APIs only (`fetch`, `URLSearchParams`, Web APIs).
- Return `JSON.stringify({ result })` on success.
- Return `JSON.stringify({ error })` on failure.

## Inputs
Provide a JSON string payload to `window.ai_edge_gallery_get_result(payload, secret)`.

Payload shape:
```json
{
  "intent": "keyword_search | nearby_search | route_planning | heatmap",
  "params": {}
}
```

## Supported intents

### 1) keyword_search
`params`:
- `keywords` (required)
- `city` (optional)
- `offset` (optional, default 20)
- `page` (optional, default 1)
- `types` (optional)

### 2) nearby_search
`params`:
- `location` (required, `lng,lat`)
- `radius` (optional, meters, default 3000)
- `keywords` (optional)
- `types` (optional)
- `sortrule` (optional, `distance` or `weight`)
- `offset` (optional, default 20)
- `page` (optional, default 1)

### 3) route_planning
`params`:
- `origin` (required, `lng,lat`)
- `destination` (required, `lng,lat`)
- `mode` (optional, `driving | walking | bicycling`, default `driving`)
- `strategy` (optional, driving strategy)

### 4) heatmap
`params`:
- `location` (required, `lng,lat`)
- `radius` (optional, default 5000)
- `keywords` (optional)
- `types` (optional)
- `pages` (optional, default 3)
- `offset` (optional, default 25)

Returns normalized `points` compatible with most heatmap renderers:
```json
[{ "lng": 116.397, "lat": 39.908, "weight": 1 }]
```

## Secret handling
Store the AMap key as a Gallery secret and pass it through the JS runtime `secret` parameter. Never hardcode the key in source files.

## Example run_js call pattern
```javascript
const payload = JSON.stringify({
  intent: "nearby_search",
  params: {
    location: "116.397428,39.90923",
    radius: 2000,
    keywords: "coffee",
    page: 1
  }
});

return await window.ai_edge_gallery_get_result(payload, secret);
```
