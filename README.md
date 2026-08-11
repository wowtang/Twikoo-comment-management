# Twikoo 评论管理后台 · 开源版

一个开箱即用的 **Twikoo 评论系统管理面板**，提供美观、响应式的后台界面，支持评论审核、配置管理、数据导入导出、深色主题等特性。**无需额外安装**，仅需一个 HTML 文件即可部署。

---

## 📖 项目简介

本项目是一个基于 **Twikoo** 评论引擎的纯前端管理面板，所有代码整合在 `index.html` 中。它通过调用 Twikoo 的官方 JavaScript SDK，实现以下功能：

- 登录验证（固定账号 + 自定义密码）
- 评论列表查看、审核（通过 / 隐藏）、删除、回复
- 多级评论树形展示（支持缩进与级数标记）
- 配置中心（通用、插件、隐私、反垃圾、人机验证、通知等分组）
- 数据导入（从 Valine、Disqus 等迁移）与导出 JSON 备份
- 一键切换明/暗主题
- 评论详情弹窗（含 IP、UA、归属地等完整信息）
- 响应式布局，适配移动端

**适用场景**：个人博客、小型社区、静态网站等使用 Twikoo 作为评论系统的站点，需要轻量级管理后台。

---

## ✨ 功能特性

| 模块 | 功能 |
|------|------|
| **登录安全** | 固定账号 + 密码；支持“记住密码”和“自动登录” |
| **评论管理** | 查看、搜索、过滤（显示/隐藏）、审核、删除、回复 |
| **树形结构** | 自动识别父子关系，用缩进和连接线展示多级评论，并显示真实级数徽章 |
| **配置中心** | 六类配置分组（通用/插件/隐私/反垃圾/人机验证/通知），每个配置项显示中文短标题、英文变量名、详细说明，并提供下拉选择、开关、多选标签等友好控件 |
| **数据导入** | 支持从 Valine、Disqus、Artalk、Waline、Twikoo 等系统导入评论 |
| **数据导出** | 一键导出全部评论与访问量为 JSON 文件 |
| **主题切换** | 跟随系统或手动切换深色/浅色模式，记忆偏好 |
| **评论详情** | 弹窗展示用户信息（昵称/邮箱/网址/UID）、网络信息（IP/归属地/UA）、评论内容、时间等，支持一键复制全部信息 |
| **移动适配** | 侧边栏抽屉，触屏友好 |

---

## 🛠 技术栈

- **前端框架**：原生 JavaScript（无第三方框架依赖）
- **UI 库**：Element UI（由 Twikoo SDK 内置）
- **评论引擎**：[Twikoo](https://twikoo.js.org/)（v1.7.15+）
- **图标库**：Font Awesome 6
- **样式**：纯 CSS 变量，支持深色模式
- **存储**：LocalStorage（记住密码、自动登录、主题偏好）

---

## 🚀 快速开始

### 1. 前置条件
- 已部署 [Twikoo 后端](https://twikoo.js.org/backend.html)（云函数或自托管），并获得 **环境 ID（envId）**。
- 一个可访问的静态服务器（或直接双击 HTML 文件本地预览）。

### 2. 下载与配置
- 下载 `index.html` 文件。
- 用文本编辑器打开，找到以下占位符并替换：

```html
<!-- 页面标题 -->
<title>[你的网站名字] · 评论管理后台</title>

<!-- 侧边栏品牌 -->
<span class="title">[你的网站名字]</span>

<!-- 登录卡片 -->
<h2 class="custom-login-title">[你的网站名字] 评论管理</h2>

<!-- Twikoo 初始化 -->
window.twikoo.init({
  envId: '[twikoo环境地址]',   // 替换为你的 envId
  ...
})

<!-- 固定账号（硬编码） -->
var FIXED_ACCOUNT = '[账号自定义]';   // 替换为你想要的登录账号

<!-- 登录密码（由用户自己输入，不硬编码） -->
```

> ⚠️ **安全提示**：登录密码通过用户输入验证，不存储在代码中；但固定账号硬编码，请修改为你自己的账号。

### 3. 部署
将修改后的 `index.html` 上传到你的网站服务器（如 Nginx、Apache、Vercel、Netlify 等），或者直接在浏览器中打开（仅用于本地测试，不建议生产）。

### 4. 使用
- 访问 `index.html` 页面，显示登录框。
- 输入预设的账号和密码，点击登录。
- 登录成功后，侧边栏导航可用，默认进入「评论管理」。
- 根据需要管理评论、调整配置、导入导出数据。

---

## 📂 目录结构

```
/
└── index.html          # 完整单页应用（所有样式、脚本、HTML 整合）
```

---

## 🔧 配置说明

### 登录设置
- **账号**：硬编码为 `[账号自定义]`，你可以修改该变量。
- **密码**：由用户输入，支持“记住密码”（保存到 LocalStorage）和“自动登录”。

### 主题偏好
- 默认跟随系统时间（6:00–18:00 为浅色，其余为深色）。
- 点击顶部工具栏的太阳/月亮图标可手动切换，偏好会保存至 LocalStorage。

### 评论显示
- 评论列表按树形顺序排列（父评论在前，子评论紧随其后）。
- 子评论显示缩进，并标注真实级数（如 ①、②、③…）。
- 点击评论中的 **时间** 可在“相对时间”和“绝对时间（YYYY-MM-DD HH:MM:SS）”之间切换。

### 配置项快捷操作
- 下拉选择（如头像 CDN、SMTP 服务）支持关键字搜索。
- 布尔值配置（true/false）显示为 iOS 风格开关。
- 多选配置（如“显示字段”）以标签按钮形式展现，点击切换。

---

## 🤝 自定义扩展

### 修改品牌信息
- 搜索 `[你的网站名字]` 并全局替换为你的网站名称。
- 更换品牌图标：修改 `.brand-logo` 内的 Font Awesome 图标类。

### 调整界面配色
- CSS 变量位于 `:root` 和 `[data-theme="dark"]` 中，可自由修改主色、背景、圆角等。

### 添加新的配置分组
1. 在 `CONFIG_MAP` 中添加分组名及对应的 Twikoo 分组标题。
2. 在侧边栏 `nav-submenu` 中添加对应的 `nav-sub-item`（`data-config` 属性）。
3. 在 `CONFIG_META` 中补充该分组的图标和描述。
4. 如需新增配置项的短标题，在 `SHORT_TITLE_MAP` 中添加映射。

---

## 📋 常见问题

**Q：登录时提示“账号错误”或“密码错误”？**  
A：请确认你已修改 `FIXED_ACCOUNT` 变量为你自己的账号，并输入正确的密码（密码未硬编码，首次登录需手动输入）。

**Q：配置修改后没有生效？**  
A：Twikoo 配置保存在后端，修改后需点击“保存”按钮。若保存失败，检查网络连接及 envId 是否正确。

**Q：评论列表不显示或为空？**  
A：确保 Twikoo 后端正常运行，且该页面路径（`path`）下已有评论数据。首次使用可先发表一条测试评论。

**Q：如何重置管理员密码？**  
A：密码由用户输入，无需重置。若忘记密码，可清除浏览器 LocalStorage 中 `twikoo-admin-pwd` 项，重新登录时输入新密码即可。

**Q：支持多管理员吗？**  
A：本面板为单账号模式，若需多管理员，建议使用 Twikoo 官方后台或二次开发。

**Q：部署到生产环境安全吗？**  
A：本面板仅作为前端界面，所有权限校验依赖 Twikoo 后端的登录令牌（Token）。请确保 Twikoo 后端配置了正确的访问控制，并定期更新密码。

---

## 📄 开源协议

本项目基于 **MIT License** 开源，你可以自由使用、修改、分发，但需保留原作者的版权声明。

---

## 🙏 致谢

- [Twikoo](https://twikoo.js.org/) – 简洁的评论系统
- [Font Awesome](https://fontawesome.com/) – 图标库
- [Element UI](https://element.eleme.io/) – Vue 组件库（由 Twikoo 内置）

---

## 🖼️ 项目预览图

<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/423414e5-485a-4a40-8d41-e1e533999728" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/fe76abba-3146-414d-a972-f7820df68722" />
<img width="1743" height="928" alt="image" src="https://github.com/user-attachments/assets/67755b6f-b2e7-448c-97f0-b41022def953" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/1ad6a745-93ed-44ac-9122-038cb418c2e5" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/3ed25ca9-c44e-4ed2-980d-0310f43a247d" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/5bdd21fc-3fc8-4b08-a964-850579044312" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/0ad6e174-7dd0-4343-8980-85f15940379c" />
<img width="1738" height="922" alt="image" src="https://github.com/user-attachments/assets/9bbe6254-c757-43ae-84e7-c757e16fbbc3" />
<img width="1735" height="922" alt="image" src="https://github.com/user-attachments/assets/7bd93263-73af-43ee-8dfa-721c816b8e34" />

---







