---
name: amap-lbs-edge-gallery
description: 在 AI Edge Gallery 中通过 run_js 调用 AMap Web Service API。
metadata:
  require-secret: true
  require-secret-description: 请输入高德 Web Service API Key
---

# amap-lbs-edge-gallery

## 调用入口
- 使用 `run_js`，入口文件为 `scripts/index.html`。

## data 最小 schema
```json
{
  "intent": "keyword_search",
  "params": {}
}
```

## 允许的 intent
- `keyword_search`

## Secret 规则
- 不要在 `data` 中传 `key`，`key` 由 secret 注入。
