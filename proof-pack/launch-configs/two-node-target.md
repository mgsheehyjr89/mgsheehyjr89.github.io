# Two-Node Target Shape

Date: 2026-04-17

## Current Target

| Field | Value |
| --- | --- |
| Nodes | 2x ASUS GX10 / NVIDIA GB10-class systems |
| Candidate model | Qwen3.5-397B-A17B UD-IQ3_S |
| Current model size | 137G |
| Secondary candidate on disk | MiniMax-M2.7 UD-IQ4_XS, 101G |
| Target slots | 8 |
| Target context pool | 4M total tokens |
| Public reserve | 20GB per node |
| Fabric | private direct high-speed link, final speed benchmark pending correct cable |

## Validation Gate

Do not call this a solved combined inference server until:

1. the correct-speed QSFP cable is installed,
2. the link negotiates without hard-coding 40G,
3. forward and reverse `iperf3` pass,
4. NIC counters stay clean under load,
5. long-context coding tasks run against the combined-node service,
6. repeated service benchmarks pass under the same launch configuration.

