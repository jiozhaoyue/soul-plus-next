# PRD: 南加北加论坛强化脚本(凛+) 核心修复与体验优化

## 1. 背景与目标
针对用户反馈的油猴脚本《南加北加论坛强化脚本(凛+)》的一系列关键缺陷及需求：
1. **GitHub 与代码仓库现状解答**：解答关于该脚本在 GitHub 与 GreasyFork 的托管生态。
2. **核心报错修复**：
   - `TypeError: Failed to execute 'fetch' on 'Window': Illegal invocation`：修复由于 Edge 密码管理器等钩子导致的全局 fetch 上下文丢失，恢复自动任务、监控帖子、收藏、评分等网络请求。
   - **购买直接刷新页面且未购买成功**：移除失败直接刷新逻辑，健壮化帖子元数据提取与异常处理，提供直观的失败原因及重试/原生操作入口。
   - **暗黑模式问题**：修复 CSS 语法错误（`color: color:`），动态注入 `darkreader-lock` 避免与 Dark Reader 扩展发生双重反色冲突。
3. **功能扩展与体验优化**：
   - 跨镜像域名配置同步（基于 GM 存储）。
   - 现代 CSS 与渲染优化（`content-visibility: auto`，滚动条暗黑配色）。
   - 快捷翻页与防丢草稿暂存。
   - 动态翻页中 NSFW 图片遮罩增强。

## 2. 详细技术方案

### 2.1 安全 Window Fetch 绑定
- 在 `fetchWithRetry` 中，通过显式指定 `targetWindow = (typeof unsafeWindow !== 'undefined' ? unsafeWindow : (typeof window !== 'undefined' ? window : globalThis))` 并使用 `fetchFn.call(targetWindow, url, options)`，确保底层 native fetch 的 `this` 始终为 `Window`，彻底规避 `Illegal invocation`。

### 2.2 帖子购买逻辑健壮化
- 改造 `getPostMetadata`：兼容 `read.php?tid-XXXX-page-Y.html`、`read.php?tid-XXXX.html`、`read.php?tid=XXXX` 等多种 URL 格式及 `window.location.href` 兜底。
- 移除 `run().catch(e => { window.location.reload(); })` 的粗暴全页刷新，改为在销售框内展示错误信息（`rinsp-buy-failed`），并展示“重试”与“原生购买”按钮。

### 2.3 暗黑模式与 Dark Reader 防冲突
- 修正第 4246 行 `color: color: var(--rinsp-dm-color-grey) !important;` 语法错误。
- 在 `applyDarkTheme` 中，当暗黑模式生效时，动态检查并添加 `<meta name="darkreader-lock">`；退出暗黑模式时移除。
- 补充 `:root` 的 `color-scheme: dark` 声明。

### 2.4 扩展功能实现
- **跨镜像域名设置同步**：将暗黑模式开关、主题偏好等常用设置无缝同步至 `GM_getValue / GM_setValue`。
- **长帖与图墙性能优化**：引入 `content-visibility: auto` 与 `contain-intrinsic-size` 规则，极大减少长列表渲染开销。
- **快捷键**：增加 `J`/`K` 快捷下一页/上一页（在非输入框焦点状态）。
