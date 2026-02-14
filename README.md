# 🚀 Cloudflare Worker 智能部署中控 (V10.2.0)

> 全部代码为 Claude Code 完成
> 自行修改延伸功能

> **版本状态**: V10.2.0 Stable
> **核心进化**: 新增 **暗黑星空模式** 主题切换，支持动态星空背景 + 毛玻璃效果。

本项目是一个基于 Cloudflare Worker 构建的深度集成化部署管理平台。它不仅能管理多个 Cloudflare 账号，还支持一键批量部署、版本回滚、自动化流量熔断以及代码级的混淆加固，是管理大规模 Worker 节点的终极工具。

---

## 🆕 V10.2.0 更新日志

### 🌌 新功能：暗黑星空主题

* **主题切换**：Header 工具栏新增 🌙/☀️ 按钮，一键切换明亮/暗黑模式。
* **动态星空**：暗黑模式下 Canvas 绘制实时动画背景：
  * 数百颗闪烁星星（多色、随机大小、明灭呼吸效果）
  * 随机流星划过（渐变拖尾）
  * 紫色/蓝色星云光晕散布深空
* **毛玻璃效果**：所有卡片在暗黑模式下采用半透明 + `backdrop-filter: blur` 效果，透出星空背景。
* **全组件适配**：表格、输入框、弹窗、彩色标签区域均有独立暗黑配色。
* **持久化**：主题选择通过 `localStorage` 保存，刷新页面后自动恢复。

---

## 📋 V10.1.0 更新日志

### 🌐 子域名管理

* **查看子域名**：在「📂 管理」弹窗中实时显示当前账号的 `xxx.workers.dev` 子域名前缀。
* **修改子域名**：点击「✏️ 修改」按钮，输入新前缀即可通过 Cloudflare API 直接修改。
* **二次确认**：修改操作附带安全提示和二次确认对话框，防止误操作。
* **并行加载**：管理弹窗同时加载 Workers 列表和子域名信息，提升响应速度。

| 新增 API 接口 | 方法 | 说明 |
|---|---|---|
| `/api/get_subdomain` | POST | 查询账号 workers.dev 子域名前缀 |
| `/api/change_subdomain` | POST | 修改账号 workers.dev 子域名前缀 |

---

## 📋 V10.0.0 更新日志

### 🔐 安全加固

* **登录改为 POST 提交**：密码不再通过 URL 明文传递。
* **Cookie 增加 Secure 标志**：确保仅通过 HTTPS 传输。
* **API 方法校验**：只读接口限制为 `GET` 方法。
* **CSRF 防护**：所有 `POST` 请求自动校验 `Origin` 头。
* **统一错误响应**：错误信息统一返回 JSON 格式。

### 🐛 缺陷修复

* **修复混淆正则 bug**：`serverSideObfuscate` 不再误删 URL。
* **修复 checkUpdate 变量冲突**：`catch(e)` 重命名为 `catch(err)`。
* **修复编辑账号 stats 重置**：保留已有流量统计数据。

### ⚡ 改进优化

* **熔断/自动更新动态化**：从 `TEMPLATES` 动态识别有 `uuidField` 的模板。
* **compatibility_date 动态化**：部署时使用当前日期。
* **消除前后端数据重复**：前端配置由后端动态注入。

---

## ✨ 核心特性

### 🔐 智能混淆体系 (Obfuscation Pro)

* **服务器端轻量混淆**：自动执行代码压缩、注释移除和 Window Polyfill 注入。
* **前端高级混淆**：批量部署内置 `JavaScript-Obfuscator`，支持自定义配置。

### 🛡️ 流量熔断与自动轮换 (Auto Fuse)

* **实时监控**：自动统计各账号当日总用量。
* **阈值熔断**：触发后自动 **UUID 随机轮换** 并 **强制混淆部署**。

### 📜 收藏夹管理 (Favorites System)

* **版本锚定**：从 GitHub 历史中挑选稳定版本加入收藏。
* **一键回滚**：从收藏夹恢复到锁定的稳定版本。

### 🌐 子域名管理 (Subdomain Management)

* **实时查看**：管理弹窗中展示当前 `xxx.workers.dev` 子域名。
* **在线修改**：一键修改子域名前缀，格式校验 + 二次确认。

### 🌌 暗黑星空主题 (Starfield Theme)

* **动态星空**：Canvas 绘制闪烁星星 + 流星 + 星云光晕。
* **毛玻璃效果**：卡片半透明，透出星空背景。
* **一键切换**：🌙/☀️ 按钮切换，localStorage 持久化。

### 🔧 自动化运维

* **Zone 智能识别**：一键拉取账号下所有域名。
* **级联资源清理**：删除 Worker 时同步清理 KV。

---

## 📖 核心操作说明

### 🛰️ 账号管理

* **添加账号**：需提供 `Account ID`、`Email` 和 `Global API Key`。
* **读取域名**：点击"读取"自动填充 Zone。

### ✨ 批量部署 (Batch Deploy)

1. 点击顶部"批量部署"。
2. **选择模板**：`CMliu` / `Joey` 等主流模板。
3. **开启混淆**：勾选"启用代码混淆"。
4. **域名绑定**：输入前缀，自动绑定预设域名。

### 🌐 修改子域名

1. 📂 管理 → 弹窗顶部显示当前子域名。
2. 点击 ✏️ 修改 → 输入新前缀 → 二次确认。

### 🌌 切换主题

1. Header 工具栏点击 🌙 按钮切换到暗黑星空模式。
2. 再次点击 ☀️ 按钮切换回明亮模式。
3. 选择自动保存，下次打开自动恢复。

---

## 🛠️ 部署教程 (保姆级)

### 1️⃣ 创建主控 Worker

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)。
2. **Workers & Pages** → **Create Worker**，命名为 `manager`。
3. 粘贴 `worker.js` (V10.2.0) 完整代码 → **Save and deploy**。

### 2️⃣ 绑定 KV 存储 (⚠️ 核心)

1. **Settings** → **Variables** → **KV Namespace Bindings**。
2. Variable name: `CONFIG_KV`，创建命名空间 `manager_data`。

### 3️⃣ 设置安全密码

1. **Environment Variables** → `ACCESS_CODE` = 你的密码。
2. *(可选)* `GITHUB_TOKEN` = GitHub PAT (解除 API 限流)。

### 4️⃣ 开始使用

访问 `https://manager.你的前缀.workers.dev`，输入密码进入控制台。

---

## 🔑 核心数据获取指南

### Cloudflare 账号信息

* **Account ID**: `dash.cloudflare.com/` 后面的字符串。
* **Global API Key**: 头像 → My Profile → API Tokens → Global API Key → View。

### GitHub Token

1. GitHub → Settings → Developer settings → Personal access tokens (classic)。
2. 公共仓库无需勾选权限，生成 `ghp_` 开头的 Token。

---

## 📝 内置模板说明

| 模板代码 | 项目名称 | 特性说明 | 建议配置 |
| --- | --- | --- | --- |
| **cmliu** | EdgeTunnel (Beta 2.0) | 功能最全，支持订阅 | 开启 KV |
| **joey** | 少年你相信光吗 | 自动修复，极简 | **关闭 KV** (变量模式) |
| **ech** | ECH Proxy | 无需维护，WebSocket | 关闭 KV |

---

## ⚠️ 免责声明

本项目仅供技术研究和学习使用，请勿用于任何非法用途。开发者不对使用本工具产生的任何后果负责。您的 API Key 仅保存在您自己的 Cloudflare KV 中，请妥善保管。
