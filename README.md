# aylambmap · 零 Key 的纯地图

> 一个只做三件事的网页地图：**显示地图 · 定位我在哪 · 搜索 / 点选反查地址**。
> 不导航、不画路线、不接路由引擎、**不需要任何 API Key**。

🌐 **在线体验**：<https://aylambmap.surge.sh/>

---

## ✨ 功能

- **🗺 纯地图**：OSM 官方瓦片 + Leaflet 渲染，无路线、无导航干扰
- **📍 自动定位**：打开即尝试浏览器定位，蓝点 + 精度圈；拒绝权限则静默回退到北京兜底
- **🔍 中文地点搜索**：Photon 优先 + Nominatim 兜底，300ms 防抖，结果按“名称 / 区县 / 城市”合并去重
- **🖱 点图反查地址**：点击地图任意处，弹窗显示中文路名 / 区 / 城市
- **🌗 深浅色跟随系统**：页面 UI 随 `prefers-color-scheme` 切换（底图为 OSM 标准样式）
- **📦 单文件交付**：仅 `index.html`，无构建、无后端、无数据库、无 token、无注册

## 🧩 技术栈（全 OSM 生态 · 全免 Key）

| 能力 | 服务 | 需 Key |
|---|---|:---:|
| 地图库 | [Leaflet 1.9](https://leafletjs.com/) (unpkg CDN) | ❌ |
| 底图瓦片 | `tile.openstreetmap.org` | ❌ |
| 地点搜索 | [Photon](https://photon.komoot.io/) (komoot) | ❌ |
| 反向地理编码 | Photon reverse + [Nominatim](https://nominatim.org/) 兜底 | ❌ |
| 定位 | 浏览器原生 `navigator.geolocation` | ❌ |

## 🚀 本地运行

推荐用本地静态服务打开，**避免 `file://` 下 OSM 瓦片被 Referer 策略拦截**：

```bash
cd 项目目录
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

> 直接双击 `index.html` 也能用搜索和定位，但 OSM 官方瓦片在 `file://` 协议下可能返回 403（黄黑占位图）。这是 OSM 瓦片使用策略限制，**不是代码问题**。

## 📦 部署

### GitHub Pages（推荐）

1. 把 `index.html` 推到仓库根目录
2. 仓库 → **Settings → Pages**
3. **Source** 选 `main` 分支、`/ (root)` 目录
4. 保存，等待约 1 分钟，访问 `https://<用户名>.github.io/<仓库名>/`

### Surge

```bash
npm install -g surge
surge . aylambmap.surge.sh
```

## 🎯 设计边界（明确不做）

- 不规划路线、不计算距离 / 耗时、不提供转弯指引 ❌
- 不接入 OSRM、GraphHopper、Valhalla 等路由服务 ❌
- 不缓存瓦片、不存搜索历史、不上传任何位置数据 ❌
- 不需要注册、不需要 API Key、不写一行后端代码 ❌

## 📁 目录结构

```
.
├── index.html      # 唯一源码：地图 + 定位 + 搜索，单文件即可运行
└── README.md       # 本文件
```

## 🤝 贡献

欢迎提 Issue 与 PR。常见可改进方向：

- 底图加载失败时给出提示（而非只显示灰底）
- 增加“重新定位”手动按钮
- 增加地图长按 / 右键选点
- 增加 URL 参数分享（`?lat=&lng=&z=`）
- 增加搜索历史（仅 `localStorage`，不上传）

## 📄 License

- **地图数据**：© [OpenStreetMap contributors](https://www.openstreetmap.org/copyright)，[ODbL](https://opendatacommons.org/licenses/odbl/) 协议
- **页面代码**：MIT，可自由复制、修改、部署
