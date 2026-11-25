# 魂これ 中文字幕插件（Tamacolle CN Subtitles）

《魂これ》网页版的中文字幕用户脚本：播放角色语音时在游戏画面上叠加整条中文字幕，不改动游戏文件。

- 当前版本：**v1.1.9**
- 字幕库：**2,608 条**（新增 28 条入浴字幕）
- 战斗规则：队长出发、我方遇敌、释放拔魂技和战斗负伤（服装破损）时显示中文字幕。普通攻击、普通受击、寻宝和陷阱等照常播放语音。
- 平时触摸、编队、庄园、购买等原有字幕规则不变。

本仓库只包含三份发布材料：可安装的用户脚本、更新元数据、本说明。

## v1.1.9 更新

字幕采用纯黑粗体无衬线字和细浅色描边，去掉底框。字幕继续整句显示。

## v1.1.8 更新

补入确认入浴时播放的 28 条语音字幕。字幕脚本通过实际播放入口识别语音文件，避免把预加载资源的台词错配给按钮音效。原有字幕、战斗显示规则和固定安装地址沿用 v1.1.7。

## v1.1.7 更新

岩代已知 53 条语音均有中文字幕。新增队长出发、我方遇敌、释放拔魂技、战斗负伤，以及任务、浴室、庄园和个室等语音。沿用 v1.1.6 的显示规则和固定安装地址。

## v1.1.6 更新

恢复队长出发、我方遇敌和释放拔魂技时的字幕。网站匹配规则继续沿用 v1.1.5。

## v1.1.5 改了什么（撤销全网页匹配）

v1.1.4 曾把匹配规则改成 `@match *://*/*`，想让脚本出现在更多 Safari Userscripts 面板里。实际后果是 **Tampermonkey 会在所有网站把它当成匹配脚本注入**，影响日常浏览，因此 v1.1.5 撤销该方案：

- `@match` 恢复为 v1.1.3 的三条游戏域名规则：
  - `https://nijitama.app/games/tamacolle/*`
  - `https://*.nijitama.app/games/tamacolle/*`
  - `https://tukitama.com/tamacolle/*`
- 非游戏网站**不再匹配**本脚本，Tampermonkey 不会注入，也不会出现在「匹配脚本」列表里。
- 版本号升到 **1.1.5**，与已发布的 v1.1.4 区分；已经装了 v1.1.4 的用户更新到 1.1.5 后，全网页匹配会自动消失，无需卸载重装。
- 脚本内的**游戏网址守卫保留**，作为运行期兜底（例如 `http://` 版本、以后误改匹配规则时仍不会在游戏外启动字幕）。
- 字幕数据库、音频映射、显示逻辑、`@name`、`@namespace`、`@updateURL`、`@downloadURL` 全部保持不变。

> 已经装了 v1.1.4 的话：打开 Tampermonkey 面板 → 该脚本 → 「检查更新」，或在约 12 小时内等它自动检查，即可升到当前版本。

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
2. 打开「设置 → Safari → 扩展」，启用 Userscripts，并允许它访问 `raw.githubusercontent.com` 与游戏域名（`nijitama.app`、`tukitama.com`），否则脚本不会在游戏页运行。
3. 用 Safari 打开上面的固定 `.user.js` 链接。
4. 点地址栏的扩展图标打开 Userscripts，按提示点安装；保存后回到游戏页面刷新。

> 当前版本只在上述三条游戏域名下匹配，因此 Userscripts 里它只出现在这些网站的匹配范围内。这是刻意的取舍：匹配面板覆盖面变小，但不干扰其它网站。

### 电脑

1. 在 Chrome / Edge / Firefox 里安装 **Tampermonkey**（或 Violentmonkey）。
2. 确认扩展已启用，用浏览器打开同一个固定 `.user.js` 链接。
3. Tampermonkey 会弹出安装页，点「安装」；之后刷新游戏页面。
4. 装好后在 Tampermonkey 的「已安装脚本」里应只看到它在 `nijitama.app` / `tukitama.com` 上生效。

### 安卓

1. 安装 **Firefox for Android**，在扩展里安装 **Tampermonkey** 并启用。
2. 用 Firefox 打开同一个固定 `.user.js` 链接，在 Tampermonkey 的安装页确认安装。
3. 如果浏览器直接把源码显示出来、没有弹出安装页：打开 Tampermonkey → 添加新脚本 → 用「从 URL 导入 / Utilities → Import from URL」，填入同一个 `.user.js` 地址导入；或把源码全选复制，粘贴覆盖到新建脚本里保存。

安装后在 <https://nijitama.app/games/tamacolle/> 刷新页面即可看到字幕。

## 从旧版升级

- **v1.1.4 → 当前版本**：直接检查更新即可，匹配规则会自动收回，无需重装。
- **v1.1.2 及更早**：这些脚本里**没有** `@updateURL` / `@downloadURL`，脚本管理器不会自动发现本仓库，必须手动迁移一次：
  1. 先在脚本管理器里**停用**（或删除）旧版，避免两份脚本同时运行、字幕重复叠加；
  2. 用上面的固定 `.user.js` 链接安装一次最新版；
  3. 刷新游戏页面。

## 自动更新说明

- 脚本头部含 `@updateURL`（指向 `.meta.js`）和 `@downloadURL`（指向 `.user.js`），两者与实际仓库 Raw 地址一致，v1.1.9 继续沿用。
- **Tampermonkey**（电脑 / 安卓）：默认约每 12 小时检查一次更新，可在「设置 → 更新」里调整或关闭。想立刻拿到新版：打开 Tampermonkey 面板 → 「已安装脚本」→ 该脚本 → 「检查更新」（或面板里的「检查脚本更新」）。
- **Userscripts（iOS/iPadOS）**：iOS 不允许后台常驻，更新通常在打开 Userscripts 扩展界面时（或手动下拉刷新脚本列表）才检查；不会像电脑那样定时静默更新。若扩展内提示有更新，点一下确认即可。
- 如果某端只弹出「有可用更新」提示而不自动装：按提示手动确认一次即可，这属于该扩展的保守策略，不是脚本问题。
- 想核对版本：脚本管理器里显示的版本号应为 `1.1.9`，与 `.meta.js` 中的 `@version` 一致。

## 发布新版本（维护流程）

以后发新版，保持**同一分支、同一路径、同一文件名**，玩家的固定链接才不会失效：

1. 在 `D:\Codex` 下用既有构建流程生成新的 `.user.js`（**不要**手工改字幕库，也不要重新生成数据库除非确实需要）。
2. **提高** `@version`（例如 `1.1.9`），并同步脚本内 `const VERSION`。
3. 确认 `@updateURL` / `@downloadURL` 仍指向本仓库 Raw 地址。
4. **重新生成** `.meta.js`：内容必须是新版脚本完整元数据头的拷贝，`@version` 与 `.user.js` 完全一致。
5. 在**同一次提交**里同时更新 `Tamacolle_CN_Subtitles.user.js` 和 `Tamacolle_CN_Subtitles.meta.js`，然后推送到 `main`。两者版本不一致会导致脚本管理器反复提示更新或判定失败。
6. 推送前自检：
   - 两个文件的 `@version` 相同；
   - `.meta.js` 只含元数据头、不含正文；
   - `@match` 只有上述三条游戏域名（**不要**再用 `*://*/*`）；
   - `node --check Tamacolle_CN_Subtitles.user.js` 通过；
   - 字幕条目数与 `audio_subtitle_sha256` 未被意外改动；
   - 入口网址判断仍在字幕初始化之前。
7. 推送后匿名访问两个 Raw 地址核对内容与版本号。

## 校验

- 字幕库：2,608 条。与 v1.1.8 的 2,608 条字幕及时间轴一致。
- 战斗负伤映射新增岩代。
- v1.1.5 相对 v1.1.4 改了四处：`@match` 三条规则、`@version`、`const VERSION`、`DB_META` 说明里的版本号；其余逐字节未动（反向还原后与 v1.1.4 完全相同）。
- `@match` 用 match-pattern 语义验证：10 条游戏网址匹配；30 条非游戏网址（GitHub、Google、YouTube、B 站、游戏主域的其它路径、相似/伪造域名、`http://`、`file://`、路径相似等）**全部不匹配**。
- 入口守卫独立验证仍生效：游戏页放行，外站与 `http://` 拦截，且外站运行时零触碰页面能力。
- 项目自带 `node --test source/runtime.test.cjs`：22/22 通过，包含入浴和预加载误弹字幕的回归测试。PC 和 iPhone 实机待复测。
- 匿名访问（未登录、无 Cookie）两个 Raw 地址应返回脚本与元数据，版本号均为 `1.1.9`。
