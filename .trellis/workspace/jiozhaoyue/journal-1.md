# Journal - jiozhaoyue (Part 1)

> AI development session journal
> Started: 2026-10-12

---

## Session: 2026-10-12 - 修复南加论坛强化脚本并扩展核心体验

### 1. 调研分析
- 确认脚本《南加北加论坛强化脚本(凛+)》无独立 GitHub 仓库，其前身为 Chrome 扩展 `soul-plus-plus-chrome-extension`。
- GreasyFork/SleazyFork 在油猴生态中被大量开发者直接作为代码托管与分发平台。
- 确认 `TypeError: Failed to execute 'fetch' on 'Window': Illegal invocation` 根因为未显式绑定 Window 宿主对象，被 Edge 浏览器 `loginCaptureHook.js` 钩子拦截后丢失 `this`。
- 确认帖子购买失败直接整页刷新根因为 `executeBackgroundBuy` 捕获异常后无条件调用 `window.location.reload()`。
- 确认暗黑模式受 Dark Reader 插件二次反色干扰，且内部样式存在 `color: color:` 语法错误。

### 2. 核心修复与变更
- **网络层修复**：新增 `safeFetch` 并升级 `fetchWithRetry`，显式使用 `fetchFn.call(targetWin, url, options)`，彻底根治 Illegal invocation。
- **购买交互优化**：健壮化 `getPostMetadata`（兼容带分页及各种参数的 tid），移除异常直接全页强刷，在原位置显示错误提示及重试/原生购买按钮。
- **暗黑模式优化**：修复 `color: color:` 语法错误，动态注入 `<meta name="darkreader-lock">` 避免 Dark Reader 插件冲突，添加 `color-scheme: dark` 原生暗黑适配。
- **跨域名同步**：升级 `createLocalStorageProperty`，支持与 `GM_getValue / GM_setValue` 双向无缝同步，解决镜像站配置不共享问题。
- **渲染与操作增强**：
  - 对帖子行和板块列表添加 `content-visibility: auto`，大幅提升长列表与无缝加载滚动帧率。
  - 增强贤者模式 NSFW 图片即时脱敏，消除滚动加载过程中的闪烁。
  - 新增 `J`/`K` 键盘快捷翻页与回帖草稿自动暂存恢复功能。

---

## Session: 2026-10-13 - 拉取原作者基线源码、构建最小侵入单 Bug 修复版并对齐增强改版

### 1. 版本拆分与基线拉取
- 从 GreasyFork 官方更新源拉取原作者（遠坂凛）v100 原始代码（18,883 行），保存为 [`南加北加论坛强化脚本(凛%2B).original.user.js`](file:///d:/Repo/Github-repo/Pubilc/southplus-script/%E5%8D%97%E5%8A%A0%E5%8C%97%E5%8A%A0%E8%AE%BA%E5%9D%9B%E5%BC%BA%E5%8C%96%E8%84%9A%E6%9C%AC%28%E5%87%9B%252B%29.original.user.js)。
- 基于原版派生出最小侵入单 Bug 修复版 [`南加北加论坛强化脚本(凛%2B).bugfix.user.js`](file:///d:/Repo/Github-repo/Pubilc/southplus-script/%E5%8D%97%E5%8A%A0%E5%8C%97%E5%8A%A0%E8%AE%BA%E5%9D%9B%E5%BC%BA%E5%8C%96%E8%84%9A%E6%9C%AC%28%E5%87%9B%252B%29.bugfix.user.js)。

### 2. 最小侵入 Bug 修复收敛与双版本对齐
- 将单 Bug 修复版与现有增强改版 [`南加北加论坛强化脚本(凛%2B).user.js`](file:///d:/Repo/Github-repo/Pubilc/southplus-script/%E5%8D%97%E5%8A%A0%E5%8C%97%E5%8A%A0%E8%AE%BA%E5%9D%9B%E5%BC%BA%E5%8C%96%E8%84%9A%E6%9C%AC%28%E5%87%9B%252B%29.user.js) 的 Bug 修复部分完全统一为仅 5 处局部极简改动（共 15 行）：
  1. `fetchWithRetry` 内联绑定 `win.fetch.call(win, url, options)`（移除独立 `safeFetch` 函数）。
  2. 修复 4246 行 `color: color:` CSS 语法错误。
  3. `html.rinsp-dark-mode` 声明 `color-scheme: dark;`。
  4. `applyDarkTheme` 内联动态添加/移除 `<meta name="darkreader-lock">`（移除独立 `updateDarkReaderLock` 函数）。
  5. 还原对 `getPostMetadata`、`enhanceBuyButtons` 和 `executeBackgroundBuy` 主流程的侵入修改，仅在 `run().catch` 中针对非 `content outdated` 异常显示 `.rinsp-buy-failed` 错误原因而不直接强刷页面。
- 现有增强改版完整保留全部 4 项扩展功能，并将 `@author` 更新为 `jiozhaoyue`。



## Session 1: 转公开与v101版本增强发布准备
<!-- trellis-session: v=2 fp=cbb874f64d97d1d3 -->

**Date**: 2026-11-06
**Task**: 转公开与v101版本增强发布准备
**Branch**: `main`

### Summary

核查上游v100基线、重构英文命名southplus-enhancer、修复免刷新回帖草稿残留Bug、强化跨域配置同步与弹窗快捷键保护、配置.gitignore与开源转公开文件
Topics: [.trellis/research/2026-11-06-public-release-enhancer.md](../../research/2026-11-06-public-release-enhancer.md)

### Git Commits

(No commits - planning session)

### Status

[OK] **Completed**


## Session 2: 转公开与v101版本增强发布准备
<!-- trellis-session: v=2 fp=9c4f6818e6d0a289 -->

**Date**: 2026-11-06
**Task**: 转公开与v101版本增强发布准备
**Branch**: `main`

### Summary

核查上游v100基线、重构英文命名southplus-enhancer、修复免刷新回帖草稿残留Bug、强化跨域配置同步与弹窗快捷键保护、配置.gitignore与开源转公开文件
Topics: [.trellis/research/2026-11-06-public-release-enhancer.md](../../research/2026-11-06-public-release-enhancer.md)

### Git Commits

| Hash | Message |
|------|---------|
| `9affc7b` | feat: release v101 with bugfixes, english naming, and public open source setup |

### Status

[OK] **Completed**


## Session 3: SoulPlus-Next Public Release and Upstream Realignment
<!-- trellis-session: v=2 fp=bffad3da72eeef50 -->

**Date**: 2026-11-06
**Task**: SoulPlus-Next Public Release and Upstream Realignment
**Branch**: `main`

### Summary

Renamed project to SoulPlus-Next, updated userscript metadata and URLs, eliminated emojis, created GitHub Actions release workflow, aligned with upstream soul-plus-plus
Topics: [.trellis/research/2026-11-06-public-release-enhancer.md](../../research/2026-11-06-public-release-enhancer.md)

### Git Commits

(No commits - planning session)

### Status

[OK] **Completed**
