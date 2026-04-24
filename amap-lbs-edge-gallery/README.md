# AMap LBS Edge Gallery Skill

This skill enables AMap (Gaode) Web Service API usage inside Google AI Edge Gallery through `run_js` in a WebView sandbox.

## Features
- Keyword POI search (`keyword_search`)
- Nearby POI search (`nearby_search`)
- Route planning (`route_planning`)
- Heatmap point generation (`heatmap`)

## Requirements
- A valid AMap Web Service API key
- AI Edge Gallery runtime with `window.ai_edge_gallery_get_result(payload, secret)`

## Input format
Send a JSON string payload:

```json
{
  "intent": "keyword_search | nearby_search | route_planning | heatmap",
  "params": {}
}
```

## Security
- Enable secret input in the skill metadata and pass the key with the JS `secret` parameter.
- Do not hardcode keys in source files.
