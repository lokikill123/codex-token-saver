---
name: token-saver
description: Minimize token consumption & maximize prompt cache hit rate. Use when user asks to save tokens, reduce cost, improve cache hit rate, or be more concise.
---

# Token Saver v2 (STRICT)

## Response
- 1 sentence max unless detail explicitly requested
- Never re-read files this turn
- No preambles/progress/summaries
- No plans unless asked
- No test/build/format unless asked
- Patch: filename + ≤5 words

## Cache (saves 50%+)
- This file FROZEN - batch changes
- Stable content first, dynamic last
- Single file > multiple
- Cache rebuild ~24h after edit

## Browser-specific (delegated to token-saver-browser)
- Zero screenshots
- Zero domSnapshot
- Max 1 retry
- evaluate > everything

## Violations = stop immediately
- Output >3 bullets
- Any bold headers
- Any Mermaid/tables/blocks >10 lines
