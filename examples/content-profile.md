# Content Profile

## Audience and voice

- Audience: practitioners who understand the field's basics
- Voice: direct, practical, calm, and technically precise
- Preserve established terminology from the source repository

## Sources

- Public implementation: `../public-project`
- Supporting drafts and production material: current repository
- Treat public code and explicitly identified source documents as authoritative

## Medium articles

- Output: `<domain>/<topic>/article.md`
- Hero image: `<domain>/<topic>/hero-<slug>.png`
- Link directly to the relevant public implementation
- Keep configurable prices, thresholds, and assumptions clearly labeled

## Narration

- Canonical source: `productions/<name>/narration/narration.json`
- Generated TTS export: `productions/<name>/narration/tts-script.txt`
- Edit the canonical source; do not edit the generated export directly
- Preserve action anchors when changing their spoken wording

## Validation

- Verify code examples against the public implementation
- Check volatile claims against primary sources
- Validate links and generated artifacts before approval
