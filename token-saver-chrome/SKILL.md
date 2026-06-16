---
name: token-saver-chrome
description: Chrome操作极致省token。复用连接、var绑定、PowerShell导航、SendKeys上传。一次成功不重试。违反即停。
---

# Token-Saver Chrome (STRICT)

## 连接（全session一次）
```js
// 先用shell找到最新路径：
// Get-ChildItem "$env:USERPROFILE\.codex\plugins\cache\openai-bundled\chrome" -Recurse -Filter "browser-client.mjs" | Select -First 1 FullName
var { setupBrowserRuntime: _bx } = await import("file:///最新路径");
await _bx({ globals: globalThis });
var _b = await agent.browsers.get("extension");
```

## 铁律
- **var 绑定**：所有跨 js 调用的引用用 var，不用 const
- **导航**：只走 PowerShell `Start-Process "chrome" -ArgumentList "URL"`，然后 claimTab
- **上传**：click file input → PowerShell `Set-Clipboard + SendKeys ^v + {ENTER}`
- **写内容**：先 evaluate 查 contenteditable/input → locator fill
- **不重连**：连接一次用全程，不反复 import
- **不读文档**：不读 browser.documentation()，不读 troubleshooting
- **内容类型**：优先图文/视频，不试文章（需要封面图）
- **只点按钮**：用 getByRole/getByText/locator，别用 evaluate 触发事件

## 失败即停
操作失败1次→告知用户，不换方法。extension连接失败→告知用户打开Chrome窗口。
