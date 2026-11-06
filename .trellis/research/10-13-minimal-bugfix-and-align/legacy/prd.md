# Minimal-invasion bugfix version and align enhanced version

## Goal

1. 拉取原作者（遠坂凛）在 GreasyFork 上的 v100 原始源码，保存为原版基线文件 `南加北加论坛强化脚本(凛%2B).original.user.js`。
2. 基于原版源码，制作一个**最小侵入、仅修复存在的 Bug** 的版本 `南加北加论坛强化脚本(凛%2B).bugfix.user.js`（保持原作者署名不变）。
3. 将现有增强改版 `南加北加论坛强化脚本(凛%2B).user.js` 中的 Bug 修复部分收敛并对齐到与上述最小侵入 Bug 修复版完全一致（不删减任何已实现的扩展增强功能），同时将改版的 `@author` 改为 `jiozhaoyue`。

## Requirements

- **R1: 原版源码拉取与基线保存**
  - 从官方更新源 `https://update.greasyfork.org/scripts/454120/%E5%8D%97%E5%8A%A0%E5%8C%97%E5%8A%A0%E8%AE%BA%E5%9D%9B%E5%BC%BA%E5%8C%96%E8%84%9A%E6%9C%AC%28%E5%87%9B%2B%29.user.js` 拉取 v100 原始脚本（18,883 行），保存为 `南加北加论坛强化脚本(凛%2B).original.user.js`，零修改。
- **R2: 最小侵入单 Bug 修复版 (`南加北加论坛强化脚本(凛%2B).bugfix.user.js`)**
  - 基于原版 v100，仅包含以下 4 项最小侵入修复（共 5 处局部 diff，不含任何扩展功能，不改 `@author`）：
    1. `fetchWithRetry`（原版 18361 行）：绑定 `const win = (typeof unsafeWindow !== 'undefined' && unsafeWindow) ? unsafeWindow : window;` 并使用 `win.fetch.call(win, url, options)`，修复 `Illegal invocation` 及由此引发的购买失败刷新。
    2. 暗黑模式 CSS（原版 4246 行）：修复 `color: color: var(--rinsp-dm-color-grey) !important;` 语法错误。
    3. 暗黑模式防 Dark Reader 冲突（原版 4006 行 & 18233 行）：在 `html.rinsp-dark-mode` 增加 `color-scheme: dark;`，并在 `applyDarkTheme()` 内联动态注入/移除 `<meta name="darkreader-lock">`。
    4. 购买异常不强刷兜底（原版 12286 行）：保持 `getPostMetadata`、`enhanceBuyButtons` 及 `executeBackgroundBuy` 主流程 100% 原生不动，仅在 `run().catch(e => ...)` 中对非 `content outdated` 异常改为在 `sellframes` 显示 `.rinsp-buy-failed` 错误原因而不直接强刷页面。
- **R3: 现有改版 (`南加北加论坛强化脚本(凛%2B).user.js`) 对齐与署名更新**
  - 保留全部 4 项扩展增强功能（跨镜像域名 GM 配置同步、`content-visibility: auto` 性能优化、贤者模式 NSFW 防闪烁遮罩、`J`/`K` 快捷翻页与草稿自动保存恢复）。
  - 将其中的 Bug 修复代码收敛为与 `bugfix` 版 100% 一致的最小侵入实现（移除多余的 `safeFetch`、`updateDarkReaderLock` 独立函数及对 `getPostMetadata` / `enhanceBuyButtons` 的侵入修改）。
  - 将头部元数据 `@author` 修改为 `jiozhaoyue`。

## Acceptance Criteria

- [x] `南加北加论坛强化脚本(凛%2B).original.user.js` 与 GreasyFork 上游 v100 源码字节级一致（18,883 行）。
- [x] `南加北加论坛强化脚本(凛%2B).bugfix.user.js` 相比 `original` 仅有上述 5 处最小侵入 Bug 修复 diff，`@author` 仍为 `遠坂凛`。
- [x] `南加北加论坛强化脚本(凛%2B).user.js` 保留全部 4 项扩展增强功能，其 Bug 修复部分与 `bugfix` 版完全一致，且 `@author` 已更新为 `jiozhaoyue`。

