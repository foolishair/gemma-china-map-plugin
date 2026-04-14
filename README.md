# 高德地图 Skill for Google AI Edge Gallery

在 Google AI Edge Gallery 中使用高德地图替代 Google Maps，为中国大陆用户提供精准的地图定位和周边 POI 搜索。

## 功能

- **地名定位**：输入任意中国地址/地名，在高德地图上精准标注
- **周边搜索**：搜索附近的餐厅、咖啡店、酒店等 POI，显示距离和联系方式
- **自动触发**：模型根据对话内容自动判断是否调用地图，无需手动指定
- **完全国内可用**：不依赖 Google 服务，无需翻墙

## 前置工作：注册高德 API Key

### 第一步：注册高德开放平台账号

1. 打开 [高德开放平台](https://console.amap.com/)
2. 点击右上角「注册」，用手机号注册账号
3. 完成实名认证（个人开发者，需要身份证号）
4. 认证审核通常**即时通过**

### 第二步：创建应用

1. 登录后进入 [控制台](https://console.amap.com/)
2. 点击左侧菜单「应用管理」→「我的应用」
3. 点击右上角「创建新应用」
4. 填写：
   - 应用名称：`AI Edge Gallery`（随意填写）
   - 应用类型：选「其他」

### 第三步：申请 Key

1. 在刚创建的应用下，点击「添加 Key」
2. 填写：
   - Key 名称：`amap-skill`（随意填写）
   - **服务平台：选「Web端(JS API)」**（必须选这个！）
   - 域名白名单：留空或填 `*`
3. 提交后你会得到两个值：
   - **API Key**（一串字母数字，如 `a1b2c3d4e5f6g7h8`）
   - **安全密钥 (Security Key)**（另一串字母数字）
4. **妥善保存这两个值**，后面要用

### 免费额度说明

| 服务 | 每日免费额度 |
|------|------------|
| 地图显示 | 无限制 |
| 地理编码（地名→坐标） | 100 次/天 |
| POI 搜索（周边查询） | 100 次/天 |

个人手机日常使用完全够用。

---

## 导入 Skill 到 AI Edge Gallery

### 方式一：通过 GitHub Pages 导入（推荐）

#### 1. Fork 或上传到 GitHub

1. 在 GitHub 上创建一个新仓库（如 `amap-china-skill`）
2. 将 `amap-china` 文件夹内容上传到仓库根目录：
   ```
   你的仓库/
   ├── SKILL.md
   ├── README.md
   └── scripts/
       ├── index.html
       └── webview.html
   ```

#### 2. 开启 GitHub Pages

1. 进入仓库「Settings」→「Pages」
2. Source 选「Deploy from a branch」
3. Branch 选 `main`，目录选 `/ (root)`
4. 点击 Save
5. 等待几分钟，GitHub Pages 会生成一个 URL，如：
   `https://你的用户名.github.io/amap-china-skill/`

#### 3. 在 AI Edge Gallery 中导入

1. 打开 AI Edge Gallery App
2. 进入 Agent Skills 页面
3. 点击添加 Skill（通常是 + 号或设置图标）
4. 选择「从 URL 导入」
5. 输入你的 GitHub Pages URL：
   `https://你的用户名.github.io/amap-china-skill/`
6. 确认导入

#### 4. 设置 API Key

首次使用时，App 会弹出一个对话框要求输入密钥。输入格式：

```
你的API_KEY|你的安全密钥
```

例如：`a1b2c3d4e5f6g7h8|x9y8z7w6v5u4t3s2`

中间用英文竖线 `|` 分隔，**不要有空格**。

### 方式二：通过本地文件导入（Android）

1. 用数据线连接手机和电脑
2. 将 `amap-china` 文件夹复制到手机存储
3. 在 AI Edge Gallery 中选择「从本地文件导入」
4. 选择 `amap-china` 文件夹中的 `SKILL.md`

---

## 使用方法

导入后，在 Agent Skills 模式下正常聊天即可。模型会自动判断是否需要调用地图。

### 示例对话

| 你说的 | 模型自动执行 |
|--------|------------|
| "故宫在哪" | 在高德地图上标注故宫位置 |
| "三里屯附近有什么咖啡店" | 搜索三里屯 2km 内的咖啡店并列出 |
| "上海外滩周边有什么好吃的" | 搜索外滩附近餐厅并显示距离 |
| "在地图上显示深圳南山" | 定位到深圳南山区 |

### 与内置 interactive-map 的关系

两个地图 Skill 可以共存：
- **amap-china**：中国境内地点（高德地图，坐标精准）
- **interactive-map**：海外地点（Google Maps）

模型会根据 SKILL.md 中的描述自动判断使用哪个。

---

## 本地测试

在导入 App 之前，你可以在电脑浏览器中测试地图功能：

1. 打开 `scripts/webview.html`，在 URL 后添加参数：
   ```
   webview.html?location=北京故宫&action=locate&key=你的API_KEY&security=你的安全密钥
   ```
2. 测试 POI 搜索：
   ```
   webview.html?location=三里屯&action=search&keyword=咖啡店&key=你的API_KEY&security=你的安全密钥
   ```
3. 确认地图正常加载、标注正确、POI 列表显示

---

## 分享到社区

如果你觉得这个 Skill 好用，可以分享给更多人。

### 方式一：分享到 Google AI Edge Gallery 社区（GitHub Discussions）

1. 确保你的 Skill 已上传到 GitHub 仓库并开启了 GitHub Pages
2. 打开 [AI Edge Gallery Skills 讨论区](https://github.com/google-ai-edge/gallery/discussions/categories/skills)
3. 点击右上角绿色按钮「New discussion」
4. 填写表单：
   - **标题**：`Amap China (高德地图) - Map skill for mainland China users`
   - **正文** 参考以下模板：

```markdown
## Amap China (高德地图)

A map skill for mainland China users. Replaces the built-in `interactive-map` (Google Maps)
with Amap (Gaode Maps), which provides accurate coordinates and rich POI data in China.

### Features
- Accurate location positioning in mainland China (no coordinate offset)
- Nearby POI search (restaurants, cafes, hotels, etc.)
- Auto-triggered by the LLM when Chinese locations are mentioned
- No VPN required

### Requirements
- Free API key from [Amap Open Platform](https://console.amap.com/)
- Network connection (for loading map tiles, no VPN needed in China)

### Import URL
`https://你的用户名.github.io/amap-china-skill/`

### Screenshots
[附上几张手机截图]

### Source Code
[你的 GitHub 仓库 URL]
```

5. 点击「Start discussion」发布

### 方式二：提交 Pull Request 到官方仓库

如果你想让这个 Skill 被更多人发现，可以尝试提交到官方仓库：

1. Fork [google-ai-edge/gallery](https://github.com/google-ai-edge/gallery) 仓库
2. 在 `skills/community/` 目录下创建 `amap-china/` 文件夹
3. 将你的 Skill 文件复制进去：
   ```
   skills/community/amap-china/
   ├── SKILL.md
   └── scripts/
       ├── index.html
       └── webview.html
   ```
4. 创建 Pull Request：
   - **标题**：`feat: Add Amap China map skill for mainland China users`
   - **描述**：说明这个 Skill 解决了什么问题（Google Maps 在中国不可用/坐标偏移），以及它的功能
5. 等待维护者 Review 和合并

### 方式三：直接分享 URL

最简单的方式——把你的 GitHub Pages URL 发给朋友：

```
https://你的用户名.github.io/amap-china-skill/
```

对方在 AI Edge Gallery 里「从 URL 导入」即可使用。

---

## 常见问题

### Q: 地图加载不出来？
- 检查手机是否联网（高德地图需要网络加载瓦片，但不需要翻墙）
- 检查 API Key 是否正确，是否选的「Web端(JS API)」类型

### Q: 提示"未找到地点"？
- 尝试更详细的地址，如"北京市朝阳区三里屯"而不是"三里屯"
- 高德地理编码对简短地名的识别可能不如完整地址

### Q: 每日 100 次够用吗？
- 个人手机日常使用足够。如果不够，可以在高德开放平台申请企业认证，额度会提升到 1000+ 次/天

### Q: 模型没有自动调用高德，还是用了 Google Maps？
- 确保你在 Agent Skills 模式下（不是 AI Chat）
- 用中文提问涉及中国地点时，模型应自动选择 amap-china
- 如果仍然选错，可以在对话中明确说"用高德地图搜索"

---

## 许可证

MIT License - 自由使用、修改和分发。
