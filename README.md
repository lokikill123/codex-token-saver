# Codex Token Saver 技能（中文版）

两个 Codex 技能，通过极致输出约束和 prompt-cache 优化，节省 50-80% token 消耗。

## 技能

### `token-saver-zh` —— 核心省 token
零寒暄、零解释、零验证、禁重复读。改完只报文件路径。统一输出格式最大化 KV cache 复用。

### `token-saver-browser` —— 浏览器省 token
禁截图（每次 50K token）、禁 domSnapshot、单页面一次 evaluate 搞定、最多重试一次、全 session 一次 bootstrap。

## 安装

```powershell
git clone https://github.com/lokikill123/codex-token-saver.git $env:USERPROFILE\.codex\skills\codex-token-saver

# 或用原生目录名：
cp -r token-saver-zh $env:USERPROFILE\.codex\skills\token-saver-zh
cp -r token-saver-browser $env:USERPROFILE\.codex\skills\token-saver-browser
```

## 用法

在 AGENTS.md 中加入，或在对话中说 "激活 token-saver"。

## 核心规则

- 输出 ≤1 句，≤3 条要点，无加粗标题，无表格
- 同回合不重读文件
- 浏览器操作零截图、零 domSnapshot
- 稳定输出格式 → 缓存命中 → 省钱
- 任何操作失败一次即停，不换方法重试

## 适用场景

让 Codex 操作浏览器/Chrome 时自动激活 token-saver-browser，配合 token-saver 核心技能，实现浏览器自动化场景下最大化的 token 节省和缓存命中率。

## 许可

MIT
