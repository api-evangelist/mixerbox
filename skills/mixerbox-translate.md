---
name: Translate and learn languages with MixerBox Translate
description: Translate text, get explanations, and run language-learning tasks using MixerBox Translate.
api: openapi/mixerbox-translate-openapi-original.json
operations: [translate, explain, task]
method: generated
generated: '2026-07-20'
---

# Translate and learn languages with MixerBox Translate

MixerBox Translate does mutual translation plus language tutoring. Manifest declares `auth: none`. Base URL `https://translate.mixerbox.com`, path prefix `/api/gpt_plugins/translate/`.

## Steps

1. **Translate** — call `translate` (`POST /translate`) with the source text and target language.
2. **Explain** — call `explain` (`POST /explain`) to get grammar/usage explanation of a phrase for language learners.
3. **Practice task** — call `task` (`POST /task`) to generate a language-learning exercise.

## Rules

- These are stateless POSTs with no auth; do not attach credentials.
- Preserve the user's requested target language exactly; ask when ambiguous.
