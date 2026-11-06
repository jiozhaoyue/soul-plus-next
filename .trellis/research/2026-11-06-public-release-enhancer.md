# Public Release, Upstream Alignment, and v101 Enhancements

> Date: 2026-11-06
> Author: jiozhaoyue

## 1. Upstream Audit & Verification
- Checked upstream GreasyFork/SleazyFork script 454120 (author: tousakarin / 遠坂凛). Verified that upstream version remains at v100.
- Checked upstream origin Chrome extension repository `FetchTheMoon/soul-plus-plus-chrome-extension`. Extension remains dormant.
- Local `southplus-enhancer.original.user.js` matches upstream v100 baseline.

## 2. File Naming Standardisation (English userscript naming)
- Refactored user-facing scripts to standard English names to avoid URL encoding (`%2B`) and cross-platform path issues:
  - `南加北加论坛强化脚本(凛+).user.js` -> `southplus-enhancer.user.js` (Enhanced v101)
  - `南加北加论坛强化脚本(凛+).bugfix.user.js` -> `southplus-enhancer.bugfix.user.js` (Minimal bugfix)
  - `南加北加论坛强化脚本(凛+).original.user.js` -> `southplus-enhancer.original.user.js` (Original upstream v100)

## 3. Bug Fixes & Enhancements (v101)
- **Draft Cleanup Fix**: In refresh-free background reply (`executeBackgroundReply`), the native form submit event was intercepted, leaving draft keys in `localStorage`. In v101, upon successful reply, `document.FORM.atc_content` dispatches an `input` event and explicitly purges `rinsp-draft-tid-*` and `rinsp-draft-common`.
- **Keyboard Shortcut Overlay Suppression**: In `initKeyboardShortcutsAndDraft`, `J`/`K` navigation now checks for open modals (`.rinsp-picwall-overlay`, `.rinsp-dialog:not(.hidden)`, `.rinsp-modal`) to avoid unintentional background page jumping while viewing images or configuring settings.
- **Deep Cross-Mirror Sync**: `createLocalStorageProperty` now prioritizes `GM_getValue` as the single source of truth across all mirror domains (`south-plus.net`, `soul-plus.net`, `white-plus.net`, etc.), falling back to `localStorage` when GM storage is empty.
- **Metadata Sanitization**: Removed upstream updateURL/downloadURL to prevent Tampermonkey from downgrading users to the unpatched upstream v100. Added bilingual metadata (`@name:zh-CN`, `@name:en`, `@description:zh-CN`, `@description:en`, `@supportURL`).

## 4. Repository Public Readiness
- Initialized clean Git repository with default branch `main`.
- Added `.gitignore` ignoring all AI agent workdirs (`.claude/`, `.cursor/`, `.gemini/`, etc.), IDE/OS files, and Trellis runtime caches while preserving `.trellis/spec/` and `.trellis/research/`.
- Created bilingual `README.md` and standard `LICENSE` (MIT).
- Provided script marketplace publishing guide for Sleazy Fork and ScriptCat.
