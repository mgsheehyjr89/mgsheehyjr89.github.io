# Short Public Post

I am publishing a public-safe evidence update for my local Thera GB10 field-validation cluster.

Current status:

- I personally purchased two ASUS GX10 / NVIDIA GB10 class systems.
- The local cluster has Qwen3.5-397B-A17B UD-IQ3_S at 137G and MiniMax-M2.7 UD-IQ4_XS at 101G on disk.
- The current two-node Qwen target is 8 slots with a 4M-token total context pool using llama.cpp / TurboQuant.
- Final two-node fabric claims are still pending the correct-speed QSFP cable. The temporary cable is only rated for 40 Gb/s.
- The public page now includes a downloadable proof pack, a one-page sponsorship PDF, Open Graph social preview metadata, benchmark CSV/JSON, methodology, limitations, launch notes, and sanitized result summaries.

Publishable single-unit data already exists:

- GPT-OSS 120B: 63 tok/s batch-1 decode in the live implementation audit, 64.02 GiB model memory, 42.46 GiB KV cache, about 1.24M tokens.
- GPT-OSS 120B llama.cpp bench: 2443.91 pp2048 t/s and 58.72 tg32 t/s.
- GPT-OSS 120B AIME25 local eval: 0.925 score over 240 samples.
- Qwen3-Coder-Next APEX/TurboQuant: 262656 context, 3 slots, 87552 tokens per slot.
- Qwen3-Coder-Next: about 46.88 tok/s single-request decode at 32K context, about 31.34 tok/s per stream at 3-way concurrency.
- Qwen3-Coder-Next raw batched decode: 98.46 tok/s aggregate at npl=3 and 141.46 tok/s aggregate at npl=8.

I added representative graphs for the data people can understand quickly:

- GPT-OSS 120B OOB stock vLLM fallback at 13 tok/s versus tuned GB10 audit at 63 tok/s.
- Qwen3-Coder-Next three-way serving from 31.34 tok/s per stream to 35.07 tok/s audited median.
- Qwen3-Coder-Next raw batched scaling up to 141.46 tok/s at npl=8.
- MMQ-off negative result: decode stayed flat while prompt throughput regressed from 162.40 to 66.96 tok/s.

We can also release kernel tuning findings:

- Global MMQ disable was not the fix: raw speed barely moved, live decode did not improve, and prompt throughput regressed hard.
- Global stream-k disable was not viable: the reproducer exceeded 6m20s and was terminated.
- The next credible target is a narrow CUDA path: mixed q8_0 K / turbo2 V VEC decode and on-the-fly turbo2 V dequantization on real GB10 sm_121 constraints.

The benchmark target is the best single local model for two GB10 nodes when the goal is maximum coding intelligence, fast inference, long context, and stable OS headroom. The tests have to use real coding tasks over long context. Short prompt demos are not enough.

The next missing piece is permanent sponsored hardware. One more GB10 unlocks a real three-node fabric/ring validation. Two more nodes plus the right QSFP switch/fabric kit unlock a four-node benchmark.

Minimum useful sponsorship:

- one permanent ASUS GX10 / NVIDIA GB10-class validation node,
- the correct high-speed fabric cable needed to join the existing setup.

Preferred sponsorship:

- two permanent GB10-class systems,
- compatible QSFP switch or fabric kit,
- correct cables/transceivers.

Public output in return: setup notes, fabric diagnostics, reproducible launch configs, model-fit tables, long-context coding benchmarks, stability notes, and kernel/runtime findings.

Contact: Mark Sheehy, mgsheehyjr89@gmail.com
