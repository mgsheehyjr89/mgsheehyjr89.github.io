# Thera GB10 Field Validation - Sponsorship One-Pager

Date: 2026-04-17  
Operator: Mark Sheehy  
Contact: mgsheehyjr89@gmail.com  
Live page: https://mgsheehyjr89.github.io/

## What Exists Today

- Two personally purchased ASUS GX10 / NVIDIA GB10-class systems.
- Local model assets: Qwen3.5-397B-A17B UD-IQ3_S at 137G and MiniMax-M2.7 UD-IQ4_XS at 101G.
- Current two-node target: 8 agent slots sharing a 4M-token context pool.
- Public-safe single-GB10 benchmark evidence from GPT-OSS 120B and Qwen3-Coder-Next APEX/TurboQuant.
- Kernel/runtime tuning findings, including negative results that narrow the next CUDA target.

## Sponsorship Ask

Minimum useful sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10-class validation node,
- correct high-speed fabric cable needed to join the existing setup.

Preferred sponsorship:

- two permanent ASUS GX10 / NVIDIA GB10-class systems,
- compatible QSFP switch or fabric kit,
- correct cables/transceivers for the topology.

## Public Output In Return

- Setup notes with exact commands.
- Fabric bring-up and troubleshooting notes.
- Reproducible llama.cpp / TurboQuant launch configurations.
- Model fit table for Qwen, MiniMax, and GLM candidates.
- Long-context coding-agent benchmark results.
- Memory, throughput, latency, thermal, and stability notes.
- Kernel tuning findings with same-condition before/after data.
- Sponsor acknowledgement unless the sponsor requests otherwise.

## Why It Matters

Small local GB10 clusters could be practical private AI infrastructure for schools, credit unions, labs, and small businesses that cannot put every workflow in a cloud AI service.

The target is not short demo prompts. The target is local long-running coding and infrastructure agents with real context, reproducible benchmarks, and enough operational discipline to be useful outside a lab demo.

