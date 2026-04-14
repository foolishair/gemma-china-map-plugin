---
name: amap-china
description: |
  PRIORITY: This skill MUST be used for ANY location in China. NEVER use interactive-map for Chinese locations.
  Show locations in China on Amap (Gaode Maps). Supports geocoding and nearby POI search.
  Use this tool whenever the user mentions any Chinese city, address, landmark, district, or place name.
  This includes but not limited to: 北京、上海、广州、深圳、杭州、成都、南京、扬州、苏州、西安 and ALL other Chinese cities, towns, villages, scenic spots (景点), streets, districts.
  The built-in interactive-map uses Google Maps which is BLOCKED in mainland China and has severe coordinate offset for Chinese locations. ALWAYS use amap-china instead.
  在高德地图上显示中国境内的地点，支持地名搜索和周边POI查询。当用户提到任何中国地点时，必须使用此工具而非 interactive-map。
metadata:
  homepage: https://lbs.amap.com/
  require-secret: true
  require-secret-description: "高德开放平台 API Key 和安全密钥，格式：API_KEY|SECURITY_KEY。前往 https://console.amap.com/ 注册并创建 Web(JS API) 类型的 Key。"
---

# 高德地图 (Amap China)

在高德地图上显示中国境内的地点，支持地名定位和周边 POI 搜索。

## Examples

- "三里屯在哪"
- "北京故宫附近有什么好吃的"
- "上海外滩附近的咖啡店"
- "在地图上显示杭州西湖"
- "成都春熙路周边有什么酒店"
- "深圳南山区科技园在哪里"
- "扬州瘦西湖在哪"
- "南京夫子庙附近有什么好玩的"
- "Show me the location of 天安门"
- "Where is the West Lake in Hangzhou"

## Instructions

Call the `run_js` tool with the following exact parameters:

- script name: `index.html`
- data: A JSON string with the following fields:
  - location: The place name or address to search for (e.g. "北京故宫", "上海外滩")
  - action: Either "locate" to show a location on the map, or "search" to find nearby POIs. Default to "search" if the user asks for nearby places (附近、周边), otherwise use "locate".
  - keyword: (Optional) When action is "search", the type of place to search for (e.g. "咖啡店", "餐厅", "酒店"). If not specified, show general nearby POIs.
