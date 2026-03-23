# Weather Skill（心知天气）

[Seniverse](https://www.seniverse.com) 天气查询 Skill，让大模型能够调用接口查询各类气象数据。

Seniverse 官方提供的 SKILL 工具包，你可以将它用于 Claude、OpenClaw 以及其他支持 Skills 的 AI 系统中。使 AI 可以获取企业级高精度天气数据。

### 覆盖能力（部分能力正在集成到 Skill 中）

**V3 接口（常规天气）**
- 🌤️ 天气实况 / 整点实况 / 极速实况
- 📅 未来 15 天逐日预报、未来 45 天超长预报
- 🕐 24 小时逐小时预报 / 过去 24 小时历史天气
- 💨 空气质量实况、预报、历史、城市排行
- 🧭 生活指数（穿衣、紫外线、洗车、旅游等 27 项，仅限中国）
- 🌅 日出日落 / 月出月落 / 月相
- 📅 农历节气 / 生肖 / 机动车限行
- ⚠️ 气象灾害预警（普通版 / 增量更新版 / 全量产品版）
- 🏙️ 城市搜索 / 自然语言天气查询
- 🌊 近海天气预报 / 逐小时潮汐预报

**V4 接口（高精度网格数据）**
- 🗺️ 公里级网格天气预报（中国 1km / 全球 10km）
- ⚡ 雷电实况 / 台风路径实况与预报
- 🛰️ 分钟级卫星云图
- 🌬️ 空气质量网格实况与预报
- 🌱 土壤温湿度实况与预报
- 🌊 海浪预报
- ☀️ 新能源专业气象（光伏功率预测等）
- 🔥 卫星火点监测

支持全国 **3,156 个**、全球 **14 万个**城市，支持 13 种语言返回。

---

## 如何获取 SENIVERSE_API_KEY

1. 前往心知天气官网注册账号：[https://www.seniverse.com/signup](https://www.seniverse.com/signup)
2. 注册后登录控制台：[https://www.seniverse.com/dashboard](https://www.seniverse.com/dashboard)
3. 在「我的API产品」中找到你的 **API 密钥（Key）**，新注册用户可以申请 14 天全接口免费试用
4. 配置环境变量。以 mac 为例，编辑 `~/.zchrc`，加入：`export SENIVERSE_API_KEY="your_api_key_here"`
5. 以 openclaw（龙虾）配置：在 `~/.openclaw` 中运行 `npx skills add seniverse/skills`。如果 `openclaw skills list` 可以看到 weather 工具，显示心知科技字样，则说明安装成功。

---

## API 版本说明

| 版本 | Base URL                       | 定位 |
|------|--------------------------------|------|
| **V3** | `https://api.seniverse.com/v3` | 城市级数据 |
| **V4** | `https://api.seniverse.com/v4` | 网格级高精度数据 |

---

## 快速示例

```bash
# 查询北京天气实况（V3）
curl "https://api.seniverse.com/v3/weather/now.json?key=YOUR_KEY&location=beijing&language=zh-Hans&unit=c"
```

---

## 相关链接

- 官网：[https://www.seniverse.com/](https://www.seniverse.com/)
- 语雀 API V3 文档：[https://seniverse.yuque.com/hyper_data/api_v3](https://seniverse.yuque.com/hyper_data/api_v3)
- 语雀 API V4 文档：[https://seniverse.yuque.com/hyper_data/api_v4](https://seniverse.yuque.com/hyper_data/api_v4)
- 示例代码（GitHub）：[https://github.com/seniverse/seniverse-api-demos](https://github.com/seniverse/seniverse-api-demos)