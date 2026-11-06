# Public Release, Upstream Alignment, and v101 Enhancements

> Date: 2026-11-06
> Author: jiozhaoyue

## 1. Upstream Audit & Verification
- Checked upstream GreasyFork/SleazyFork script 454120 (author: tousakarin / 遠坂凛). Verified that upstream version remains at v100.
- Checked upstream origin Chrome extension repository `FetchTheMoon/soul-plus-plus-chrome-extension`. Extension remains dormant.
- Local `southplus-enhancer.original.user.js` matches upstream v100 baseline.

## 2. Project & File Naming: SoulPlus-Next (魂+ Next)
- Directly referenced upstream heritage: `FetchTheMoon/soul-plus-plus-chrome-extension` (Soul++).
- Adopted distinct new project identity: `SoulPlus-Next` (`soul-plus-next`, 魂+ Next).
- Refactored user-facing scripts:
  - `soul-plus-next.user.js` (Enhanced v101)
  - `soul-plus-next.bugfix.user.js` (Minimal bugfix v100.1)
  - `soul-plus-next.original.user.js` (Original upstream v100 baseline)
- Updated `@name`, `@namespace`, `@updateURL`, `@downloadURL`, and `@homepageURL` to point to `jiozhaoyue/soul-plus-next`.

## 3. Bug Fixes & Enhancements (v101)
- **Draft Cleanup Fix**: In refresh-free background reply (`executeBackgroundReply`), the native form submit event was intercepted, leaving draft keys in `localStorage`. In v101, upon successful reply, `document.FORM.atc_content` dispatches an `input` event and explicitly purges `rinsp-draft-tid-*` and `rinsp-draft-common`.
- **Keyboard Shortcut Overlay Suppression**: In `initKeyboardShortcutsAndDraft`, `J`/`K` navigation now checks for open modals (`.rinsp-picwall-overlay`, `.rinsp-dialog:not(.hidden)`, `.rinsp-modal`) to avoid unintentional background page jumping while viewing images or configuring settings.
- **Deep Cross-Mirror Sync**: `createLocalStorageProperty` now prioritizes `GM_getValue` as the single source of truth across all mirror domains (`south-plus.net`, `soul-plus.net`, `white-plus.net`, etc.), falling back to `localStorage` when GM storage is empty.
- **Real-time Auto-update**: Userscripts include official `@updateURL` and `@downloadURL` on GitHub raw `main`, plus GitHub Actions release workflow for automated distribution.
- **Documentation Standards**: Strict zero-emoji policy applied across all documentation, metadata, and communications.

## 4. Repository Public Readiness
- Target repository: `jiozhaoyue/soul-plus-next` (Public).
- Added `.gitignore` ignoring all AI agent workdirs (`.claude/`, `.cursor/`, `.gemini/`, etc.), IDE/OS files, and Trellis runtime caches while preserving `.trellis/spec/` and `.trellis/research/`.
- Created bilingual `README.md` and standard `LICENSE` (MIT) with proper credits to FetchTheMoon and tousakarin.
- Configured GitHub Actions CI workflow `.github/workflows/release.yml`.
- Provided script marketplace publishing guide for Sleazy Fork and ScriptCat.
