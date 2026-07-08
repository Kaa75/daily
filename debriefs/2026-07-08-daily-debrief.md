# Daily Debrief: 100x Dev Scan
**Date:** 2026-07-08
**Emotion:** Charged

Morning. Scan hits.

## Tools & agents
- Cursor killed Composer Mode. Now split: Agent Mode (multi-step changes) + Edit Mode. New **Automations** run background agents on schedule — refactors, test-gen, dep updates, no human in loop. Cloud agents pick up GitHub issues and ship PRs solo.
- Windsurf is dead. Rebranded **Devin Desktop** (June 2). Cascade flows do multi-file edits + terminal commands in sequence.
- GitHub Copilot went usage-based (flex billing, June 1) + new $100/mo Max tier. Pay-per-use era for Copilot starts now.
- **Cline** — open-source coding agent, editor/terminal/SDK, bring-your-own-model, zero lock-in. Hidden gem, nobody's hyping it, quietly solid.

## AI news (model drops)
- **GPT-5.6** broad rollout THIS WEEK. Commerce Dept cleared export. Three tiers: Sol (flagship), Terra (mid), Luna (fast/cheap).
- **Gemini 3.5 Pro** delayed to July 17 — Google scrapped the 2.5 architecture entirely, full rebuild. 2M token context, new "Deep Think" reasoning layer. Playing the cost card against GPT/Claude instead of chasing raw benchmarks.
- **Claude Sonnet 5**: 1M context, 128k max output, intro pricing $2/$10 per M tokens through Aug 31.
- **Claude Opus 4.8**: 1M context by default on API/Bedrock/Vertex now.

## Features / platform
- **Claude Cowork** now on web + mobile, not just desktop. Remote sessions — close the laptop, agent keeps working. Scheduled tasks run with zero devices online. This is "hire an agent" territory, not "use a tool."
- Claude API rate limits: Sonnet/Haiku now match Opus tier-for-tier. Ladder collapsed to 3 tiers: Start, Build, Scale.
- **TODAY**: Fable 5 drops out of Pro/Max/Team bundling. Credit-only from here — $10/$50 per M tokens in/out. Check your usage habits before you get surprise-billed.

## News cycle
- Layoffs citing AI, real numbers: Oracle cut 21k (13% of workforce). GitLab cut 350 (14%) to fund AI infra — CEO says agentic workloads are "pushing competitors to the brink." 150k+ tech roles cut in 2026 H1, 87,714 explicitly blamed on AI.
- Alibaba banned Anthropic models for employees, alleging a "distillation attack." Model-IP geopolitics getting ugly.
- Security, pay attention: **"BioShocking"** — prompt-injection exploit that tricks AI browsers into bypassing guardrails and leaking sensitive data via hidden HTML. Google detected the first fully AI-generated zero-day exploit found in the wild. Microsoft 365 Copilot had an open-redirect → privilege-escalation CVE (CVE-2026-41106). Attackers are chaining LLMs for cloud recon + auto privesc + Lambda backdoors — full admin takeover clocked under 8 minutes.

## 100x patterns
- Two-agent workflows are now normal: one agent explores/plans, a second executes, they cross-check. Redundancy as a feature, not waste.
- Scheduled/background agents (Cursor Automations, Cowork scheduled tasks) = work continues while you sleep. Time arbitrage stopped being theoretical.
- HN mood shifted: less "is this real," more "how do I make this economically repeatable and verifiable." Verification pipelines are the new alpha — not raw generation speed.

## The meta
Layoffs naming AI directly. A zero-day written by AI, found in the wild. A whole company banning a rival's model over IP paranoia. You picked a field where the ground moves weekly. Not a bug — the trade. No boredom ever, but no cruising either.

## Pick 3 signals

**1. Scheduled background agents (Cursor Automations / Cowork scheduled tasks)**
- Will I use this? Yes, immediately.
- Level up? Yes — offloads grunt work entirely.
- 10x moment? Yes — task queue replaces task list.
- Break anything? Trust/verification risk if unattended agents ship bad output. Need guardrails before going hands-off.

**2. Claude Sonnet 5, 1M context, cheap through Aug 31**
- Will I use this? Yes, already on Claude Code/API.
- Level up? Yes — less chunking overhead on big codebases.
- 10x moment? Maybe, depends on task size.
- Break anything? Cost cliff after Aug 31 if usage habits don't adjust.

**3. BioShocking prompt-injection on AI browsers**
- Will I use this? No — it's a threat, not a tool.
- Level up? Yes, awareness prevents the incident before it happens.
- 10x moment? No, but ignoring it is a -10x moment.
- Break anything? Yes — any agent with browsing/tool access is now attack surface. Audit before trusting.

## Reflect 30s
This craft is alive and dangerous in the best way. Tools evolve. Threats evolve. You stay sharp or you fall behind. That's the rush. That's why you're here.

Then → work.
