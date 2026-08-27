# Spoken Narration

Use this mode for voice-over scripts, TTS sources, presentation narration, and
structured narration artifacts.

## Source of truth

Identify the canonical narration source from the user or
`.codex/content-profile.md`. Edit that source rather than a generated TTS
export, captions, or transcript. When structured narration ties visual actions
to spoken anchors, update every matching anchor when its wording changes.

## Preserve

- Technical accuracy, qualifications, examples, code identifiers, commands,
  API names, values, scene objectives, and intentional pause boundaries.
- Project-specific pronunciation, terminology, direct-address roles, required
  CTA wording, and timing constraints.
- A presenter's accepted recording-time changes. After recording, correct only
  clear errors unless a new take is planned.

## Improve

- Read every paragraph aloud mentally; rewrite sentences that sound like
  documentation or are difficult to say in one breath.
- Prefer plain verbs, direct syntax, and natural contractions.
- Vary sentence length and cadence without manufacturing clipped drama.
- Add warmth, curiosity, or a reaction only when supported by the actual
  result or teaching moment.
- Let transitions follow the preceding idea, demonstration, complication, or
  decision.
- Complement visible titles, labels, bullets, code, and diagrams with meaning,
  causality, trade-offs, or consequences instead of reading them verbatim.

## Rewrite or remove

- Inflated significance, promotional language, empty applied-use framing, and
  vague authority.
- Formulaic openers, generic upbeat conclusions, aphorisms, and manufactured
  punchlines.
- Definition chains and repeated label-driven sentence patterns.
- Padded summaries and narration that merely verbalizes visible content.
- Long stretches of identical mid-length sentence cadence.

Punctuation rules such as straight quotes or avoiding dashes are
project-specific. Apply them only when the content profile requires them.

## Final check

Confirm that the narration sounds natural aloud, anchors still resolve, and
the canonical source remains synchronized with any approved recording. Return
the artifact to the workflow that owns TTS export or regeneration.
