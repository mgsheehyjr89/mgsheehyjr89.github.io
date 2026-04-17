# Limitations And Caveats

Date: 2026-04-17

## Current Caveats

- The temporary cable is rated for 40 Gb/s, so final GB10 fabric throughput is not claimed yet.
- The public graph image intentionally excludes final two-node fabric throughput.
- Qwen Coder values in the public graphs are single-GB10 historical baselines, not final combined-node service results.
- The current page uses generated evidence graphics and screenshots; physical photos of the local machines still need to be added by the operator.
- Some model and benchmark artifacts remain local because raw logs can contain private paths, hostnames, or operational context.
- The 20GB-per-node reserve is a public planning guardrail, not the absolute minimum observed during internal tests.

## Not Claimed Yet

- No public claim that C-1 and C-2 are a fully validated combined inference server.
- No final two-node throughput claim.
- No final Qwen vs MiniMax vs GLM coding-agent winner.
- No claim that current kernel tuning has produced a deployable CUDA speedup.

## Required Before Stronger Claims

- Correct-speed QSFP cable installed.
- Forward and reverse fabric benchmarks captured.
- NIC error/drop/FEC counters captured before and after sustained load.
- Long-context real coding tasks run across candidates.
- Repeated service benchmarks captured under the same launch configuration.

