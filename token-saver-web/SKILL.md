---
name: token-saver-web
description: 任何网站操作极致省token。一条路径到底、零盲试、零重复读。违反即停。
---

# Token-Saver Web (STRICT)

## 核心原则
**一次找对路径，一条路走到底。不试第二种方法。**

## 连接（全session一次）
```js
// Shell先跑一次找路径，记下来，不复读
// Get-ChildItem "$env:USERPROFILE\.codex\plugins\cache\openai-bundled\chrome" -Recurse -Filter "browser-client.mjs" | Select -First 1 FullName
var { setupBrowserRuntime: _bx } = await import("file:///路径");
await _bx({ globals: globalThis });
var _b = await agent.browsers.get("extension");
```

## 导航（唯一方式）
```
Shell: Start-Process "chrome" -ArgumentList "URL"
→ 等5秒 → openTabs → find tab → claimTab
```
不试 goto、evaluate location、tabs.new({url})、goBack。

## 查页面（一次 evaluate）
```js
var info = await tab.playwright.evaluate(() => {
  var inputs = document.querySelectorAll('input, textarea, [contenteditable]');
  return [...inputs].slice(0,10).map(el => ({
    tag: el.tagName, type: el.type,
    placeholder: el.getAttribute("placeholder")||"",
    contentEditable: el.getAttribute("contenteditable")||"",
    className: el.className.substring(0,30),
    visible: el.offsetParent!==null
  }));
});
```
不读 domSnapshot。不读文档。不读截图。

## 填内容（查到后用 locator）
```js
// 普通input
var box = tab.playwright.getByPlaceholder("placeholder");
await box.fill("内容");

// contenteditable
var editor = tab.playwright.locator('[contenteditable="true"].class名');
await editor.click({timeoutMs:3000});
await editor.fill("内容");
```
不试多种 selector。placeholder 优先。

## 上传文件（唯一方式）
```js
// 1. 点 file input
var fi = tab.playwright.locator('input[type="file"]');
await fi.click({timeoutMs:5000});

// 2. Shell 粘贴路径
// Set-Clipboard "路径"; SendKeys ^v; SendKeys {ENTER}
```
不试 setInputFiles、force click、evaluate click、拖拽、boundingBox。

## 点按钮
```js
tab.playwright.getByRole("button",{name:"按钮名",exact:true})
// 或
tab.playwright.getByText("按钮名")
```
一次 click。不试 evaluate dispatchEvent。

## 失败降级（最多2条路径）
路径1（首选）→ 失败 → 告知用户原因（≤1句）→ 用户说"换方法" → 路径2（备选）
- 路径2 失败 → 放弃，告知用户
- 总共最多2条路径，禁止盲目试第3种

## 铁律（违反即停）
- var 绑定，不用 const
- 导航只走 Shell+openTabs+claimTab
- 查页面只走一次 evaluate，不读 domSnapshot/文档/截图
- 上传只走 click file input + Shell SendKeys
- 操作失败 → 告知原因 → 用户确认后走路径2 → 再败则停
- 不重试同一 selector
- 不读 SKILL.md >30 行
- 不反复重连
