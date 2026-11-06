# South Plus Forum Enhancer (凛+ 增强重构版)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v101-brightgreen.svg)](southplus-enhancer.user.js)
[![UserScript](https://img.shields.io/badge/UserScript-Tampermonkey%20%7C%20ScriptCat%20%7C%20Violentmonkey-orange.svg)](southplus-enhancer.user.js)

针对南加/北加/东加/白加/魂加（South-Plus、North-Plus 等相关论坛）的高性能全功能体验增强油猴脚本。

本项目基于原作者 **遠坂凛** 的 SleazyFork 脚本（ID: 454120，前身为 Chrome 扩展 `soul-plus-plus-chrome-extension`）进行重构、Bug 彻底修复、键盘交互与多镜像域名深度同步扩展，专为极致浏览体验而生。

---

## 🌟 核心特色与功能

### 1. ⚡ 免刷新交互与智能草稿保护
- **购买免刷新**：自动获取帖子元数据并在原位异步完成购买，杜绝整页重新加载。
- **免刷新回帖**：异步提交回帖，自动滚动至新楼层并更新页面状态。
- **智能草稿恢复与清理（v101 修复增强）**：
  - 自动实时在本地保存回帖草稿，意外关闭或切换页面不丢失。
  - 成功回帖（包括免刷新回复）后**自动彻底清理草稿**，杜绝以往版本残留旧草稿反复弹出的问题。

### 2. 🌙 沉浸式原生暗黑模式
- 动态注入 `<meta name="darkreader-lock">`，彻底杜绝与第三方 Dark Reader 等反色扩展产生二次反色/文字发白冲突。
- 原生声明 `color-scheme: dark`，统一浏览器滚动条与表单控件暗黑质感。
- 修复原版 CSS 属性冗余语法错误（`color: color:`），杜绝样式解析警告。

### 3. ⌨️ 极速键盘导航（带弹窗防误触）
- `J` / `K` 键快速进行上一页 / 下一页跳转翻页。
- **弹窗防误触保护（v101 增强）**：当处于大图图墙模式（PicWall）、设置弹窗（Rinsp Dialog）或搜索框交互时，自动屏蔽快捷键翻页，防止看图与配置时误翻页。

### 4. 🌐 跨镜像域名配置双向无缝同步
- 针对南+庞大的镜像域名群（`south-plus.net`, `south-plus.org`, `soul-plus.net`, `north-plus.net`, `white-plus.net` 等）：
- 采用 `GM_getValue` 作为跨域配置的核心持久化源，解决传统 `localStorage` 仅限单域名生效、镜像站换网址后设置丢失或分裂的痛点。

### 5. 🚀 渲染性能优化与 SFW 贤者安全模式
- 引入现代 CSS `content-visibility: auto`，视口外楼层与长列表节点按需延迟渲染，大幅降低长贴内存占用并提升高刷新率滚动流畅度。
- **SFW 贤者模式优化**：NSFW 图片即时滤镜脱敏，消除滚动懒加载图片时的明暗闪烁。

---

## 📦 仓库版本说明

| 文件名 | 类型 | 说明 |
| :--- | :--- | :--- |
| **[`southplus-enhancer.user.js`](southplus-enhancer.user.js)** | **推荐强化版 (v101)** | 包含全部 Bug 修复 + 智能草稿清理 + 跨镜像同步 + 快捷键导航 + 渲染性能优化 |
| **[`southplus-enhancer.bugfix.user.js`](southplus-enhancer.bugfix.user.js)** | **最小侵入单 Bug 修复版** | 严格保持原版 100% 结构，仅局部修复 Illegal invocation、暗黑样式与购买异常处理 |
| **[`southplus-enhancer.original.user.js`](southplus-enhancer.original.user.js)** | **上游原版基线 (v100)** | 原作者原始代码镜像存档（零修改），作为基线比对与审计依据 |

---

## 📥 安装指南

### 前提条件
请先在浏览器中安装任意一款现代用户脚本管理器：
- [Tampermonkey (篡改猴)](https://www.tampermonkey.net/)
- [ScriptCat (脚本猫)](https://docs.scriptcat.org/)
- [Violentmonkey (暴力猴)](https://violentmonkey.github.io/)

### 安装链接
- **增强重构版 (推荐)**：
  - 点击安装：[southplus-enhancer.user.js](https://raw.githubusercontent.com/jiozhaoyue/southplus-script/main/southplus-enhancer.user.js)
- **单 Bug 修复版 (纯净)**：
  - 点击安装：[southplus-enhancer.bugfix.user.js](https://raw.githubusercontent.com/jiozhaoyue/southplus-script/main/southplus-enhancer.bugfix.user.js)

---

## 🛠️ 脚本市场发布指南 (Publishing Guide)

### 1. 发布到 Sleazy Fork (Greasy Fork 成人分区)
> **注意**：由于南+论坛涉及成人内容，Greasy Fork 会将该脚本自动归类或要求发布至 **Sleazy Fork**。
1. 登录 [Sleazy Fork](https://sleazyfork.org/)。
2. 点击右上角 **“发布新脚本” (Post a script)**。
3. 将 [`southplus-enhancer.user.js`](southplus-enhancer.user.js) 的全部内容复制粘贴到脚本代码区。
4. 填写简短更新说明（如 `v101: 修复免刷新回帖草稿清理、完善跨域同步、快捷键优化`）。
5. 点击提交即可完成发布。

### 2. 发布到 ScriptCat (脚本猫)
1. 登录 [ScriptCat 脚本市场](https://scriptcat.org/)。
2. 点击 **“控制台” -> “发布脚本”**。
3. 粘贴 [`southplus-enhancer.user.js`](southplus-enhancer.user.js) 内容，脚本猫会自动识别元数据（`@name`, `@version`, `@match` 等）。
4. 勾选开源协议 `MIT` 并点击发布。

---

## 📝 更新日志 (Changelog)

### v101 (2026-11)
- **重构与命名规范化**：脚本与仓库全面采用英文标准命名 `southplus-enhancer.user.js`，避免 URL 编码问题。
- **草稿自动清理**：修复免刷新回帖成功后无法触发原生表单提交事件导致草稿无法清除的 Bug。
- **快捷键交互防护**：在图墙（PicWall）或设置弹窗开启时自动抑制 J/K 翻页，防止后台误跳页。
- **跨镜像深度同步**：改进 `createLocalStorageProperty`，优先通过 `GM_getValue` 保证各镜像域名配置一致性。
- **元数据与多语言**：适配中英文双语元数据标签，移除原作者旧覆盖更新源，适配 GitHub Releases 与各大脚本市场。

### v100 (基线修复)
- 修复 Edge 浏览器扩展拦截环境下的 `TypeError: Failed to execute 'fetch' on 'Window': Illegal invocation`。
- 修复暗黑模式 `color: color:` 语法错误与 Dark Reader 插件二次反色冲突。
- 购买异常时显示错误信息而不强行整页刷新。

---

## ⚖️ 开源协议 (License)
本项目遵循 [MIT License](LICENSE)。原版代码版权归原作者 **遠坂凛** 所有，改版增强与维护由 **jiozhaoyue** 负责。
