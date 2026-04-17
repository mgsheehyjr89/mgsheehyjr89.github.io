# Public Benchmark Methodology

Date: 2026-04-17

## Scope

This proof pack reports public-safe local evidence from ASUS GX10 / NVIDIA GB10-class systems used for local long-context inference and coding-agent validation.

The public page currently emphasizes single-GB10 baselines because the correct-speed QSFP cable for final fabric benchmarking has not arrived yet.

## Measurement Rules

1. Separate direct backend measurements from OpenAI-compatible serving measurements.
2. Record model, quantization, context, slot count, backend, and test surface.
3. Preserve negative tuning results when they narrow the next engineering target.
4. Do not publish private LAN addresses, credentials, serial numbers, receipts, employer documents, or raw private session history.
5. Do not claim the two-node inference server is solved until fabric, long-context tasks, and repeated service benchmarks pass under the same recorded configuration.

## Current Public Benchmark Surfaces

| Surface | Purpose |
| --- | --- |
| GPT-OSS 120B live implementation audit | Confirms one working large-model lane on a GB10-class node. |
| GPT-OSS 120B llama.cpp bench | Independent prompt/decode benchmark surface. |
| GPT-OSS 120B AIME25 local eval | Functional quality signal beyond throughput. |
| Qwen3-Coder-Next single-request serving | User-facing decode speed for one active request. |
| Qwen3-Coder-Next three-way serving | Agent-like concurrency baseline. |
| Qwen3-Coder-Next raw batched decode sweep | Backend throughput ceiling before service overhead. |
| Kernel tuning reproducer | Same-condition tuning checks for GB10 runtime paths. |

## Pending Methodology Additions

After the correct-speed QSFP cable arrives:

1. record negotiated link speed without hard-coding 40G,
2. capture MTU and NIC counters before load,
3. run forward `iperf3`,
4. run reverse `iperf3`,
5. run jumbo-frame checks if valid,
6. capture NIC counters after sustained load,
7. repeat model-serving benchmarks using the same launch configuration.

