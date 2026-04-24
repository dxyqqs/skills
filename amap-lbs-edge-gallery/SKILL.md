---
name: amap-lbs-edge-gallery
description: Use this skill to call AMap (Gaode) Web Service APIs from Google AI Edge Gallery via run_js in a WebView sandbox. Minimal rollout currently supports keyword_search only.
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
  "intent": "keyword_search",
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

## Rollout plan (restore in order)
After single-function stabilization, restore intents in this exact order:

1. `nearby_search`
2. `route_planning`
3. `heatmap`

For each restored intent, keep the same guardrails:
- return summary-oriented payloads;
- enforce an explicit item count cap (`offset`/result limit).

## Secret handling
Store the AMap key as a Gallery secret and pass it through the JS runtime `secret` parameter. Never hardcode the key in source files.

## Example run_js call pattern
```javascript
const payload = JSON.stringify({
  intent: "keyword_search",
  params: {
    keywords: "coffee",
    city: "beijing",
    offset: 10,
    page: 1
  }
});

return await window.ai_edge_gallery_get_result(payload, secret);
```

Unsupported intents currently return:
```text
Unsupported intent during minimal rollout: <intent>
```
