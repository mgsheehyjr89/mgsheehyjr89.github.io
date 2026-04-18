# Public Post Draft

I published a validation card for a privately funded two-node ASUS GX10 / NVIDIA GB10 local inference testbed.

Current public state:

- 2x ASUS GX10 / NVIDIA GB10-class systems installed locally.
- Qwen3.5-397B-A17B UD-IQ3_S and MiniMax-M2.7 UD-IQ4_XS staged together, 238 GB total.
- Current two-node target: one high-capability model, 8 agent slots, 4M-token context pool, llama.cpp / TurboQuant serving.
- Final two-node fabric throughput is not claimed yet; the correct-speed QSFP cable is still the gating item.
- Public proof pack includes benchmark CSV/JSON, methodology, limitations, launch notes, sanitized summaries, graph assets, and a sponsor one-pager.

Publishable single-node evidence:

- GPT-OSS 120B tuned GB10 audit: 63 tok/s batch-1 decode.
- GPT-OSS 120B local eval: 0.925 over 240 AIME25 samples.
- GPT-OSS 120B memory profile: 64.02 GiB model memory and 42.46 GiB KV cache headroom.
- Qwen3-Coder-Next APEX/TurboQuant: 262656 context, 3 slots, 87552 tokens per slot.
- Qwen3-Coder-Next raw batched decode: 98.46 tok/s aggregate at npl=3 and 141.46 tok/s aggregate at npl=8.

Runtime findings:

- Global MMQ disable was not an acceptable tuning path: live decode did not improve and prompt throughput regressed from 162.40 to 66.96 tok/s.
- Global stream-k disable was not viable on the current branch.
- The next credible CUDA target is a narrower TurboQuant decode path on the actual GB10 `sm_121` constraints.

The evaluation target is not a short demo prompt. The target is long-context coding-agent work: real repositories, multi-file edits, tool use, tests, failure recovery, queue behavior, memory pressure, and completion quality.

Minimum useful hardware sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10-class validation node,
- correct high-speed fabric cable needed to join the existing setup.

Preferred sponsorship:

- two permanent GB10-class systems,
- compatible QSFP switch or fabric kit,
- correct cables/transceivers.

Public deliverables in return: setup notes, fabric diagnostics, reproducible launch configurations, model-fit tables, long-context coding benchmarks, stability notes, and kernel/runtime findings.

Contact: Mark Sheehy, mgsheehyjr89@gmail.com
