# SoulPlus-Next (魂+ Next)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v101-brightgreen.svg)](soul-plus-next.user.js)
[![Userscript](https://img.shields.io/badge/Userscript-Tampermonkey%20%7C%20ScriptCat%20%7C%20Violentmonkey-orange.svg)](soul-plus-next.user.js)
[![Auto Update](https://img.shields.io/badge/Auto--Update-GitHub%20Raw%20%26%20Actions-blueviolet.svg)](https://raw.githubusercontent.com/jiozhaoyue/soul-plus-next/main/soul-plus-next.user.js)

面向南加/魂加/北加/白加/东加等系列论坛（South-Plus、Soul-Plus、North-Plus 等相关镜像站）的现代全功能体验套件与脚本重构版。

本项目直接继承自经典浏览器扩展项目 [FetchTheMoon/soul-plus-plus-chrome-extension](https://github.com/FetchTheMoon/soul-plus-plus-chrome-extension)（Soul++）及其后续油猴移植版（SleazyFork ID: 454120）。在保留上游经典无缝浏览体验的基础上，进行现代浏览器兼容性修复、草稿智能闭环保护、原生深色模式防冲突加固、键盘弹窗联动防护以及全镜像域名配置深度双向同步。

---

## 上游溯源与演进关系

| 项目阶段 | 项目名称 | 开发者 / 维护者 | 状态与说明 |
| :--- | :--- | :--- | :--- |
| 原版上游扩展 | soul-plus-plus-chrome-extension | FetchTheMoon (水中捞月) | 经典 Chrome 扩展，由于商店政策限制已下架并归档 |
| 移植维护版 | 南加北加论坛强化脚本 (凛+) | 遠坂凛 (tousakarin) | 油猴移植版 (SleazyFork 454120)，停更于 v100 |
| 本项目 (Next) | **SoulPlus-Next (魂+ Next)** | jiozhaoyue | **当前活跃维护**：现代化重构、Bug修复、实时热更、跨镜像同步 |

---

## 核心功能与特性

### 1. 免刷新交互与智能草稿保护
- 购买免刷新：异步获取帖子售价元数据并在当前视图就地完成购买，避免整页重新加载带来的打断感。
- 免刷新回帖：异步提交回帖内容，自动定位至新增楼层并无缝更新页面上下文。
- 智能草稿闭环机制：
  - 编辑器自动实时将输入内容持久化至本地草稿池，意外关闭标签或切换网络时随时还原。
  - 在免刷新回帖或普通回帖成功后，自动执行草稿池清理并重置编辑器状态，杜绝以往版本旧草稿残留弹出的顽疾。

### 2. 现代暗黑模式与反色保护
- 原生声明 color-scheme: dark，统一浏览器原生滚动条、表单按钮和输入框的深色渲染质感。
- 动态注入 meta 标签 darkreader-lock，防止与 Dark Reader 等第三方反色扩展产生冲突导致文字发白或双重反色。
- 修复原版 CSS 中属性语法错误（如 color: color:），消除控制台样式解析告警。

### 3. 极速键盘导航与弹窗防误触
- 支持使用 J 键与 K 键实现上一页与下一页的无延迟快捷翻页。
- 弹窗上下文感知（Modal Guard）：当处于大图图墙模式（PicWall）、设置控制台（Dialog）或搜索输入状态时，自动抑制快捷键触发，避免看图与交互时发生意外翻页。

### 4. 全镜像域名配置深度同步
- 南+论坛拥有广泛的镜像域名生态（包括 south-plus.net、south-plus.org、soul-plus.net、north-plus.net、white-plus.net、east-plus.net 等）。
- 重构配置存储层，优先采用 GM_getValue / GM_setValue 作为跨域单一事实来源，彻底解决以往依赖单一域名 localStorage 导致镜像站切换后偏好设置割裂与丢失的问题。

### 5. 渲染性能优化与 SFW 贤者安全模式
- 运用现代 CSS content-visibility: auto 特性，长帖子楼层与列表在视口外延迟绘制，有效减小长列表内存消耗并改善高刷屏滚动的帧率稳定性。
- SFW 贤者安全模式：敏感图片即时滤镜脱敏与头像替换，去除滚动懒加载图片时的明暗闪烁。

---

## 仓库版本矩阵

| 文件名 | 类型 | 说明 |
| :--- | :--- | :--- |
| [soul-plus-next.user.js](soul-plus-next.user.js) | 推荐强化版 (v101) | 包含完整功能：Bug修复、草稿清理、跨镜像同步、快捷键防护、性能优化 |
| [soul-plus-next.bugfix.user.js](soul-plus-next.bugfix.user.js) | 纯净修复版 (v100.1) | 保持原版最小改动，仅修复 Illegal invocation、Dark Reader 样式与购买异常 |
| [soul-plus-next.original.user.js](soul-plus-next.original.user.js) | 上游基线存档 (v100) | 原作者原始代码镜像存档（零修改），用于差异比对与合规审查 |

---

## 安装指南

### 前提环境
请在支持 Userscript 的现代浏览器中安装任意一款脚本管理器：
- [Tampermonkey](https://www.tampermonkey.net/)
- [ScriptCat](https://docs.scriptcat.org/)
- [Violentmonkey](https://violentmonkey.github.io/)

### 安装地址与镜像源

#### 推荐强化版 (SoulPlus-Next)
- [GitHub 官方直链 (即时更新)](https://raw.githubusercontent.com/jiozhaoyue/soul-plus-next/main/soul-plus-next.user.js)
- [jsDelivr 全球 CDN 镜像](https://cdn.jsdelivr.net/gh/jiozhaoyue/soul-plus-next@main/soul-plus-next.user.js)

#### 纯净修复版 (Bugfix Only)
- [GitHub 官方直链](https://raw.githubusercontent.com/jiozhaoyue/soul-plus-next/main/soul-plus-next.bugfix.user.js)
- [jsDelivr 全球 CDN 镜像](https://cdn.jsdelivr.net/gh/jiozhaoyue/soul-plus-next@main/soul-plus-next.bugfix.user.js)

---

## 实时更新机制说明

为了保证脚本在发布后能够第一时间获取修复与功能更新，本项目采用全链路热更机制：

1. 脚本元数据直连官方源：
   在脚本头部内建 @updateURL 与 @downloadURL，统一指向 GitHub main 分支的原始发布地址。
2. 自动化发布流：
   每次向 main 分支提交代码后，GitHub Actions 自动化流水线将执行代码合规检测并构建 Release 产物。
3. 客户端静默/自动感知：
   当脚本管理器（如 Tampermonkey / ScriptCat）执行例行检查或用户手动点击检查更新时，客户端将实时拉取最新版本完成无缝升级。

---

## 脚本市场发布操作指南

### 1. 发布至 Sleazy Fork (Greasy Fork 成人分区)
注意：由于论坛涉及成人内容，相关脚本在 Greasy Fork 体系下需归类于 Sleazy Fork。
1. 登录 Sleazy Fork 平台。
2. 点击右上角 "发布新脚本" (Post a script)。
3. 打开本地 soul-plus-next.user.js，全选复制并粘贴到脚本源码输入框。
4. 元数据标签 (@name, @version, @match, @updateURL 等) 将被自动解析。
5. 填写版本更新说明并确认发布。

### 2. 发布至 ScriptCat (脚本猫市场)
1. 登录 ScriptCat 开发者控制台。
2. 进入 "控制台" -> "发布脚本"。
3. 粘贴 soul-plus-next.user.js 源码，确认识别的权限清单与域名列表。
4. 勾选 MIT 开源许可证，提交即可在脚本猫市场公开展示。

---

## 支持的论坛镜像域名列表

脚本适配以下全部论坛官方及镜像域名：
- south-plus.net / south-plus.org
- soul-plus.net
- north-plus.net
- white-plus.net
- east-plus.net
- level-plus.net
- snow-plus.net
- spring-plus.net
- summer-plus.net
- blue-plus.net
- imoutolove.me

---

## 更新日志

### v101
- 项目命名全面升级为 SoulPlus-Next (魂+ Next)，致敬原上游扩展 soul-plus-plus。
- 修复免刷新回帖成功后原生表单提交事件拦截导致的草稿无法清理问题。
- 快捷键翻页集成弹窗防误触保护，在图墙浏览或弹出设置面板时自动屏蔽 J/K 跳转。
- 跨镜像配置存储层重构，采用 GM 存储作为主数据源，保障多镜像域数据无缝同步。
- 脚本配置全自动化热更链接与双语元数据标签。

### v100 (基线修复)
- 修复 Chromium / Edge 浏览器环境下因脚本拦截导致的 Illegal invocation 异步错误。
- 修复暗黑主题中 color 属性语法错误，注入防反色标记解决与 Dark Reader 的渲染冲突。
- 优化购买逻辑，当返回异常信息时显示详细提示而非强行整页重载。

---

## 开源许可与致谢

- 本项目基于 [MIT License](LICENSE) 开源。
- 致敬经典 Chrome 扩展 soul-plus-plus 原作者 FetchTheMoon。
- 感谢油猴移植版维护者 遠坂凛。
- 后续维护、重构与持续更新由 jiozhaoyue 负责。
