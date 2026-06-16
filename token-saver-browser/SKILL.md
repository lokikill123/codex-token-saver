---
name: token-saver-browser
description: "Browser automation with extreme token saving. No screenshots/DOM/docs. One bootstrap per session. Violation = immediate stop."
---

# Token-Saver Browser v2 (STRICT)

## Init (once per session, no docs read)
```js
const { setupBrowserRuntime: _s } = await import("file:///C:/Users/lokik/.codex/plugins/cache/openai-bundled/browser/26.609.41114/scripts/browser-client.mjs");
await _s({ globals: globalThis });
globalThis.browser = await agent.browsers.get("iab");
```

## Ops Template (max cache hit)

### Navigate (1 js call with confirm)
```js
var _t = (await browser.tabs.list())[0] || await browser.tabs.new({url:"ABOUT:BLANK"});
if (!(await _t.url()).includes("DOMAIN")) await _t.goto("URL",{timeoutMs:15000});
// confirm: await _t.title()
```

### Act (single evaluate for everything)
```js
_t.playwright.evaluate(() => {
  // click + type + read all in one function
  var btn = document.querySelector("BUTTON_SELECTOR");
  if(btn) btn.click();
  document.querySelector("INPUT_SELECTOR")?.focus();
  return {ok:1, url:location.href};
});
```

## Hard Rules (stop on violation)
- NO screenshot (50K token each) unless user says "screenshot"
- NO domSnapshot - use evaluate instead
- NO retry >1 on same target
- NO 2+ js calls for same page
- NO reading SKILL.md >30 lines
- NO js_reset (unless kernel crash)
- NO CDP/Chrome/ComputerUse switching
- NO agent.documentation / browser.documentation

## Fail-fast
Any op fails once = tell user, don't switch method.
Node REPL crash = tell user, fall back to Shell.
