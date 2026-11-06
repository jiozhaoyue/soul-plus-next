# Quality Guidelines

> Code quality standards for frontend development.

---

## Overview

This repository maintains three synchronized variants of the SouthPlus userscript (`南加北加论坛强化脚本(凛+)` v100):
- `南加北加论坛强化脚本(凛%2B).original.user.js`: Unmodified upstream baseline by 遠坂凛.
- `南加北加论坛强化脚本(凛%2B).bugfix.user.js`: Minimal-invasion bugfix-only variant preserving upstream authorship and structure.
- `南加北加论坛强化脚本(凛%2B).user.js`: Enhanced variant (`@author jiozhaoyue`) whose bugfix hunks must remain 100% identical to `.bugfix.user.js`.

---

## Forbidden Patterns

- **Unbound global `fetch()` in userscript sandboxes**: Calling bare `fetch(url, options)` when `@grant unsafeWindow` is enabled loses the `Window` receiver (`this`) under browser hooks (such as Edge `loginCaptureHook.js`), throwing `TypeError: Failed to execute 'fetch' on 'Window': Illegal invocation`.
- **Invasive rewrites for bugfixes**: Do not rewrite helper functions (like `getPostMetadata` or `enhanceBuyButtons`) or introduce top-level wrapper functions when a 1–5 line inline fix in the existing function (`fetchWithRetry`, `applyDarkTheme`, `executeBackgroundBuy`) resolves the root cause.

---

## Required Patterns

- **Explicit `Window` binding in `fetchWithRetry`**:
  ```javascript
  const win = (typeof unsafeWindow !== 'undefined' && unsafeWindow) ? unsafeWindow : window;
  const response = await win.fetch.call(win, url, options);
  ```
- **Bugfix Parity**: Every bugfix applied to `南加北加论坛强化脚本(凛%2B).bugfix.user.js` must be identical line-for-line in `南加北加论坛强化脚本(凛%2B).user.js`.

---

## Testing Requirements

- Run `node --check` on all `.user.js` variants after any edit.
- Verify `unified_diff(original, bugfix)` contains only the minimal bugfix hunks, and `unified_diff(bugfix, enhanced)` contains only `@author` and enhancement hunks.

