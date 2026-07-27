# Daily Debrief: 100x Dev Scan
**Date:** 2026-07-20
**Mood:** wired
**Note:** first debrief in this repo. no baseline to diff against. everything below = new to log.

---

Morning. Sun up, terminal up. Scan hits:

## Tools & agents
- Copilot: Kimi K2.7 Code hit GA inside Copilot. Also agent session streaming, public preview. Watch new AI credit/session limits, they changed too.
- GitHub Models RETIRES July 30. If pointed at it, migrate now, not later.
- MCP spec 2026-07-28 release candidate — biggest rev since launch. Stateless core. MCP Apps (server renders real HTML UI inside agent). Tasks extension for long-running async work. OAuth/OIDC baked in.
- AgentPrizm shipped AgentMemory + AgentSkills (Jul 9): REST + MCP combo, persistent agent memory across sessions. No more re-explaining yourself to your own agent.
- Continue (open source agent CLI) was the ONLY tool in a field of 11 that mitigated the GuardFall shell-injection class by default. Worth a look if you're picking an agent harness.

## AI news — model drops
- OpenAI GPT-5.6 family (Jul 9): Sol (top reasoning/coding/science), Terra (5.5-quality, half cost), Luna (cheap/fast/high-volume).
- Anthropic: Opus 4.7 / Sonnet 4.6 got deeper repo-level agent behavior. Claude Fable 5 came back Jul 1 after export-control suspension.
- xAI Grok 4.5 (Jul 16): 1.5T param MoE, trained ON Cursor interaction data. 83.3% Terminal-Bench 2.1. ~4.2x fewer output tokens than Opus 4.8 on SWE-Bench Pro. $2/$6 pricing. Now default in Grok Build, live in Cursor.
- Moonshot Kimi K3 dropped same day as Grok 4.5 (Jul 16). Four labs, one week. That's not a coincidence, that's a race.
- Meta Muse Spark 1.1: 1M token context + computer-use across desktop/browser/mobile.
- Google Gemini 3.5 Live Translate: 70+ languages, near-real-time speech-to-speech.

## Features — platform stuff
- MCP Tasks extension = agents can fire long-running work without holding the connection hostage. Real async pattern, not a hack.
- MCP Apps = server-rendered interactive UI INSIDE the agent session. No more text-only tool output.
- PyTorch 2.13: ~12x sparse-attention speedup claimed on Apple Silicon.

## News cycle — threats worth knowing
- **GuardFall**: shell-injection guard bypass class. Hits 10 of 11 surveyed open-source coding agents — Aider, Cline, Goose, Open Interpreter, OpenHands, opencode, Plandex, Roo-Code, SWE-agent, Hermes. Root cause: the guard checks raw command text, bash rewrites/expands that text AFTER the guard looks at it (quoting, $IFS, substitution). Guard and shell never see the same command. No single CVE — it's a design flaw baked into the whole category.
- **Claude Code GitHub Action poisoning**: `checkWritePermissions` trusted ANY actor ending in `[bot]`, no real check. Attacker opens a malicious issue → triggers the workflow → Claude Code auto-runs `cat`/`head` without asking → reads `/proc/self/environ` → grabs OIDC token vars → exchanges for a privileged GitHub App token with WRITE access to the action's own source → poisons it for every repo pinned to a floating tag. Patched in v1.0.94. This already happened for real once: Cline's claude-code-action got hit in Feb, npm token stolen, unauthorized `cline@2.3.0` pushed.
- 78% of orgs now report AI incidents or vulnerabilities. Adoption outran the guardrails. Again.

## 100x patterns
- Grok 4.5's real story isn't the benchmark, it's the token efficiency — same or better output for a fraction of the tokens. That's direct $ and latency arbitrage on every agent loop you run.
- MCP Tasks extension kills the need for your own janky "keep the agent alive" infra for long jobs. Standardize on it.
- Pick agent tooling that fails safe BY DEFAULT (see: Continue) over tooling you have to manually harden after the fact. Cheaper than getting burned.

## The meta
Same week four labs ship frontier models AND a shell-injection class breaks 10 of 11 agents you might be running on auto-execute right now. Both things are true at once. That tension IS the job. You picked a field where the tools that make you 100x faster are the same tools that can 100x your blast radius if you don't read the fine print. That's not a bug in the career choice. That's the whole game.

---

## Pick 3 signals

**1. Grok 4.5 in Cursor**
- Will I use this? Probably yes — cheap, fast, trained on the exact tool I already run.
- Level me up? Yes, if the efficiency claim holds under real workloads, not just benchmark conditions.
- 10x moment hiding? Yes — cost/latency arbitrage compounds across every agent call you make.
- Break anything? No, but don't trust the benchmark table blind — Grok was scored at "high" effort, Opus/Fable at "max." Not apples to apples.

**2. Claude Code GitHub Action supply chain flaw**
- Will I use this? Yes — go check your own repos TODAY if you pin claude-code-action to a floating tag.
- Level me up? Yes — forces better CI/CD hygiene (pin to SHA, not tag).
- 10x moment hiding? No. This is a stop-and-check item, not a growth item.
- Break anything? Yes, already did, for real, to a real project (Cline). Could've been you.

**3. MCP 2026-07-28 spec (Tasks + Apps + OAuth)**
- Will I use this? Yes, if building anything agent-facing.
- Level me up? Yes — standardized async task pattern removes custom plumbing you'd otherwise hand-roll.
- 10x moment hiding? Yes — real UI inside agent sessions changes what "agent tool" even means.
- Break anything? Maybe — spec's still RC, expect breaking changes vs whatever you build against it now.

---

## Reflect (30s)
This craft is alive and dangerous in the best way. Tools evolve. Threats evolve. You stay sharp or you fall behind. That's the rush. That's why you're here.

Then → work.
