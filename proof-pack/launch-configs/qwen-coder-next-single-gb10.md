# Qwen3-Coder-Next Single-GB10 Launch Notes

Date: 2026-04-17

## Public Values

- Model asset: `Qwen3-Coder-Next-APEX-I-Quality.gguf`
- Downloaded size: `50,390,241,280` bytes
- Serving context: `262656`
- Slots: `3`
- Tokens per slot: `87552`
- Single-request decode: about `46.88 tok/s` at `32K` context
- Three concurrent requests: about `31.34 tok/s` per stream at `262656` total context
- Repeated-run audited lane: `35.07 tok/s` average decode, about `105.2 tok/s` aggregate at 3-way

## Raw Batched Decode Sweep

| npl | Aggregate tok/s |
| ---: | ---: |
| 3 | 98.46 |
| 4 | 112.63 |
| 5 | 121.93 |
| 6 | 130.55 |
| 8 | 141.46 |

## Public Reproduction Shape

The public benchmark shape is:

```text
backend: llama.cpp / TurboQuant branch
quant/cache profile: q8_0 K / turbo2 V where applicable
context: 262656
slots: 3
comparison: direct backend vs OpenAI-compatible serving path
```

Private paths and local host bindings are intentionally omitted.

