---
layout: default
title: "Thera GB10 Field Validation"
description: "Two ASUS GX10 / NVIDIA GB10 nodes, public-safe single-unit model baselines, and kernel tuning findings from local long-context inference work."
---

# Thera GB10 Field Validation

Date: 2026-04-17  
Status: public-safe proof snapshot, before final fabric benchmarks with the correct-speed QSFP cable

I am building a local long-context inference and coding-agent cluster around ASUS GX10 / NVIDIA GB10 class systems. I personally purchased the first two nodes and have them running locally. The immediate goal is to validate whether small GB10 clusters can serve private, long-running coding and infrastructure agents with sustained context and enough system headroom.

The public record now includes three kinds of evidence:

- current GB10 hardware and model-asset proof,
- single-unit GPT-OSS 120B and Qwen3-Coder-Next APEX/TurboQuant baselines,
- kernel tuning findings that rule out easy runtime toggles and identify the next credible CUDA path.
- representative graphs for OOB versus tuned decode, Qwen serving-shape tuning, raw batched scaling, and the MMQ negative result.
- a public proof pack with benchmark CSV/JSON, methodology, limitations, launch notes, sanitized summaries, a zip download, and a one-page sponsorship PDF.

Private LAN addresses, receipts, serial numbers, credentials, employer-private diagrams, and raw session history are intentionally excluded from the public copy.

## Evidence Summary

| Item | Current public value |
| --- | --- |
| Purchased systems | 2x ASUS GX10 / NVIDIA GB10 class nodes |
| Primary public host label | `thera128gx10-1` |
| Second public host label | `thera128gx10-2` |
| GPU class | NVIDIA GB10 / `sm_121` |
| Current model assets | Qwen3.5-397B IQ3 at 137G, MiniMax M2.7 IQ4 at 101G |
| Two-node Qwen target | 8 slots, 4M total-token context pool |
| Fabric status | setup functional, final benchmark pending correct-speed QSFP cable |

## Sponsorship Ask

Minimum useful sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10-class validation node,
- correct high-speed fabric cable needed to join the existing setup.

Preferred sponsorship:

- two permanent ASUS GX10 / NVIDIA GB10-class systems,
- compatible QSFP switch or fabric kit,
- correct cables/transceivers for the topology.

Public output in return:

- setup notes with exact commands,
- fabric bring-up and troubleshooting notes,
- reproducible llama.cpp / TurboQuant launch configurations,
- model-fit tables for Qwen, MiniMax, and GLM candidates,
- long-context coding-agent benchmark results,
- memory, throughput, latency, thermal, and stability notes,
- kernel tuning findings with same-condition before/after data.

## Public Proof Pack

Published artifact links:

- `proof-pack.zip`
- `proof-pack/README.md`
- `proof-pack/benchmark-results.csv`
- `proof-pack/benchmark-results.json`
- `proof-pack/graph-source-data.csv`
- `proof-pack/methodology.md`
- `proof-pack/limitations.md`
- `proof-pack/sponsorship-one-pager.pdf`
- `proof-pack/launch-configs/`
- `proof-pack/sanitized-logs/`

Physical photos of the machines and cable/fabric setup are still pending operator capture. The page does not use stock photos as proof.

## Representative Graphs

The public page includes `benchmark-graphs.png` with four visual summaries:

- GPT-OSS 120B OOB stock vLLM fallback at `13 tok/s` versus tuned GB10 audit at `63 tok/s`.
- Qwen3-Coder-Next three-way serving from `31.34 tok/s` per stream to `35.07 tok/s` audited median.
- Qwen3-Coder-Next raw batched scaling from `98.46 tok/s` at npl=3 to `141.46 tok/s` at npl=8.
- Kernel tuning negative result: MMQ-off decode stayed flat at `31.36` versus `31.38 tok/s`, while prompt throughput regressed from `162.40` to `66.96 tok/s`.

The graph caption states that two-node fabric throughput is not graphed yet because the correct-speed QSFP cable is still pending.

## Single-Unit GPT-OSS 120B Data

| Measurement | Recorded value | Why it matters |
| --- | --- | --- |
| Live implementation audit | `63 tok/s` batch-1 decode | Confirms a working GPT-OSS 120B lane on one GB10-class system. |
| Model memory | `64.02 GiB` MXFP4 | Shows the 120B MoE fits inside the 128GB unified-memory envelope. |
| KV cache headroom | `42.46 GiB`, about `1.24M` tokens | Useful prior for long-context budgeting. |
| llama.cpp bench | `2443.91` pp2048 t/s, `58.72` tg32 t/s | Independent prompt-processing and decode-speed evidence. |
| AIME25 local eval | `0.925` score over `240` samples | Functional eval data exists, not just synthetic throughput numbers. |

## Single-Unit Qwen3-Coder-Next APEX/TurboQuant Data

| Measurement | Recorded value | Why it matters |
| --- | --- | --- |
| Model asset used | `Qwen3-Coder-Next-APEX-I-Quality.gguf`, `50,390,241,280` bytes | Known-good single-unit APEX model used for runtime bring-up. |
| Verified serving geometry | `262656` context, `3` slots, `87552` tokens per slot | Concrete long-context serving shape. |
| Single-request decode | About `46.88 tok/s` at `32K` context | Baseline speed for one active request. |
| Three concurrent requests | About `31.34 tok/s` per stream at `262656` total context | Relevant to planner, implementor, and auditor agents sharing the box. |
| Raw batched decode sweep | `98.46 tok/s` aggregate at npl=3, `141.46 tok/s` aggregate at npl=8 | Backend ceiling before OpenAI-compatible server overhead. |
| Repeated-run audited lane | `35.07 tok/s` average decode, about `105.2 tok/s` aggregate at 3-way | Median-of-5 result that survived the audit pass. |

## Kernel Tuning Findings

The kernel work is publishable because it records negative results and narrows the next real optimization target.

| Experiment or finding | Measured result | Engineering conclusion |
| --- | --- | --- |
| Raw baseline for Qwen3-Coder-Next tuning | `speed_tg = 90.19 tok/s` on pp128/tg128/pl3 | Direct backend baseline for selector-level experiments. |
| Disable MMQ globally | Raw `90.73 tok/s`; live decode `31.36` vs baseline `31.38`; live prompt t/s regressed from `162.40` to `66.96` | MMQ yes/no is not the real lever. |
| Disable stream-k globally | Same reproducer exceeded `6m20s` and was terminated; expected baseline was about `2m36s` | stream-k is required on the current branch. |
| Nsight direction | Hot work remains around quantized `mul_mat_q` paths and small-K MoE-shaped kernels | Next accepted edit needs occupancy and launch evidence. |
| TurboQuant decode path | Active profile uses `K=q8_0`, `V=turbo2`; q8_0 K is already compact integer-dot math | Safer first target: mixed VEC decode and turbo2 V dequantization. |
| GB10 Blackwell constraint | `sm_121` is not datacenter Blackwell; no WGMMA/tcgen05 assumptions | Optimizations must match the actual GB10 ISA and memory hierarchy. |

The release-worthy point is discipline: reproducer first, same-condition comparisons, negative results preserved, then a narrow CUDA target.

## Current Two-Node Model Work

| Asset or target | Current value | Status |
| --- | --- | --- |
| Qwen3.5-397B-A17B UD-IQ3_S | `137G` on disk | Primary two-node long-context candidate. |
| MiniMax-M2.7 UD-IQ4_XS | `101G` on disk | Smaller challenger for coding-agent speed and intelligence testing. |
| Combined model storage | `238G` for the two current large model assets | Both fit on disk for side-by-side testing. |
| Qwen two-node serving target | `8` slots, `4M` total-token context pool | Working target from the current combined-node workstream. |
| System reserve | 20GB per node reserved for OS and stability in public planning | Keeps public claims away from OOM-edge operation. |

## Cable And Fabric Status

The temporary cable is rated for 40 Gb/s. That is enough for setup work, interface configuration, and functional bring-up, but it is not enough for a fair GB10 fabric performance claim.

Planned fabric validation after the correct cable arrives:

1. Confirm link negotiation without hard-coding the link to 40 Gb/s.
2. Run forward and reverse `iperf3` across the direct fabric.
3. Run jumbo-frame checks if the negotiated path supports MTU 9000.
4. Capture NIC error/drop/FEC counters before and after sustained load.
5. Repeat model-serving benchmarks after fabric validation.

No public claim should say "combined inference server is solved" until the fabric run, long-context coding tasks, and repeated-run service benchmarks all pass under the same recorded configuration.

## Benchmark Question

The practical question is not "what is the biggest model that can be squeezed into memory." The question is:

> What is the best single local model for two GB10 nodes when the target is maximum coding intelligence, fast inference, long context, and enough headroom to keep the operating systems stable?

Current candidates:

| Candidate | Why it matters |
| --- | --- |
| Qwen3.5-397B-A17B IQ3 class | Already recorded as a working two-node long-context baseline. |
| MiniMax-M2.7 IQ4 class | Smaller on disk than Qwen IQ3 and a serious coding-agent challenger. |
| GLM-5.1 IQ3 class | Potentially the most interesting long-running-agent candidate if fit and runtime shape validate cleanly. |

Every candidate needs real coding tasks over long context: repo-scale context, multi-step edits, debugging, test execution, and the ability to finish without stubbing or quitting early.

## Hardware Sponsorship Ask

I am seeking permanent sponsored hardware, not a temporary loaner.

Minimum useful sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10 class validation node,
- correct cable needed to join the fabric.

Preferred sponsorship:

- two permanent ASUS GX10 / NVIDIA GB10 class systems,
- compatible QSFP high-speed switch or fabric kit,
- correct cables/transceivers for the topology.

Public deliverables:

1. Three-node setup notes with exact commands.
2. Fabric bring-up and troubleshooting notes.
3. Reproducible llama.cpp / TurboQuant launch configurations.
4. Real long-context coding benchmark results.
5. Model fit table for Qwen, MiniMax, and GLM candidates.
6. Memory, throughput, latency, thermal, and stability notes.
7. Kernel tuning findings with same-condition before/after data.
8. Honest disclosure and acknowledgement of sponsored hardware.

## Data Safety

My professional background includes campus network administration and financial-sector systems administration. This project cares about private local inference, long-context agents, and systems work where cloud-only AI is not always the right answer.

Public benchmark tasks will use public repositories, synthetic infrastructure tasks, redacted examples, or purpose-built test repos. No member data, credentials, internal network diagrams, confidential procedures, or private employer documents will be included.

Contact: Mark Sheehy, `mgsheehyjr89@gmail.com`
