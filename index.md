---
layout: default
title: "Thera GB10 Local Inference Validation"
description: "Two ASUS GX10 / NVIDIA GB10 nodes, shareable benchmark evidence, model assets, runtime findings, limitations, and a permanent hardware sponsorship request."
---

# Thera GB10 Local Inference Validation

Date: 2026-04-18  
Status: shareable validation card, before final fabric benchmarks with the correct-speed QSFP cable

This record documents a privately funded two-node ASUS GX10 / NVIDIA GB10 local inference testbed for long-context coding and infrastructure agents.

The public validation card includes:

- current GB10 hardware and node-state summary,
- single-unit GPT-OSS 120B and Qwen3-Coder-Next APEX/TurboQuant baselines,
- kernel/runtime findings that rule out broad runtime toggles and identify the next credible optimization path,
- representative graphs for OOB versus tuned decode, Qwen serving-shape tuning, raw batched scaling, and the MMQ negative result,
- a proof pack with benchmark CSV/JSON, methodology, limitations, launch notes, sanitized summaries, a zip download, and a one-page sponsorship PDF.

Private LAN addresses, receipts, serial numbers, credentials, employer-private diagrams, and raw session history are intentionally excluded from the published copy.

## Validation Summary

| Item | Current public value |
| --- | --- |
| Installed systems | 2x ASUS GX10 / NVIDIA GB10-class nodes |
| Primary public host label | `thera128gx10-1` |
| Second public host label | `thera128gx10-2` |
| GPU class | NVIDIA GB10 / `sm_121` |
| Current model assets | Qwen3.5-397B IQ3 at 137G, MiniMax M2.7 IQ4 at 101G |
| Two-node target | 8 slots, 4M total-token context pool |
| Fabric status | setup work in progress; final benchmark pending correct-speed QSFP cable |

## Measured Evidence

| Measurement | Recorded value | Interpretation |
| --- | --- | --- |
| GPT-OSS 120B tuned decode | `63 tok/s` batch-1 decode | Useful local 120B inference lane on one GB10-class system. |
| GPT-OSS 120B local eval | `0.925` over `240` AIME25 samples | Functional evaluation data accompanies throughput data. |
| GPT-OSS 120B memory | `64.02 GiB` MXFP4 | The 120B MoE leaves meaningful room on a 128GB unified-memory node. |
| GPT-OSS 120B KV headroom | `42.46 GiB`, about `1.24M` tokens | Useful prior for long-context budgeting. |
| Qwen3-Coder-Next serving geometry | `262656` context, `3` slots, `87552` tokens per slot | Concrete long-context serving geometry. |
| Qwen3-Coder-Next raw sweep | `98.46 tok/s` aggregate at npl=3, `141.46 tok/s` aggregate at npl=8 | Backend ceiling before OpenAI-compatible service overhead. |

## Runtime Findings

| Experiment or finding | Measured result | Engineering conclusion |
| --- | --- | --- |
| Raw baseline for Qwen3-Coder-Next tuning | `speed_tg = 90.19 tok/s` on pp128/tg128/pl3 | Direct backend baseline for selector-level experiments. |
| Disable MMQ globally | Raw `90.73 tok/s`; live decode `31.36` vs baseline `31.38`; prompt t/s regressed from `162.40` to `66.96` | Global MMQ disable is not an acceptable tuning path. |
| Disable stream-k globally | Same reproducer exceeded `6m20s` and was terminated; expected baseline was about `2m36s` | stream-k is required on the current branch. |
| TurboQuant decode path | Active profile uses `K=q8_0`, `V=turbo2` | Safer first target: mixed VEC decode and turbo2 V dequantization. |
| GB10 Blackwell constraint | `sm_121` is not datacenter Blackwell | Optimizations must match the actual GB10 ISA and memory hierarchy. |

## Claims Not Yet Made

- No public claim that C-1 and C-2 are a fully validated combined inference server.
- No final two-node fabric throughput claim.
- No final Qwen vs MiniMax vs GLM coding-agent winner.
- No claim that current kernel tuning has produced a deployable CUDA speedup.

Required before stronger claims:

1. Correct-speed QSFP cable installed.
2. Forward and reverse fabric benchmarks captured.
3. NIC error/drop/FEC counters captured before and after sustained load.
4. Long-context real coding tasks run across candidates.
5. Repeated service benchmarks captured under the same launch configuration.

## Hardware Sponsorship Ask

Minimum useful sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10-class validation node,
- correct high-speed fabric cable needed to join the existing setup.

Preferred sponsorship:

- two permanent ASUS GX10 / NVIDIA GB10-class systems,
- compatible QSFP switch or fabric kit,
- correct cables/transceivers for the topology.

Public deliverables:

1. Three-node setup notes with exact commands.
2. Fabric bring-up and troubleshooting notes.
3. Reproducible llama.cpp / TurboQuant launch configurations.
4. Real long-context coding benchmark results.
5. Model-fit table for Qwen, MiniMax, and GLM candidates.
6. Memory, throughput, latency, thermal, and stability notes.
7. Kernel tuning findings with same-condition before/after data.
8. Sponsored-hardware acknowledgement unless a sponsor requests otherwise.

Contact: Mark Sheehy, `mgsheehyjr89@gmail.com`
