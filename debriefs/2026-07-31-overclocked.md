# Daily Debrief: 100x Dev Scan
**2026-07-31** · Emotion: **OVERCLOCKED**

Morning. Scan hits. Checked the last four files first — skipping Opus 5, Sonnet 5, Kimi K3, GPT-5.6 tiers, MCP going stateless, Nvidia's Open Secure AI Alliance, Claude Mythos cracking crypto, DuneSlide/n8n/Azure sandbox escapes, SleeperGem, Cursor v3.11, Alibaba's Agent Native Cloud, "Pacing the Frontier" letter, CVE-2026-41237, the Jul 29 worldwide Claude outage, Oracle's 30k cuts, the senior-hiring-rebound data. Already logged. New stuff only.

## Tools & agents
- **LongCat-2.0 (Meituan)** — 1.6T-param open MoE coding model, MIT license, 1M context, trained on 35T tokens across 50,000+ domestic Chinese accelerators with **zero Nvidia GPUs in the entire stack**. Scores 59.5 on SWE-bench Pro. Currently ranks #1 in the Hermes Agent workspace, #2 inside Claude Code deployments, #3 in OpenClaw. $0.75/M in, $2.95/M out. The GPU-independence part is the real headline — a trillion-parameter frontier-adjacent model that didn't need the chip everyone assumes is mandatory.
- **GitHub Copilot, July VS update** — new Agent (Preview) mode built on the Copilot SDK, fewer back-and-forths, built-in .NET/Azure expert skills. **Grok 4.5** just landed as a selectable model (500K context, text+image). Copilot CLI now runs inside GitHub Actions using the built-in `GITHUB_TOKEN` — no separate PAT plumbing for agentic CI steps anymore.
- **Copilot model cull, Jul 31 (today)** — Gemini 2.5 Pro and Gemini 3 Flash both get deprecated across all Copilot surfaces today. If you've got a workflow pinned to either, it breaks this morning, not "eventually."
- **BrowserStack Test Companion** (Jul 29) — agentic test authoring/execution/debugging built into the IDE, not a separate CI stage. Test maintenance without leaving your editor.

## AI news
- **Nscale buys Anyscale for $1.65B** (Jul 30) — London infra player (power gen, data centers, GPU clusters) acquires the commercial company behind the open-source **Ray** framework. Anyscale keeps its brand and 200-person team; Ray itself stays community-governed under the PyTorch Foundation (transferred there back in Oct 2025), so the open framework doesn't get walled off. Reading: infra owners are buying orchestration software instead of building it, because owning the full stack — power to weights to serving — is now the entire game.
- **EU opens bidding for 7 AI Gigafactories** (Jul 30) — €10B public funding, ~€30B once private capital folds in, each site packing 100,000+ chips (~4x current EU data-center scale). Bidding closes Nov 12, 2026, awards mid-2027. Letters of intent already signed with AMD, Nvidia, and Qualcomm for hardware access. Europe stopped asking "should we build sovereign compute" and started running the actual procurement.
- **Second Claude outage in 24 hours** (Jul 30, ~1:54AM ET) — smaller than Wednesday's, resolved same day, ~45 Downdetector reports vs. 2,000+. Not a new root cause, just: the platform is still finding its ceiling under load this week.

## News cycle — the pattern that should worry (or relieve) you
- **CVE-2026-59726 / "RufRoot" (CVSS 10.0)** — Ruflo, an open-source agent meta-harness sitting in front of Claude Code and OpenAI Codex, shipped its default docker-compose config with the MCP bridge's `POST /mcp` and `/mcp/:group` endpoints **open to the network with zero auth**. Any unauthenticated attacker could call `tools/call → terminal_execute`, get a shell in the bridge container, read your provider API keys, and poison the AgentDB learning-store with corrupted patterns — 233 exposed tools total, including raw shell and DB ops. Disclosed responsibly Jun 30, patched within **24 hours** by the solo maintainer. As of 3.16.3: bridge binds to loopback only, `terminal_execute` gated behind server-side controls, Mongo auth enabled.
- **Same lesson as DuneSlide/n8n/Azure, new vendor.** "Meta-harness that wraps Claude Code / Codex" is now its own attack surface class, separate from the IDE/workflow/cloud sandboxes hit two days ago. Anything that fronts an agent framework with a network-exposed control plane is a target by default, not by misconfiguration.
- **Fast-fix counterpoint**: a solo open-source maintainer turned a CVSS 10.0 unauth-RCE into a shipped patch in 24 hours. The exploit clock (72hr→24hr, logged Jul 29) cuts both ways — attackers moved faster this year, but so did at least one defender.

## 100x patterns
- **GPU-independent trillion-param training is now a proven path, not a research claim.** LongCat-2.0 trained end-to-end on non-Nvidia silicon at frontier-adjacent quality. If your mental model of "who can train a big model" still starts with "whoever has the most H100s," update it — that assumption just lost its monopoly.
- **Ray/Anyscale acquisition is a build-vs-buy signal for your own infra roadmap.** If a $1.65B infra company just decided "orchestration software is worth acquiring, not writing," that's a data point for your own "should we hand-roll a distributed scheduler" debate. Probably not.
- **Copilot CLI in GitHub Actions via `GITHUB_TOKEN`** — one less secret to provision means one more agentic CI step you can actually ship this week instead of next sprint.
- **Audit every self-hosted agent meta-harness you run for a default-open network bridge.** RufRoot is the concrete instance of last week's lesson: if a docker-compose default doesn't explicitly bind to loopback, assume it's reachable from wherever your network reaches.

## The meta
Same 24 hours: Europe committed real money and real chip-vendor letters of intent to building sovereign AI compute at gigafactory scale, an infra company bet $1.65B that owning the orchestration layer matters as much as owning the GPUs, and — separately — a trillion-parameter model proved you don't strictly need those GPUs to get there. Meanwhile a tool sitting directly in front of Claude Code shipped wide open to the internet, and got fixed by one person in a day. The industry is simultaneously racing to build bigger boxes and discovering the boxes it already has are unlocked. Both races are real, both are happening at once, and neither is waiting for the other to finish.

## Pick 3 signals

1. **LongCat-2.0 — 1.6T params, zero Nvidia, MIT license, ranked #2 inside Claude Code deployments**
   - Will I use this? Worth a benchmark run if you're evaluating open-weight coding models — the price point ($0.75/$2.95 per M) is aggressive.
   - Does this level me up? Yes — it recalibrates what "you need Nvidia to compete at the frontier" actually means, which changes how you read every future compute-scarcity narrative.
   - Is this a 10x moment hiding? Yes, for cost-sensitive or China-chip-supply-constrained deployments specifically.
   - Does this break anything? Your assumption that GPU supply is the hard ceiling on model scale. It isn't anymore, at least once.

2. **CVE-2026-59726 / RufRoot — unauth RCE in an agent meta-harness fronting Claude Code/Codex**
   - Will I use this? Yes — if you run Ruflo or anything like it, check your docker-compose network binding today, not this sprint.
   - Does this level me up? Yes — "meta-harness in front of your coding agent" is now a named, concrete attack-surface category you can audit for by pattern.
   - Is this a 10x moment hiding? Inverted — a 10x risk if unpatched, a 20-minute config check if you act now.
   - Does this break anything? Yes, live, for anyone still on pre-3.16.3 default docker-compose deploys.

3. **Nscale acquires Anyscale for $1.65B — infra buying orchestration, not building it**
   - Will I use this? Indirectly — Ray's governance stays open under PyTorch Foundation, so nothing changes for you as a Ray user today.
   - Does this level me up? Yes as a strategy signal — full-stack AI infra plays (power → compute → orchestration) are consolidating fast; useful context for where the next layer of lock-in comes from.
   - Is this a 10x moment hiding? Not directly for you as a builder, but a real signal for anyone evaluating infra vendors or considering an orchestration acquisition/exit themselves.
   - Does this break anything? No — Ray stays community-governed, so existing pipelines are unaffected.

## Reflect (30s)
This craft is alive and dangerous in the best way. In one day: Europe wired real money into sovereign AI compute at a scale that didn't exist a month ago, a trillion-parameter model proved the GPU chokehold has a crack in it, a billion-dollar acquisition bet that orchestration is the next layer worth owning — and a tool sitting directly in the path of Claude Code shipped to the internet wide open, then got closed by one person in 24 hours. The scale keeps jumping and the mistakes keep happening at the same speed the fixes do. Tools evolve, threats evolve, capital moves faster than either. You stay sharp or you fall behind. That's the rush. That's why you're here.

Then → work.

---
### Sources
- [Meituan Releases LongCat-2.0: A 1.6T-Parameter Open MoE Model with Native 1M Context — MarkTechPost](https://www.marktechpost.com/2026/07/05/meituan-releases-longcat-2-0-a-1-6t-parameter-open-moe-model-with-native-1m-context-and-longcat-sparse-attention/)
- [Meituan open sources LongCat-2.0 — trained entirely on Chinese chips — VentureBeat](https://venturebeat.com/technology/meituan-open-sources-longcat-2-0-the-1-6t-near-frontier-agentic-coding-model-thats-been-leading-openrouter-trained-entirely-on-chinese-chips)
- [GitHub Copilot in Visual Studio — July update — GitHub Changelog](https://github.blog/changelog/2026-07-30-github-copilot-in-visual-studio-july-update/)
- [Nscale buys Anyscale as it seeks to own more of the AI compute stack — TechCrunch](https://techcrunch.com/2026/07/30/nscale-buys-anyscale-as-it-seeks-to-own-more-of-the-ai-compute-stack/)
- [Nscale to Buy AI Software Startup Anyscale for $1.65 Billion — Bloomberg](https://www.bloomberg.com/news/articles/2026-07-30/nscale-to-buy-ai-software-startup-anyscale-for-1-65-billion)
- [EU Pledges €10 Billion in Public Funding for New AI Data Centers — Bloomberg](https://www.bloomberg.com/news/articles/2026-07-30/eu-pledges-10-billion-in-public-funding-for-new-ai-data-centers)
- [EU opens applications for €10bn AI gigafactory scheme — Sifted](https://sifted.eu/articles/eu-opens-applications-for-e10bn-ai-gigafactory-scheme)
- [EU lays out $11.4 billion for 7 AI gigafactories — ABC News](https://abcnews.com/Technology/wireStory/eu-lays-114-billion-7-ai-gigafactories-aims-135218478)
- [Ruflo MCP Flaw Lets Unauthenticated Attackers Run Commands and Poison AI Memory — The Hacker News](https://thehackernews.com/2026/07/ruflo-mcp-flaw-lets-unauthenticated.html)
- [Maximum severity vulnerability in Ruflo AI platform allows memory tampering — SC Media](https://www.scworld.com/brief/maximum-severity-vulnerability-in-ruflo-ai-platform-allows-memory-tampering)
- [CVE-2026-59726 — NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-59726)
- [Is Claude / Anthropic AI down? [July 30, 2026] — DesignTAXI Community](https://community.designtaxi.com/topic/34294-is-claude-anthropic-ai-down-july-30-2026/)
- [Is Claude Down? Users Report AI Platform Issues as Anthropic Confirms Outage — Newsweek](https://www.newsweek.com/claude-down-outage-capacity-constraints-not-working-anthropic-12262120)
- [AI News Today, July 30 — Top AI Stories & Live Updates — AI Weekly](https://aiweekly.co/ai-news-today)
- [AI Agents News — Week of July 30, 2026 — aiagentstore.ai](https://aiagentstore.ai/ai-agent-news/this-week)
