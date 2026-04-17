# GB10 Public Proof Evidence Snapshot

Date: 2026-04-17  
Scope: sanitized local evidence for `docs/gb10-public-proof/index.html`

This file records the local facts used in the proof post. It intentionally omits serial numbers, receipts, private screenshots, private network details, and credentials.

## Host Identity

Command:

```bash
hostnamectl
```

Sanitized result:

```text
Static hostname: thera128gx10-1
Operating System: Ubuntu 24.04.4 LTS
Kernel: Linux 6.17.0-1014-nvidia
Architecture: arm64
Hardware Vendor: ASUSTeK COMPUTER INC.
Hardware Model: GX10
Firmware Version: GX10DGX.0103.2026.0129.1152
```

## GPU

Command:

```bash
nvidia-smi --query-gpu=name,memory.total,driver_version --format=csv,noheader
```

Result:

```text
NVIDIA GB10, [N/A], 580.142
```

Note: this platform reports unified memory differently from a discrete GPU, so `nvidia-smi` does not expose a normal VRAM total in this query.

## High-Speed NICs

Command:

```bash
lspci | rg -i 'nvidia|mellanox|connectx|ethernet|infiniband'
```

Relevant result:

```text
0000:01:00.0 Ethernet controller: Mellanox Technologies MT2910 Family [ConnectX-7]
0000:01:00.1 Ethernet controller: Mellanox Technologies MT2910 Family [ConnectX-7]
0002:01:00.0 Ethernet controller: Mellanox Technologies MT2910 Family [ConnectX-7]
0002:01:00.1 Ethernet controller: Mellanox Technologies MT2910 Family [ConnectX-7]
000f:01:00.0 VGA compatible controller: NVIDIA Corporation Device 2e12 (rev a1)
```

## Network State

Command:

```bash
ip -br addr show
```

Sanitized result:

```text
LAN management interface: up
Private fabric interface: up
Private fabric bond: up
Additional high-speed interfaces: up
```

The public post does not include private LAN addresses.

## Model Files Present

Command:

```bash
du -sh /home/thera/TheraData/thera_storage/models/node_c/*
```

Result:

```text
101G  /home/thera/TheraData/thera_storage/models/node_c/MiniMax-M2.7-UD-IQ4_XS
137G  /home/thera/TheraData/thera_storage/models/node_c/Qwen3.5-397B-A17B-UD-IQ3_S
```

## Graph Asset

Generated shareable graph file:

```text
/home/thera/Thera/docs/gb10-public-proof/benchmark-graphs.png
```

Graph panels:

```text
GPT-OSS 120B OOB stock vLLM fallback: 13 tok/s
GPT-OSS 120B tuned GB10 audit: 63 tok/s
Qwen3-Coder-Next initial three-way serving: 31.34 tok/s per stream
Qwen3-Coder-Next audited tuned median: 35.07 tok/s per stream
Qwen3-Coder-Next raw batched decode: 98.46, 112.63, 121.93, 130.55, 141.46 tok/s at npl=3,4,5,6,8
MMQ-off decode comparison: 31.38 baseline vs 31.36 MMQ off
MMQ-off prompt comparison: 162.40 baseline vs 66.96 MMQ off
```

The graph explicitly excludes two-node fabric throughput until the correct-speed QSFP cable is installed and retested.

## Social And Proof-Pack Assets

Generated public page assets:

```text
/home/thera/Thera/docs/gb10-public-proof/social-card.png
/home/thera/Thera/docs/gb10-public-proof/favicon.png
/home/thera/Thera/docs/gb10-public-proof/proof-pack.zip
/home/thera/Thera/docs/gb10-public-proof/proof-pack/sponsorship-one-pager.pdf
```

Proof-pack files:

```text
proof-pack/README.md
proof-pack/hardware-summary.md
proof-pack/methodology.md
proof-pack/limitations.md
proof-pack/benchmark-results.csv
proof-pack/benchmark-results.json
proof-pack/graph-source-data.csv
proof-pack/CHANGELOG.md
proof-pack/launch-configs/gpt-oss-120b-single-gb10.md
proof-pack/launch-configs/qwen-coder-next-single-gb10.md
proof-pack/launch-configs/two-node-target.md
proof-pack/sanitized-logs/gpt-oss-120b-summary.log
proof-pack/sanitized-logs/qwen-coder-next-summary.log
proof-pack/sanitized-logs/kernel-tuning-summary.log
proof-pack/sponsorship-one-pager.md
proof-pack/sponsorship-one-pager.pdf
```

The proof pack omits private LAN addresses, credentials, serial numbers, receipts, employer-private diagrams, raw private sessions, and confidential operational data.

## Live Serving State At Snapshot Time

Command:

```bash
pgrep -af 'llama-server|rpc-server'
```

Result:

```text
No matching process at snapshot time.
```

Meaning: the public post uses the Qwen two-node service shape from the current Node C runbook as an internal baseline, but does not claim live throughput or latency from this snapshot.

## Runbook Source

Local source used for current model and memory-budget notes:

```text
/home/thera/Thera/docs/operations/node-c-best-model-turboquant-runbook.md
```

Key recorded values from that runbook:

```text
Node C-1: thera128gx10-1
Node C-2: thera128gx10-2.Zen
Nominal memory: 128 GB unified memory per GB10 node
Reserve: 20 GB per node
Usable budget: about 208 to 216 GB combined
Recorded Qwen service shape: 8 slots, 4M total context, llama.cpp/TurboQuant
Current MiniMax asset target: MiniMax-M2.7 UD-IQ4_XS
```

## Single-Unit GPT-OSS 120B Data

Local source artifacts:

```text
/home/thera/Thera/.agents/engineering/gptoss-120b-node-c/audit-implementation.md
/home/thera/runtime/node_c/llama-cpp-turboquant/benches/dgx-spark/dgx-spark.md
/home/thera/runtime/node_c/llama-cpp-turboquant/benches/dgx-spark/run-aime-120b-t8-x8-high.log
/home/thera/runtime/node_c/llama-cpp-turboquant/benches/dgx-spark/aime25_openai__gpt-oss-120b-high_temp1.0_20251109_094547.json
```

Key recorded values:

```text
Live implementation audit: 63 tok/s batch-1 decode
Model memory: 64.02 GiB MXFP4
KV cache available: 42.46 GiB, about 1.24M tokens
llama.cpp GPT-OSS 120B bench: pp2048 2443.91 t/s, tg32 58.72 t/s
AIME25 local eval: score 0.925 over 240 samples
```

## Single-Unit Qwen3-Coder-Next APEX/TurboQuant Data

Local source artifacts:

```text
/home/thera/Thera/.agents/engineering/node-c-llamacpp-apex-turboquant/implementation_log.md
/home/thera/Thera/.agents/engineering/node-c-blackwell-kernel-tuning/spec.md
/home/thera/Thera/.agents/engineering/node-c-blackwell-kernel-tuning/implementation_log.md
/home/thera/Thera/.agents/engineering/node-c-tierc-llamacpp-apex-tq/handoffs/lorentz_benchmark_governor_handoff.md
```

Key recorded values:

```text
Model asset used: Qwen3-Coder-Next-APEX-I-Quality.gguf
Downloaded size: 50,390,241,280 bytes
Verified serving geometry: 262656 context, 3 slots, 87552 tokens per slot
Single-request decode: about 46.88 tok/s at 32K context
Three concurrent requests: about 31.34 tok/s per stream at 262656 total context
Raw batched decode: 98.46 tok/s aggregate at npl=3, 141.46 tok/s aggregate at npl=8
Repeated-run audited lane: 35.07 tok/s average decode, about 105.2 tok/s aggregate at 3-way
```

## Kernel Tuning Findings

Local source artifacts:

```text
/home/thera/Thera/.agents/engineering/node-c-blackwell-kernel-tuning/spec.md
/home/thera/Thera/.agents/engineering/node-c-blackwell-kernel-tuning/implementation_log.md
/home/thera/Thera/.agents/engineering/node-c-tierc-llamacpp-apex-tq/handoffs/planck_kernel_runtime_handoff.md
```

Key recorded values and conclusions:

```text
Raw baseline: speed_tg = 90.19 tok/s on pp128/tg128/pl3
Global MMQ disable: raw 90.73 tok/s, live decode 31.36 vs baseline 31.38
Global MMQ disable prompt regression: prompt_tps_avg 162.40 -> 66.96
Global stream-k disable: exceeded 6m20s on a reproducer with about 2m36s baseline and was terminated
Conclusion: MMQ yes/no and stream-k off are not viable high-level fixes
Next narrow target: mixed q8_0 K / turbo2 V VEC decode path and on-the-fly turbo2 V dequantization
Hardware constraint: GB10 sm_121 is not datacenter Blackwell; do not assume WGMMA/tcgen05
```
