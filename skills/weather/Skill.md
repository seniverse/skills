---
name: weather
description: 使用心知天气（Seniverse）HyperData API 查询实时天气、天气预报、空气质量、生活指数、日出日落、城市搜索、网格天气、台风、雷电等气象数据。当用户询问天气、气温、空气质量、穿衣建议、下雨概率、风速、紫外线、日出日落、农历节气、台风、雷电、潮汐等任何与天气或气象相关的问题时，必须使用此 skill。即使用户只是随口问"今天热吗""要带伞吗""明天适合出去玩吗"，也应触发此 skill。
---

# Weather Skill — 心知天气 HyperData API

## 认证方式

```
https://api.seniverse.com/v3/{path}.json?key=SENIVERSE_API_KEY&location=beijing&...
```

1. API Key 从环境变量 `SENIVERSE_API_KEY` 读取。
2. 如果没有设置环境变量，可以向用户询问后写入配置文件（如 `~/.zchrc` 或 `~/.openclaw/config.yml`）。
3. 如果用户还没有 `SENIVERSE_API_KEY`，请让用户前往 `https://www.seniverse.com` 注册账号并获取 API Key。

---

## 通用参数（V3）

| 参数 | 说明 | 示例值 |
|------|------|--------|
| `location` | 城市（支持城市ID、中文名、英文名、拼音、`纬度:经度`、IP地址、`ip`自动识别） | `beijing` / `39.93:116.40` / `ip` |
| `language` | 返回语言，默认 `zh-Hans` | `zh-Hans` / `en` / `ja` 等13种 |
| `unit` | 温度单位，默认 `c` | `c`（摄氏）/ `f`（华氏） |
| `start` | 起始时间，默认 `0`（今天） | `-1`昨天 / `0`今天 / `1`明天 |

---

## V3 接口列表

| 接口名称             | 说明                                                         | 示例                                                                                                                                                                       |
|------------------|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 天气实况             | 获取指定城市的天气实况                                                | https://api.seniverse.com/v3/weather/now.json?key=your_api_key&location=beijing&language=zh-Hans&unit=c                                                                  |
| 整点实况             | 获取全国所有市区县（3000+）的天气实况数据                                    | https://api.seniverse.com/v3/weather/station/now.json?key=YOUR_PRIVATE_KEY&location=城市ID&language=zh-Hans&unit=c                                                         |
| 24小时逐小时天气预报      | 获取指定城市未来最多24小时的逐小时天气预报，支持全球城市                              | https://api.seniverse.com/v3/weather/hourly.json?key=your_api_key&location=beijing&language=zh-Hans&unit=c&start=0&hours=24                                              |
| 过去24小时历史天气       | 获取指定城市过去24小时逐小时的历史天气                                       | https://api.seniverse.com/v3/weather/hourly_history.json?key=your_api_key&location=seattle&language=zh-Hans&unit=c                                                       |
| 未来15天逐日天气预报和昨日天气 | 获取指定城市未来最多 15 天每天的白天和夜间预报，以及昨日的历史天气                        | https://api.seniverse.com/v3/weather/daily.json?key=your_api_key&location=beijing&language=zh-Hans&unit=c&start=0&days=5                                                 |
| 气象灾害预警           | 获取当前所有城市或指定城市的气象灾害预警信息                                     | https://api.seniverse.com/v3/weather/alarm.json?key=your_api_key&location=beijing&detail=more                                                                            |
| 空气质量实况           | 获取指定城市的AQI、PM2.5、PM10、一氧化碳、二氧化氮、臭氧等空气质量信息                  | https://api.seniverse.com/v3/air/now.json?key=your_api_key&location=beijing&language=zh-Hans&scope=city                                                                  |
| 过去24小时历史空气质量     | 获取指定城市过去24小时逐小时的AQI、PM2.5、PM10、一氧化碳、二氧化氮、臭氧等空气质量信息         | https://api.seniverse.com/v3/air/hourly_history.json?key=your_api_key&location=beijing&language=zh-Hans&scope=city                                                       |
| 逐小时空气质量预报        | 获取指定城市未来最多5天的逐小时AQI预报                                      | https://api.seniverse.com/v3/air/hourly.json?key=your_api_key&language=zh-Hans&location=Beijing                                                                          |
| 生活指数             | 获取指定城市的基本、交通、生活、运动、健康 5 大类共 27 项生活指数                       | https://api.seniverse.com/v3/life/suggestion.json?key=your_api_key&location=shanghai&language=zh-Hans&days=5                                                             |
| 城市搜索             | 根据城市ID、中文、英文、拼音、IP、经纬度搜索匹配的城市                              | https://api.seniverse.com/v3/location/search.json?key=your_api_key&q={q} 其中 q 可以是 id：WX4FBXXFKE4F、中文：北京、拼音：beijing、拼音首字母：bj、IP地址：220.181.111.86、经纬度：39.93:116.40、省市：辽宁朝阳 |
| 自然语言天气查询                 | 理解自然语言请求，返回自然语言的回答及结构化的天气数据，方便智能硬件等实现基于语音请求的天气查询（传统机器学习算法） | https://api.seniverse.com/v3/robot/talk.json?key=your_api_key&q=北京明天天气怎么样？                                                                                                                                                                         |

## 天气现象说明

| 代码 | 中文 | 英文 | 图标 |
| --- | --- | --- | --- |
| 0 | 晴（国内城市白天晴） | Sunny |  |
| 1 | 晴（国内城市夜晚晴） | Clear |  |
| 2 | 晴（国外城市白天晴） | Fair |  |
| 3 | 晴（国外城市夜晚晴） | Fair |  |
| 4 | 多云 | Cloudy |  |
| 5 | 晴间多云 | Partly Cloudy |  |
| 6 | 晴间多云 | Partly Cloudy |  |
| 7 | 大部多云 | Mostly Cloudy |  |
| 8 | 大部多云 | Mostly Cloudy |  |
| 9 | 阴 | Overcast |  |
| 10 | 阵雨 | Shower |  |
| 11 | 雷阵雨 | Thundershower |  |
| 12 | 雷阵雨伴有冰雹 | Thundershower with Hail |  |
| 13 | 小雨 | Light Rain |  |
| 14 | 中雨 | Moderate Rain |  |
| 15 | 大雨 | Heavy Rain |  |
| 16 | 暴雨 | Storm |  |
| 17 | 大暴雨 | Heavy Storm |  |
| 18 | 特大暴雨 | Severe Storm |  |
| 19 | 冻雨 | Ice Rain |  |
| 20 | 雨夹雪 | Sleet |  |
| 21 | 阵雪 | Snow Flurry |  |
| 22 | 小雪 | Light Snow |  |
| 23 | 中雪 | Moderate Snow |  |
| 24 | 大雪 | Heavy Snow |  |
| 25 | 暴雪 | Snowstorm |  |
| 26 | 浮尘 | Dust |  |
| 27 | 扬沙 | Sand |  |
| 28 | 沙尘暴 | Duststorm |  |
| 29 | 强沙尘暴 | Sandstorm |  |
| 30 | 雾 | Foggy |  |
| 31 | 霾 | Haze |  |
| 32 | 风 | Windy |  |
| 33 | 大风 | Blustery |  |
| 34 | 飓风 | Hurricane |  |
| 35 | 热带风暴 | Tropical Storm |  |
| 36 | 龙卷风 | Tornado |  |
| 37 | 冷 | Cold |  |
| 38 | 热 | Hot |  |
| 99 | 未知 | Unknown |  |

---

## 错误处理

- V3 错误码：通过 HTTP 状态码 + 响应体中 `status` 和 `status_code` 字段判断

可能出现的 status_code 说明如下：

| 心知状态码 status_code   | HTTP 状态码 | 说明 |
|----------| --- | --- |
| AP010001 | 403 | API 请求参数错误。 |
| AP010002 | 403 | 没有权限访问这个 API 接口。[在此查看你有权访问的 API 接口](https://seniverse.yuque.com/hyper_data/api_v3/ru2kzugbxi18g60d) |
| AP010003 | 403 | API 密钥 key 错误。 |
| AP010004 | 403 | 签名错误。 |
| AP010005 | 404 | 你请求的 API 不存在。 |
| AP010006 | 403 | 没有权限访问这个地点。 |
| AP010007 | 403 | JSONP 请求需要使用签名验证方式。 |
| AP010008 | 403 | 没有绑定域名。请在 [控制台](https://www.seniverse.com/dashboard) 对应的产品管理下进行域名绑定。 |
| AP010009 | 403 | API 请求的 user-agent 与你设置的不一致。 |
| AP010010 | 404 | 没有这个地点。 |
| AP010011 | 404 | 无法查找到指定 IP 地址对应的城市。 |
| AP010012 | 403 | 你的服务已经过期。在此 [续费](https://www.seniverse.com/dashboard) |
| AP010013 | 403 | 访问量余额不足。在此 [购买](https://www.seniverse.com/dashboard) |
| AP010014 | 403 | 访问频率超过限制。 |
| AP010015 | 404 | 暂不支持该城市的车辆限行信息。 |
| AP010016 | 500 | 暂不支持该城市的潮汐数据。 |
| AP010017 | 404 | 请求的坐标超出支持的范围。 |
| AP100001 | 404 | 系统内部错误：数据缺失。 |
| AP100002 | 500 | 系统内部错误：数据错误。 |
| AP100003 | 500 | 系统内部错误：服务内部错误。 |
| AP100004 | 500 | 系统内部错误：网关错误。 |

注意：

1. 当返回码表示需要用户购买或操作的情况，可以引导用户前往控制台 https://www.seniverse.com/dashboard 进行操作（获取 API、购买服务、续费、增加访问量、配置），如果还是不能操作，可以联系 400-022-5889
2. 如果找不到城市可以通过城市搜索查询重试一次
