# Published Location

Published on 2026-04-16.

Updated on 2026-04-17 with single-unit GPT-OSS 120B data, Qwen3-Coder-Next APEX/TurboQuant data, kernel tuning findings, the evidence image asset, representative benchmark graphs, a full public proof-page redesign, social sharing assets, and a downloadable sponsorship proof pack.

Live page:

```text
https://mgsheehyjr89.github.io/
```

GitHub repository:

```text
https://github.com/mgsheehyjr89/mgsheehyjr89.github.io
```

Published file:

```text
index.html
evidence-visual.png
benchmark-graphs.png
social-card.png
favicon.png
proof-pack.zip
proof-pack/
```

Current publication record:

```text
See the GitHub Pages repository history for the latest published commit.
```

Verification performed:

```bash
curl -sS -L -o /tmp/gh-pages-live.html -w '%{http_code} %{url_effective}\n' https://mgsheehyjr89.github.io/
rg -q '0.925|Qwen3-Coder-Next|Kernel Tuning Findings|141.46' /tmp/gh-pages-live.html
curl -sS -L -o /tmp/benchmark-graphs-live.png -w '%{http_code} %{content_type} %{size_download}\n' https://mgsheehyjr89.github.io/benchmark-graphs.png
```

Result:

```text
2026-04-16: 200 https://mgsheehyjr89.github.io/; original page content verified
2026-04-17: 200 https://mgsheehyjr89.github.io/?v=d9686ac-final
2026-04-17: markers verified: 0.925, Qwen3-Coder-Next, Kernel Tuning Findings, 141.46, evidence-visual.png
2026-04-17: image verified: 200 image/png 100607 bytes
2026-04-17: graph commit pushed: 947df74 Add GB10 benchmark graphs
2026-04-17: graph markers verified: benchmark-graphs.png, OOB Vs Tuned, Representative graphs, 141.46, Kernel Tuning Findings
2026-04-17: graph image verified: 200 image/png 135614 bytes, 1600x1280 RGB
2026-04-17: polish commit pushed: 2a46e41 Polish GB10 proof page design
2026-04-17: polish markers verified live: --panel-dark, --accent-gold, benchmark-graphs.png, OOB Vs Tuned, Evidence Worth Sharing
2026-04-17: live desktop screenshot captured at 1440x1800; live mobile screenshot captured at 390x1400
2026-04-17: redesign commit pushed: b04a19b Redesign GB10 proof page
2026-04-17: redesign markers verified live: Thera Field Lab, hero-stat-strip, Hardware in hand, Performance Story In Four Graphs, The Case At A Glance
2026-04-17: redesigned evidence image verified: 200 image/png 127762 bytes, 1800x1050 RGB
2026-04-17: live redesign screenshots captured at 1440x2100 and 390x1500
2026-04-17: proof-pack publication prepared: Add GB10 sponsorship proof pack
2026-04-17: local proof-pack verification passed: HTML links resolve, JSON parses, zip tests clean, one-page PDF is 1 page
2026-04-17: proof-pack commit pushed: 981ef6a Add GB10 sponsorship proof pack
2026-04-17: live proof-pack markers verified: Sponsor The Next GB10 Node, Artifacts People Can Inspect, proof-pack.zip, sponsorship-one-pager.pdf, twitter:card, social-card.png
2026-04-17: live assets verified: social-card.png 1200x630, favicon.png 256x256, proof-pack.zip 15269 bytes with clean unzip test, sponsorship-one-pager.pdf 1 page
2026-04-17: live proof-pack screenshots captured at 1440x3200 and 390x2200
2026-04-17: polish commit pushed: ee0b703 Polish GB10 public sponsorship page
2026-04-17: live polish markers verified: Thera GB10 Validation, Evidence brief, Permanent GB10 Hardware Request, Download The Verification Materials, What Is Already Verified
2026-04-17: live polish assets verified: evidence-visual.png 137455 bytes, social-card.png 45084 bytes, proof-pack.zip 13928 bytes with clean unzip test, sponsorship-one-pager.pdf 1 page
2026-04-17: live polish screenshots captured at 1440x3200 and 390x2200
```
