# Daily Debrief: 100x Dev Scan — 2026-07-12

*(first scan. no old logs to check against. clean slate.)*

Morning. Scan hits:

## Tools & agents
- **Fable 5 back online.** Anthropic flip switch July 1, US export ban lifted. Full Claude.ai, Claude Code, Cowork access again. Beast was caged 3 weeks, now loose.
- **GPT-5.6 family (Sol, Terra, Luna) GA July 9.** Now ChatGPT default. GPT-5 Turbo variant: 40% cheaper, only 6-8% behind full GPT-5. Cost-per-token war heating up.
- **Sonnet 5 intro pricing:** $2/$10 per million, near-Opus 4.8 performance. Cheap smart. Grab it before Aug 31 window closes.
- **Google Antigravity 2.0** dropped at I/O 2026. Full agent-first platform, free preview. Windsurf still king of parallel multi-worktree agent runs ($15/mo).
- **Claude Code desktop got a built-in browser.** Agent can click, read, navigate live sites like it does local dev previews. Sandboxed. This is a real unlock for debugging against live docs/staging.
- **`/doctor` (aka `/checkup`) now self-heals.** Finds dead skills, duplicate CLAUDE.md files, unused MCP servers, trims bloat automatically. One command, less rot.

## AI news
- MCP spec **locks final July 28, 2026** — 10-week test window closing now. If you're building on MCP, freeze assumptions this month or get burned by drift.
- Microsoft pushing Dataverse coding-agent plugin into Claude, Cursor, Copilot — cross-vendor agent data plumbing becoming a thing. Vendor lock-in cracking open a little.
- NanoBanana 2 Lite (Google): image gen under 4 sec, $0.034/1000 images. Image gen commoditizing hard.

## Features / hidden tricks
- `/doctor` dedup trick above — use it weekly, not just when broken.
- Claude Code browser mode = skip manual screenshot pasting for live-site debug loops.
- Enterprise MCP connector provisioning (Okta) — if you're on a team plan, zero-touch connector access now exists. Ask your admin.

## News cycle — threats worth knowing
- **GhostApproval attack**: malicious repo plants a symlink, AI coding agent asks "write to this harmless-looking file?" — you say yes, write actually lands on a sensitive system path. Decades-old symlink trick, new agent victim. **Check what you're actually approving before you click yes in Claude Code / Cursor.**
- **Skill scanners get owned**: security scanners for AI-agent "skills" get bypassed >90% of the time by the best evasion trick tested. Installing random community skills = installing random unverified code. Don't.
- **China flagged Claude Code as backdoor risk** (CNBC, July 8). Geopolitics now shapes which agent stack you're "allowed" to trust. Watch this if you work adjacent to regulated/gov contracts.
- **"Bad Epoll" CVE-2026-46242** — Linux kernel local privesc via epoll race + use-after-free. Patch your boxes.
- Attackers using SEO poisoning + hidden HTML prompt injection to get agents to make fraudulent payments autonomously. Your shopping/payment agent is now an attack surface.

## 100x patterns
- Orchestration > raw autonomy. HN consensus: skills beat prompts, verification is the bottleneck, workflows matter more than demos. Translation — stop admiring one-shot demos, build the harness around the agent.
- **Tokenmaxxing is dying.** Amazon killed its internal token-usage leaderboard ("Kirorank") after devs gamed it — burning tokens ≠ shipping value. Measure output, not spend. Don't cargo-cult "more agent calls = more 10x."
- 10x engineer → 100x engineer isn't "type faster." It's orchestrating fleets of agents that do the typing. If you're still hand-driving every diff, you're leaving multiplier on the table.

## The meta
Model prices dropping, capability climbing, tools self-healing, attackers moving in minutes not days. Whole field resets every quarter. That's not chaos — that's the game.

---

## Pick 3 signals

**1. Claude Code `/doctor` self-heal + browser mode**
- Will I use this? Yes — reduces manual cleanup + screenshot-paste debugging.
- Level me up? Yes, small compounding time-save daily.
- 10x hiding? No, but it's a real friction killer.
- Breaks anything? No.

**2. GhostApproval symlink attack on AI coding agents**
- Will I use this? N/A — it's a threat, not a tool. But I will change behavior: read the actual write target before approving.
- Level me up? Yes — security awareness is a skill multiplier, not just a tax.
- 10x hiding? No.
- Breaks anything? Yes — could break your machine/creds if ignored. This is the one that bites you asleep at the wheel.

**3. Orchestration-over-autonomy shift (skills > prompts, verification is the bottleneck)**
- Will I use this? Yes — rethink how I structure agent tasks, invest in verify steps not just prompt tweaks.
- Level me up? Yes, directly — this is the actual 100x lever right now.
- 10x hiding? Yes — this is the real one. Whoever nails "verified autonomous orchestration" first wins the decade.
- Breaks anything? No, but ignoring it means competitors lap you.

---

## Reflect (30s)

This craft is alive and dangerous in the best way. Model that costs $2/M today makes yesterday's SOTA look like a toy. Same week, a symlink trick from decades ago just walked past a brand new AI agent's defenses like it was nothing. Tools evolve. Threats evolve just as fast, sometimes using the *exact same old tricks* nobody bothered to re-check. You stay sharp or you get owned by 2004-era symlink abuse through a 2026 AI agent. That's the rush. That's why you're here. Also, yeah — some days you wonder if you should've just done plumbing. Then Fable 5 comes back online and you remember: no, this is the good chaos.

Then → work.

---

**Emotion: wired**
