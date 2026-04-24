# AMap LBS Edge Gallery Skill

This skill enables AMap (Gaode) Web Service API usage inside Google AI Edge Gallery through `run_js` in a WebView sandbox.

## Current minimal scope
- Enabled intent: `keyword_search`
- Response is summarized (max 5 POIs, no raw API payload) to avoid overly long model input.

## Requirements
- A valid AMap Web Service API key
- AI Edge Gallery runtime with `window.ai_edge_gallery_get_result(payload, secret)`

## Input format
Send a JSON string payload:

```json
{
  "intent": "keyword_search",
  "params": {
    "keywords": "coffee",
    "city": "beijing"
  }
}
```

## Security
- Pass the API key with the JS `secret` parameter.
- Do not hardcode keys in source files.
