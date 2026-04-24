---
name: amap-lbs-skill
description: 高德地图服务 Skill
metadata:
  require-secret: true
  require-secret-description: 请输入你的高德 Web Service API Key
---

# amap-lbs-skill

一个用于调用高德地图 Web Service API 的示例 Skill。

## 输入示例

```json
{
  "keyword": "肯德基",
  "city": "北京"
}
```

## 安全说明

- API Key 必须通过 Gallery 的 secret 输入框提供。
- 不要把 API Key 放进 prompt、源码或数据输入中。
