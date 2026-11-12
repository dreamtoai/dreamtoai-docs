# DreamTo API docs — agent instructions

Mintlify site (`docs.json`, MDX pages). Chinese is the default language; every page has an English counterpart under `en/`.

## Generated files — never edit by hand

- `openapi/zh.json`, `openapi/en.json`
- `video/seedance-2-0/scenarios/*.mdx` and `en/video/seedance-2-0/scenarios/*.mdx`

They are generated from the DreamTo Gateway source code, and any hand edit is overwritten on the next generation. Report changes to them as issues.

## Rules

- Every public API must have an OpenAPI page with Try it, generated from code, with zh + en descriptions for every field and every allowed value.
- Keep zh and en pages in sync; English links use the `/en/` prefix.
- Run `mint broken-links` before committing. Restart `mint dev` after OpenAPI changes.
- Never put real API keys in examples.
