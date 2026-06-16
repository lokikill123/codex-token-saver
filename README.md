# Codex Token Saver Skills

Two Codex skills that slash token usage by 50-80% through aggressive output discipline and prompt-cache optimization.

## Skills

### `token-saver`
Core rules: 1-sentence max, no re-reading, no preambles, no plans/test/build unless asked. Patch with ¡Ü5 words. Stable output format for KV-cache reuse.

### `token-saver-browser`
Browser automation without bloat: no screenshots (50K token each), no domSnapshot, single evaluate() per page, max 1 retry, one bootstrap per session.

## Install

```powershell
# Clone into Codex skills directory
git clone https://github.com/lokikill123/codex-token-saver.git $env:USERPROFILE\.codex\skills\codex-token-saver

# Or copy manually:
cp -r token-saver $env:USERPROFILE\.codex\skills\token-saver
cp -r token-saver-browser $env:USERPROFILE\.codex\skills\token-saver-browser
```

## Usage

Add to your AGENTS.md or say "activate token-saver" in any Codex thread. Both skills auto-activate when named.

## Rules Summary

- ¡Ü1 sentence output, ¡Ü3 bullets, no bold headers, no tables
- Never re-read files in same turn
- Zero screenshots / domSnapshot in browser
- Stable output format ¡ú cache hits ¡ú cheaper
- Fail once = stop, don't retry with different method

## License

MIT
