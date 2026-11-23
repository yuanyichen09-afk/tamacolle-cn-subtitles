# 魂これ 中文字幕插件（Tamacolle CN Subtitles）

《魂これ》网页版的中文字幕用户脚本：播放角色语音时在游戏画面上叠加整条中文字幕，不改动游戏文件。

- 当前版本：**v1.1.4**
- 字幕库：**2,538 条**（与 v1.1.3 完全一致，未重新生成）
- 战斗规则：战斗画面**只**叠加「战斗负伤（服装破损）」语音的中文字幕；攻击、拔魂技、普通受击等其他战斗语音照常播放，不出字幕。
- 平时触摸、编队、庄园、购买等原有字幕规则不变。

本仓库只包含三份发布材料：可安装的用户脚本、更新元数据、本说明。

## v1.1.4 改了什么

- 匹配规则从三条具体网址改为 `@match *://*/*`，让脚本能出现在更多 Safari **Userscripts 的网页匹配面板**里。
- 代价是脚本会被注入到所有网页，因此**执行入口先检查当前网址**：只读 `location`，
  非《魂これ》游戏页立即 `return`，不创建字幕层、不读写存储、不发请求、不挂定时器。
- 只有这两个域名会真正启动字幕引擎：
  - `https://nijitama.app/games/tamacolle/…`（含 `*.nijitama.app` 子域）
  - `https://tukitama.com/tamacolle/…`
- 其余一切页面（含 `http://` 版本、相似域名如 `nijitama.app.example.org`、`fakenijitama.app`、`tukitama.com.evil.com`）都只做一次网址判断后退出。
- 脚本名称、`@namespace`、字幕数据库、音频映射、显示逻辑、自动更新地址全部保持不变。

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
2. 打开「设置 → Safari → 扩展」，启用 Userscripts，并把网站访问权限设为**允许**（至少对 `raw.githubusercontent.com` 与 `nijitama.app` 允许）。是否显示在面板里也取决于这个许可。
3. 用 Safari 打开上面的固定 `.user.js` 链接。
4. 点地址栏的扩展图标打开 Userscripts，按提示点安装；保存后回到游戏页面刷新。
5. 因为 v1.1.4 用的是 `*://*/*`，该脚本会出现在 Userscripts 的多个网页匹配列表里——这是预期行为，只有游戏页才会真的运行字幕。

### 电脑

1. 在 Chrome / Edge / Firefox 里安装 **Tampermonkey**（或 Violentmonkey）。
2. 确认扩展已启用，用浏览器打开同一个固定 `.user.js` 链接。
3. Tampermonkey 会弹出安装页，点「安装」；之后刷新游戏页面。

> 装了 v1.1.4 后，Tampermonkey 会在很多网站上注入这个脚本（因为 `*://*/*`），但它只做一次网址判断就退出，不影响页面。若你只想让它在游戏页运行，可在 Tampermonkey 里把该脚本的「用户匹配 / User matches」限制到上述两个域名（属于可选优化，不影响功能）。

### 安卓

1. 安装 **Firefox for Android**，在扩展里安装 **Tampermonkey** 并启用。
2. 用 Firefox 打开同一个固定 `.user.js` 链接，在 Tampermonkey 的安装页确认安装。
3. 如果浏览器直接把源码显示出来、没有弹出安装页：打开 Tampermonkey → 添加新脚本 → 用「从 URL 导入 / Utilities → Import from URL」，填入同一个 `.user.js` 地址导入；或把源码全选复制，粘贴覆盖到新建脚本里保存。

安装后在 <https://nijitama.app/games/tamacolle/> 刷新页面即可看到字幕。

## 从旧版升级

v1.1.2 及更早的脚本里**没有** `@updateURL` / `@downloadURL`，脚本管理器不会自动发现这个仓库，所以必须手动迁移一次：

1. 先在脚本管理器里**停用**（或删除）旧版脚本，避免两份脚本同时运行、字幕重复叠加。
2. 用上面的固定 `.user.js` 链接安装一次最新版。
3. 刷新游戏页面。

从 v1.1.3 起元数据里已带更新地址，之后新版会自动检查更新。

## 自动更新说明

- 脚本头部含 `@updateURL`（指向 `.meta.js`）和 `@downloadURL`（指向 `.user.js`），两者与实际仓库 Raw 地址一致，v1.1.4 继续沿用。
- **Tampermonkey**（电脑 / 安卓）：默认约每 12 小时检查一次更新，可在「设置 → 更新」里调整或关闭。想立刻拿到新版：打开 Tampermonkey 面板 → 「已安装脚本」→ 该脚本 → 「检查更新」（或面板里的「检查脚本更新」）。
- **Userscripts（iOS/iPadOS）**：iOS 不允许后台常驻，更新通常在打开 Userscripts 扩展界面时（或手动下拉刷新脚本列表）才检查；不会像电脑那样定时静默更新。若扩展内提示有更新，点一下确认即可。
- 如果某端只弹出「有可用更新」提示而不自动装：按提示手动确认一次即可，这属于该扩展的保守策略，不是脚本问题。
- 想核对版本：脚本管理器里显示的版本号应为 `1.1.4`，与 `.meta.js` 中的 `@version` 一致。

## 发布新版本（维护流程）

以后发新版，保持**同一分支、同一路径、同一文件名**，玩家的固定链接才不会失效：

1. 在 `D:\Codex` 下用既有构建流程生成新的 `.user.js`（**不要**手工改字幕库，也不要重新生成数据库除非确实需要）。
2. **提高** `@version`（例如 `1.1.5`），并同步脚本内 `const VERSION`。
3. 确认 `@updateURL` / `@downloadURL` 仍指向本仓库 Raw 地址。
4. **重新生成** `.meta.js`：内容必须是新版脚本完整元数据头的拷贝，`@version` 与 `.user.js` 完全一致。
5. 在**同一次提交**里同时更新 `Tamacolle_CN_Subtitles.user.js` 和 `Tamacolle_CN_Subtitles.meta.js`，然后推送到 `main`。两者版本不一致会导致脚本管理器反复提示更新或判定失败。
6. 推送前自检：
   - 两个文件的 `@version` 相同；
   - `.meta.js` 只含元数据头、不含正文；
   - `.user.js` 以 `.user.js` 结尾、对应 `@downloadURL`；`.meta.js` 以 `.meta.js` 结尾、对应 `@updateURL`；
   - `node --check Tamacolle_CN_Subtitles.user.js` 通过；
   - 字幕条目数与 `audio_subtitle_sha256` 未被意外改动；
   - 入口网址判断仍在字幕初始化之前。
7. 推送后匿名访问两个 Raw 地址核对内容与版本号。

## 校验

- 字幕库：2,538 条，`audio_subtitle_sha256 = 92e69d7e69af6ec170e5745ffe8f9caf7f7f6d625d67f8e42de689a05a7f70b5`（与 v1.1.3 相同）。
- 战斗负伤文件 34 个，集合未变。
- 相对 v1.1.3，正文只多了入口网址判断 7 行（另加一个空行）；其余差异仅 `@version`、`const VERSION`、`DB_META` 说明里的版本号。
- 入口守卫已对 24 条 URL 做矩阵验证：两个正式域名（含 `*.nijitama.app` 子域）启动，17 类非游戏页面全部立即退出且零触碰页面能力。
- 匿名访问（未登录、无 Cookie）两个 Raw 地址应返回脚本与元数据，版本号均为 `1.1.4`。
