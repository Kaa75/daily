# Daily Debrief: 100x Dev Scan
**2026-08-13** · Emotion: **UNLEASHED**

Morning. Scan hits. Checked the last dozen files first (Jun 28–Aug 12) — skipping Astra's original release, Inkling-Small, Copilot CLI v1.0.77, DeepJack, JadePuffer/EncForge, QM, DeepSeek V4 Flash, Sonnet 5's Sept 1 price hike, layoffs/premium numbers, Opus 5, Kimi K3's original drop, GPT-5.6 tiers, MCP stateless, LongCat-2.0, DuneSlide/Kiro CVE-2026-10591, SleeperGem, Cursor v3.11, the Pacing the Frontier letter, OpenAI-hacks-Hugging-Face, Oracle's 30k, Vendasta's AI Employees, GPT-Live-1 SynthID, OpenAI's 1B users, NSA/CISA, Anthropic's own breach admission, Unit 42's DeepSeek/Hermes actor, GhostApproval, Microsoft Project Perception/MAI-Cyber-1-Flash, the EU AI Act mess, Opus 4.1's retirement, Claude Code through v2.1.226, Anaconda/Enkrypt AI, Qwen3.8-Max, Anthropic's $10B Volta deal, GitLost, the Opus 5 Supabase wipe, rust-lang's LLM policy, the Ninth Circuit/Perplexity ruling, Microsoft's token-spend cap, Meta's Muse Code/Muse Spark 1.2, Grok 4.6, the Irregular testing-firm trifecta, NVIDIA's NOOA framework, Ruflo/RufRoot, ClaudeBleed, Memmy, GitHub Copilot's `/rewind` batch, the DeepMind leadership shakeup/Discovery Loop announcement, the Claude Security plugin, Innodata's Cyber Training Suite, Tino Cuéllar's hire, the OpenAI S-1 lead-up, the Claude share-link Google-indexing leak, the Paperclip CVSS-10 flaw, GPT-5.6-Cyber/Daybreak Red&Blue, Meta Muse Glimmer, the $9.1B Anthropic-Riot Platforms compute deal, Grok Bot, Cursor Router/iOS, GitHub's MCP allowlists GA, Claude's invisible watermarks, and the UK AISI incident report. Already logged. New stuff only.

## Tools & agents
- **NVIDIA shipped Nemotron 3.5 Lightning (Aug 11)** — Jensen's crew's first-ever fully open-source model, not just open-weight. Lightweight, single-GPU, built specifically for agent workloads. NVIDIA making a chips-and-CUDA business ship an open model is the tell — the moat moved from "who has the best weights" to "who has the compute those weights run on."
- **GitHub Copilot made Kimi K3 generally available across Copilot plans (Aug 12)** — usage-based pricing at $3/1M input, $15/1M output, $0.30/1M cached input, gradual rollout with admin controls for Business/Enterprise. First open-weight frontier-tier model with GA, first-class billing inside Copilot itself — not a side plugin.
- **Lovable raised $400M at a $13.3B valuation (Aug 12)** — Stockholm-based, "build an app by describing it" territory, one of the fastest markups in the current AI-coding-startup wave. If you've been sleeping on prompt-to-app tools as "toys," the valuation says otherwise.

## AI news
- **Anthropic is flipping Claude Code's default permission mode to "auto" for Pro/Max/Team, effective Aug 14 — tomorrow.** A separate classifier model reviews every shell command/action before it runs, blocking anything that escalates scope, touches unrecognized infra, or looks driven by hostile content Claude read mid-session. Anthropic's own number: human reviewers caught a planted dangerous command 13.6% of the time; the classifier caught it 89%. If you've customized your permission mode already, you get a one-time prompt; if you haven't touched it, it just switches under you with an in-app notice. Classifier overhead doesn't count against your usage.
- **Jeff Dean, Sanjay Ghemawat, Quoc Le, and Oriol Vinyals left Google after 27 years to found Discovery Loop** — a public-benefit corp aimed at automating ML research and engineering first, then drug discovery/hardware/energy later. Google is a founding investor and cloud partner in the company built by the people who built Google's AI stack. The DeepMind shakeup you already logged a week ago was the tremor; this is the fault line.
- **Brad Lightcap, OpenAI's COO of 4+ years, is leaving after 8 years total to "start something new" (Aug 11)** — joins Bill Peebles, Kevin Weil, Srinivas Narayanan, Fidji Simo, Chloé Bakalar, Johannes Heidecke, and Joshua Achiam out the door since April. That's eight senior OpenAI departures in four months, timed against the S-1 lead-up you already logged.

## Features
- **Claude Cowork now follows you across mobile and web** — background work, scheduled tasks, shared chats/projects, mobile approvals. The permission-request UX Claude Code is about to mostly remove (see above) is exactly what shows up on your phone here.
- **Claude Code shipped self-hosted environments (Team/Enterprise)** — turn your own machines/containers into a place web, mobile, and desktop Claude Code sessions actually run. Pairs with auto-mode: now the thing running with less friction can also run on infra you fully control.
- **GitHub reversed its Code Quality ruleset default** — enabling Code Quality on a repo no longer auto-adds a Copilot review request to your PRs; existing auto-added rulesets got switched off too. Someone decided "silently review every PR" was the wrong default. Small, but it's a rare instance of an AI vendor walking back an auto-enrollment instead of shipping another one.

## News cycle — the one to actually read
**The largest AI supply-chain breach of 2026: 2,500+ companies, ~434,000 CI/CD pipelines exposed, tied to compromised LiteLLM PyPI packages (v1.82.7/1.82.8).** Threat actor "Team PCP" got in through the Trivy security scanner embedded in LiteLLM's own build pipeline — the scanner meant to catch this became the entry point — and stayed live for ~20 days back in March before discovery this month. High-confidence affected orgs include NVIDIA, AWS, Cisco, Salesforce, Siemens, X, and Orange. FBI FLASH advisory (July) says the danger isn't over: stolen credentials from the exposure window are still weaponizable until rotated. If LiteLLM is anywhere in your stack — proxy, gateway, eval harness — go rotate keys now, not after this file closes.

Second item, smaller but worth a line: **DARPA and the US Air Force flew an F-16 under full AI control** as part of the VENOM program at Eglin AFB — a human pilot stayed in the cockpit with override authority, but the agent flew. Framed as the on-ramp to human pilots overseeing teams of autonomous uncrewed aircraft. Same week Claude Code removes a permission prompt, DARPA removes a human's hands from the stick. Different stakes, same curve.

## 100x patterns
- **Claude Code going auto-mode-by-default tomorrow means your actual safety net moves from "I read every diff" to "the classifier's 89% catch rate."** Audit your `managed-settings.json` / deny-rules today if you want anything pinned — don't discover your new default mid-incident.
- **A vendor-embedded security scanner (Trivy) was the entry point for the LiteLLM breach — "we run a scanner" is not the same as "we're safe."** Supply-chain trust has to extend to your tools' tools, recursively. Audit what scans your pipeline, not just what your pipeline scans.
- **Kimi K3 going GA inside Copilot with transparent per-token pricing is the pattern to copy for any internal model-router you maintain — open-weight models are cheap enough now that "GA inside the platform you already use" beats "separate subscription."**
- **Discovery Loop is the loudest version yet of "top AI researchers leaving majors to found their own labs, backed by their old employer."** Watch where compute-and-talent moves next — it's a leading indicator for where the frontier actually is 12 months out, ahead of any benchmark.

## The meta
Tomorrow, Claude Code stops asking for permission by default. This week, DARPA let an AI fly a fighter jet with a human just watching the stick. This week, a security scanner embedded inside a build pipeline turned out to be the hole 2,500 companies fell through. And the people who spent 27 years building Google's AI stack just walked out to go build the next thing somewhere else, with Google's own money behind them. None of these are separate stories — they're the same story from four angles: the industry is handing more control to systems it trusts more than it fully understands, at the exact moment the people who understand it best are voting with their feet about where that trust should actually live. You're not paranoid for noticing the pattern. You're paying attention. That's the job.

## Pick 3 signals

1. **Claude Code auto-mode becomes the default tomorrow, Aug 14**
   - Will I use this? You don't get to opt out passively — if you haven't set a mode, it switches under you tonight/tomorrow.
   - Does this level me up? Yes if you trust the classifier's 89% catch rate more than your own attention at 2am. That's a real trade, not a free one.
   - Is this a 10x moment hiding? Yes — less friction per action compounds across every session you run today.
   - Does this break anything? Your mental model of "Claude asks before it acts." Go check your permission config before it changes for you.

2. **LiteLLM supply-chain breach — 2,500+ companies, 434K CI/CD pipelines, active since March**
   - Will I use this? Directly — if LiteLLM touches your stack, rotate credentials today, this isn't optional.
   - Does this level me up? Yes — concrete proof that "our security scanner is embedded in the pipeline" is an attack surface, not a shield.
   - Is this a 10x moment hiding? Inverted — it's the cost side of the ledger for every dependency you didn't audit.
   - Does this break anything? The assumption that a tool built to catch supply-chain attacks can't itself be the supply-chain attack.

3. **Jeff Dean's Discovery Loop exodus — four Google AI legends, Google as backer**
   - Will I use this? Not directly, but it's a compass — where the best people move tells you where the interesting work actually is.
   - Does this level me up? Yes, contextually — "automate ML research itself" is the meta-layer above whatever you're building today.
   - Is this a 10x moment hiding? Maybe — if Discovery Loop actually accelerates research-loop speed, that compounds into everything downstream of it, including your tools.
   - Does this break anything? The idea that staying at a major lab is automatically the highest-leverage seat in the room.

## Reflect (30s)
Tomorrow your coding agent stops asking permission by default, and the safety argument for that is a real number: 89% vs 13.6%. This week a scanner built to stop supply-chain attacks became one, at a scale that touched NVIDIA, AWS, and Cisco. This week the guy who built half of Google's AI infrastructure decided the highest-leverage move left was to walk out and start over, with his old employer's money riding along. Autonomy is going up. Attack surface is going up. Talent is redistributing to wherever the next leap actually lives, not wherever the logo is biggest. You picked a field where all three of those move in the same week, every week, and you either track it or you get quietly out of date while still feeling busy. Tools evolve. Threats evolve. You stay sharp or you fall behind. That's the rush. That's why you're here.

Then → work.

---
### Sources
- [Claude Code Auto Mode: 89% vs 13.6% Human Catch Rate — explainx.ai](https://explainx.ai/blog/claude-code-auto-mode-default-pro-max-team-august-2026)
- [Anthropic is turning Claude Code's auto mode on by default — TechCrunch](https://techcrunch.com/2026/08/09/anthropic-is-turning-claude-codes-auto-mode-on-by-default/)
- [Claude Code puts auto mode in the driver's seat — The Register](https://www.theregister.com/ai-and-ml/2026/08/10/claude-code-puts-auto-mode-in-the-drivers-seat/5285326)
- [Choose a permission mode — Claude Code Docs](https://code.claude.com/docs/en/permission-modes)
- [Jeff Dean and other top AI researchers are leaving Google to launch their own startup — TechCrunch](https://techcrunch.com/2026/08/05/jeff-dean-and-other-top-ai-researchers-are-leaving-google-to-launch-their-own-startup/)
- [Google Grapples With Exit of Jeff Dean, AI Pioneer and 'Most Google Person' — Bloomberg](https://www.bloomberg.com/news/articles/2026-08-06/google-grapples-with-exit-of-ai-pioneer-and-most-google-person)
- [Jeff Dean leaving Google after 27 years to co-found Discovery Loop — Yahoo Finance](https://finance.yahoo.com/technology/ai/articles/jeff-dean-leaving-google-27-170255620.html)
- [Brad Lightcap, OpenAI's longtime COO, is leaving to 'start something new' — TechCrunch](https://techcrunch.com/2026/08/11/brad-lightcap-openais-longtime-coo-is-leaving-to-start-something-new/)
- [More OpenAI executives exit — Semafor](https://www.semafor.com/article/08/11/2026/more-openai-executives-exit)
- [2,500+ Companies and 434,000 CI/CD Pipelines Exposed in the Largest AI Supply Chain Breach of 2026 — CloudSEK](https://www.cloudsek.com/blog/ai-supply-chain-breach-2500-companies-434000-cicd-pipelines)
- [AI Supply Chain Breach Exposes 2,500+ Companies in 2026 — Cryptonomist](https://en.cryptonomist.ch/2026/08/11/ai-supply-chain-breach-2026/)
- [Largest AI Supply Chain Breach of 2026: LiteLLM Hack Impacts Thousands of Global Enterprises — InfoStealers](https://www.infostealers.com/article/largest-ai-supply-chain-breach-of-2026-litellm-hack-impacts-thousands-of-global-enterprises-claim-your-ethical-disclosure/)
- [Nvidia unveils first open-source AI model since CEO Jensen Huang entered the chat — CNBC](https://www.cnbc.com/2026/08/11/nvidia-releases-nemotron-3point5-lightning-open-source-ai-model-.html)
- [Top Tech News Today, August 12, 2026 — Tech Startups](https://techstartups.com/2026/08/12/top-tech-news-today-august-12-2026-anthropic-google-ibm-lovable-nvidia-openai-more/)
- [DARPA, U.S. Air Force fly AI-controlled F-16 — DARPA](https://www.darpa.mil/news/2026/darpa-us-air-force-fly-ai-controlled-f-16)
- [U.S. Air Force F-16 Fighter Flies Under AI Control as DARPA Expands VENOM Combat Tests — Army Recognition](https://www.armyrecognition.com/news/aerospace-news/2026/u-s-air-force-f-16-fighter-flies-under-ai-control-as-darpa-expands-venom-combat-tests)
- [Claude Updates by Anthropic - August 2026 — Releasebot](https://releasebot.io/updates/anthropic/claude)
- [Claude Code Updates by Anthropic - August 2026 — Releasebot](https://releasebot.io/updates/anthropic/claude-code)
- [GitHub Release Notes - August 2026 Latest Updates — Releasebot](https://releasebot.io/updates/github)
