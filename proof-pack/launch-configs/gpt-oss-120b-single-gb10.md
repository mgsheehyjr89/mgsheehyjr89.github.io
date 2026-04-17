# GPT-OSS 120B Single-GB10 Launch Notes

Date: 2026-04-17

This file records public-safe launch context, not a full private shell history.

## Public Values

- Model: GPT-OSS 120B
- Quant / memory note: MXFP4, `64.02 GiB` model memory
- KV headroom: `42.46 GiB`, approximately `1.24M` tokens
- Live implementation audit decode: `63 tok/s` batch-1
- llama.cpp bench: `2443.91` pp2048 t/s, `58.72` tg32 t/s
- AIME25 local eval: `0.925` over `240` samples

## Reproducibility Notes

The exact local launch script remains in the private Thera runtime tree because raw paths and shell history can include private context.

The next public pass should extract a sanitized command with:

- model path replaced by `<model_path>`,
- host bindings removed,
- private LAN addresses removed,
- environment variables reduced to those necessary for reproduction.

