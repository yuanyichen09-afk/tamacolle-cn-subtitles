# 魂これ 中文字幕插件（Tamacolle CN Subtitles）

《魂これ》网页版的中文字幕用户脚本：播放角色语音时在游戏画面上叠加整条中文字幕，不改动游戏文件。

- 当前版本：**v1.1.3**
- 字幕库：**2,538 条**
- 战斗规则：战斗画面**只**叠加「战斗负伤（服装破损）」语音的中文字幕；攻击、拔魂技、普通受击等其他战斗语音照常播放，不出字幕。
- 平时触摸、编队、庄园、购买等原有字幕规则不变。

本仓库只包含三份发布材料：可安装的用户脚本、更新元数据、本说明。

## 固定安装链接

装一次这个链接即可，以后新版都从同一地址更新，不用再换链接：

**https://raw.githubusercontent.com/yuanyichen09-afk/tamacolle-cn-subtitles/main/Tamacolle_CN_Subtitles.user.js**

- 更新元数据（脚本管理器自动检查用）：
  https://raw.githubusercontent.com/yuanyichen09-afk/tamacolle-cn-subtitles/main/Tamacolle_CN_Subtitles.meta.js
- 仓库主页：https://github.com/yuanyichen09-afk/tamacolle-cn-subtitles

仓库是公开的，下载和安装都不需要 GitHub 账号。

## 安装说明（三端）

### iPhone / iPad

1. 在 Safari 里从 App Store 安装扩展 **Userscripts**（免费）。
2. 打开「设置 → Safari → 扩展」，启用 Userscripts，并允许它访问 `raw.githubusercontent.com`。
3. 用 Safari 打开上面的固定 `.user.js` 链接。
4. 点地址栏的扩展图标打开 Userscripts，按提示点安装；保存后回到游戏页面刷新。

### 电脑

1. 在 Chrome / Edge / Firefox 里安装 **Tampermonkey**（或 Violentmonkey）。
2. 确认扩展已启用，用浏览器打开同一个固定 `.user.js` 链接。
3. Tampermonkey 会弹出安装页，点「安装」；之后刷新游戏页面。

### 安卓

1. 安装 **Firefox for Android**，在扩展里安装 **Tampermonkey** 并启用。
2. 用 Firefox 打开同一个固定 `.user.js` 链接，在 Tampermonkey 的安装页确认安装。
3. 如果浏览器直接把源码显示出来、没有弹出安装页：打开 Tampermonkey → 添加新脚本 → 用「从 URL 导入 / Utilities → Import from URL」，填入同一个 `.user.js` 地址导入；或把源码全选复制，粘贴覆盖到新建脚本里保存。

安装后在 <https://nijitama.app/games/tamacolle/> 刷新页面即可看到字幕。

## 从旧版升级

v1.1.2 及更早的脚本里**没有** `@updateURL` / `@downloadURL`，脚本管理器不会自动发现这个仓库，所以必须手动迁移一次：

1. 先在脚本管理器里**停用**（或删除）旧版脚本，避免两份脚本同时运行、字幕重复叠加。
2. 用上面的固定 `.user.js` 链接安装一次 v1.1.3。
3. 刷新游戏页面。

从 v1.1.3 起元数据里已带更新地址，以后新版会自动检查更新。

## 自动更新说明

- 脚本头部含 `@updateURL`（指向 `.meta.js`）和 `@downloadURL`（指向 `.user.js`），两者与实际仓库的 Raw 地址一致。
- **Tampermonkey**（电脑 / 安卓）：默认约每 12 小时检查一次更新，可在「设置 → 更新」里调整或关闭。想立刻拿到新版：打开 Tampermonkey 面板 → 「已安装脚本」→ 该脚本 → 「检查更新」（或面板里的「检查脚本更新」）。
- **Userscripts（iOS/iPadOS）**：iOS 不允许后台常驻，更新通常在打开 Userscripts 扩展界面时（或手动下拉刷新脚本列表）才检查；不会像电脑那样定时静默更新。若扩展内提示有更新，点一下确认即可。
- 如果某端只弹出「有可用更新」提示而不自动装：按提示手动确认一次即可，这属于该扩展的保守策略，不是脚本问题。
- 想核对版本：脚本管理器里显示的版本号应为 `1.1.3`，与 `.meta.js` 中的 `@version` 一致。

## 发布新版本（维护流程）

以后发新版，保持**同一分支、同一路径、同一文件名**，玩家的固定链接才不会失效：

1. 在 `D:\Codex` 下用既有构建流程生成新的 `.user.js`（v1.1.3 的发布副本由 `D:\Codex\Tamacolle_v113_work\make_publish_copy.cjs` 生成：它只在元数据头插入/保留更新地址，正文与字幕库逐字节不动）。
2. **提高** `@version`（例如 `1.1.4`），并同步更新脚本内 `const VERSION`（如果有）。
3. **重新生成** `.meta.js`：内容必须是新版脚本完整元数据头的拷贝，`@version` 与 `.user.js` 完全一致。
4. 在**同一次提交**里同时更新 `Tamacolle_CN_Subtitles.user.js` 和 `Tamacolle_CN_Subtitles.meta.js`，然后推送到 `main`。两者版本不一致会导致脚本管理器反复提示更新或判定失败。
5. 推送前自检：
   - 两个文件的 `@version` 相同；
   - `.meta.js` 只含元数据头、不含正文；
   - `.user.js` 结尾是 `.user.js`、`.meta.js` 结尾是 `.meta.js`；
   - 用 `node --check Tamacolle_CN_Subtitles.user.js` 通过语法检查；
   - 字幕库条目数与 `audio_subtitle_sha256` 未被意外改动。
6. 推送后匿名访问两个 Raw 地址核对内容与版本号（见下）。

## 校验

- 发布前基线：2,538 条字幕，`audio_subtitle_sha256 = 92e69d7e69af6ec170e5745ffe8f9caf7f7f6d625d67f8e42de689a05a7f70b5`，战斗负伤文件 34 个。
- 发布副本与 D 盘原版（`D:\Codex\Tamacolle_CN_Subtitles_v1.1.3\Tamacolle_CN_Subtitles_v1.1.3.user.js`，保留作备份）相比，仅元数据头多出 `@updateURL`、`@downloadURL` 两行。
- 匿名访问（未登录、无 Cookie）两个 Raw 地址应返回脚本与元数据，且版本号均为 `1.1.3`。
