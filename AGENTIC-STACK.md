# ⭐ Agentic Engineering Starter-Stack

**The recommended skill stack for professional, agentic software development — with structure and discipline.**

*Status: July 2026. Tested with Claude Code; most skills also run in Codex CLI, Cursor, OpenCode, and GitHub Copilot CLI.*

> This is the featured, opinionated setup of this collection. Where the [main catalog](README.md) lists *what exists*, this guide prescribes *what to actually use together* to turn coding agents into a disciplined software-engineering process.

---

## Why this stack

Coding agents write a lot of code, fast. The real problem sits *before* the first prompt: unclear requirements, no plan, no tests, no review. This stack enforces discipline at exactly those points.

It covers four phases:

| Phase | Skill | Source |
|---|---|---|
| **Clarify requirements** | `brainstorming` (Superpowers), `/grill-with-docs` (Pocock) | obra, mattpocock |
| **Specify & plan** | `writing-plans` (Superpowers), optional Spec-Kit | obra, GitHub |
| **Implement** | `test-driven-development` (Superpowers), `/tdd` (Pocock) | obra, mattpocock |
| **Debug & review** | `systematic-debugging`, subagent review (Superpowers), `/diagnose` (Pocock) | obra, mattpocock |

On top come two efficiency building blocks (`/caveman`, `skill-creator`) and a security rulebook for installing third-party skills.

---

## 1. Foundation: Superpowers (obra/superpowers)

- **Repo:** https://github.com/obra/superpowers
- **Plugin page:** https://claude.com/plugins/superpowers
- **Author:** Jesse Vincent · MIT license · actively maintained · listed in the official Claude plugin directory

Superpowers is a complete workflow framework of 20+ composable skills. It walks the agent through a fixed sequence: brainstorm → design spec → implementation plan → execution via subagents → review → merge.

### Install

```bash
# In Claude Code:
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

# Verify:
/help
# Expected commands: /superpowers:brainstorm, /superpowers:write-plan, /superpowers:execute-plan
```

### The core skills

**`brainstorming`** — Blocks any implementation until four steps are done: context exploration, clarifying questions (one at a time, Socratic), solution variants, design sign-off. The result is a design document with a self-review pass for placeholders and contradictions. Trigger: `/superpowers:brainstorm`, or automatically once the agent detects that something is to be built.

**`writing-plans`** — Breaks the approved design into 2–5-minute tasks, each with exact file paths, code, and verification steps. The bar (per the README): the plan must be clear enough that an over-eager junior with no project context and no love for testing could execute it flawlessly.

**`using-git-worktrees`** — After design sign-off, creates an isolated branch plus worktree and verifies a green test baseline before the first line of code. Also a safety measure: the agent never works directly on `main`.

**`test-driven-development`** — Enforces real red-green-refactor cycles. The test must fail before implementation code is written. YAGNI and DRY are wired in as first principles.

**`systematic-debugging`** — Four-phase method: root-cause investigation, pattern analysis, hypothesis testing, implementation. After three failed fix attempts, an architecture review is triggered automatically.

**Subagent-driven development with code review** — Per task the skill writes a failing test, then the code, refactors, and dispatches a review subagent that reads the diff cold against spec and plan. Flagged issues are fixed before the next task. If a task reveals a contradiction with the spec, the loop stops and asks.

### When Superpowers is the wrong choice

For tiny tasks the workflow is too heavy — even CSS tweaks take forever because subagents and plans spin up. Fix: for one-liners and hotfixes, simply don't trigger the brainstorming flow and work directly. Superpowers fits solo work in a single repo best; multi-repo features with strict role separation hit its limits.

---

## 2. Precision tools: mattpocock/skills (selection)

- **Repo:** https://github.com/mattpocock/skills
- **Author:** Matt Pocock · MIT license · actively maintained

The repo holds ~30 skills. Three are enough for the starter stack, a fourth is optional. Community field reports after a week of real use (devtalk.com) confirm exactly this selection.

### Install

```bash
# All skills, global:
npx skills@latest add mattpocock/skills --yes --global

# Or selectively, just the starter picks:
npx -y skills add mattpocock/skills --skill grill-with-docs --agent claude-code
npx -y skills add mattpocock/skills --skill caveman --agent claude-code
npx -y skills add mattpocock/skills --skill diagnose --agent claude-code

# Then restart Claude Code so the symlinks take effect.
# Once per repo: /setup-matt-pocock-skills  (issue tracker, labels, docs path)
```

### `/grill-with-docs`

An interview mechanism before coding. In practice the agent asks 16–50 questions per session, checks the plan against the existing domain model, sharpens terminology, and maintains a `CONTEXT.md` with project-specific vocabulary plus ADRs as decisions are made. Every later session benefits from the glossary: the agent says "Materialization Cascade" instead of twenty words of paraphrase.

Time cost: the full flow takes 15–20 minutes. Skip it for hotfixes and small features. The lean variant `/grill-me` is three sentences and works without doc upkeep. If you already run your own grill skill, take only `/grill-with-docs` for the `CONTEXT.md` value.

### `/caveman`

Strips filler, pleasantries, problem restatements, and unsolicited explanations from agent output — at full technical accuracy. An independent benchmark across 11 real dev tasks (aiagentsfirst.com) measured 294 vs. 1,214 output tokens per response — roughly 65% less. Session-scoped, triggered via `/caveman` or "caveman mode".

Caveat: on tasks with deep reasoning (complex logic, math), heavy compression can hurt quality. A March 2026 arXiv paper shows both effects: up to 26 percentage points accuracy gain on some benchmarks, losses on complex reasoning.

### `/diagnose`

Structured debugging with a real debug loop. Most valuable when error messages mislead. Overlaps with Superpowers' `systematic-debugging`; in practice, use `/diagnose` for quick one-offs and the Superpowers method inside the larger workflow.

### Optional: `/tdd`, `/to-prd`, `/handoff`

`/tdd` is strong for isolated functions; for complex UI components, test-first slows you down because tests are hard to specify up front. `/to-prd` and `/to-spec` generate requirements documents from conversations. `/handoff` writes a handover document you can pass to other agents (Codex, Copilot CLI) or a fresh Claude session.

### Known weaknesses of the repo

TypeScript bias in some misc skills (`/migrate-to-shoehorn`, `/setup-pre-commit`); the engineering skills are language-agnostic. The `CONTEXT.md` concept needs real upkeep. The grill skills need frontier models — smaller open-source models refuse to grill or bail out early.

---

## 3. Optional module: Spec-Driven Development with Spec-Kit

- **Framework:** https://github.com/github/spec-kit
- **Skill implementation:** https://github.com/SpillwaveSolutions/sdd-skill

Only add this if one of these holds:

1. The spec must be read by people who never open Claude Code (PM, business, audit).
2. The spec must live long-term as a Git artifact and outlive sessions.

This decision rule comes from the DataCamp comparison of Superpowers, Spec Kit, and BMAD-METHOD (May 2026). For everything else, Superpowers alone is enough.

The skill runs seven phases: Constitution (project principles), Specify, Clarify, Plan, Tasks, Analyze, Implement. Requirements live versioned in a `.specify/` directory; feature branches are created automatically. The sdd-skill variant also supports existing code: reverse-engineering existing projects into the SDD format and generating a constitution from existing code.

**Combined setup:** Spec-Kit for the spec phase (artifacts in Git, reviewable across the team), then point Superpowers' `subagent-driven-development` at the Spec-Kit plan file with one line of config. Result: a durable spec plus a tight implementation loop.

```bash
# Spec-Kit CLI:
uv tool install specify-cli
# Install the skill per the sdd-skill repo README
```

---

## 4. Meta-skill: skill-creator (Anthropic, official)

- **Repo:** https://github.com/anthropics/skills

```bash
/plugin install skill-creator@claude-plugins-official
```

The skill interviews you about a recurring workflow and scaffolds a clean `SKILL.md` with a keyword-rich description so the skill triggers reliably. It can evaluate and improve existing skills. This turns every repeated prompt into a versionable skill.

---

## The workflow in concert

```
Idea
 └─> /superpowers:brainstorm          (Socratic interview, design doc)
      └─> optional: /grill-with-docs   (domain check, CONTEXT.md, ADRs)
           └─> /superpowers:write-plan (2–5-min tasks, verification)
                └─> using-git-worktrees (isolated branch, green baseline)
                     └─> /superpowers:execute-plan
                          ├─> TDD: Red -> Green -> Refactor per task
                          ├─> review subagent reads each diff cold
                          └─> on spec contradiction: stop + ask
                               └─> requesting-code-review (full diff vs. spec)
                                    └─> Merge
Cross-cutting:
  /caveman   -> fewer output tokens (long sessions)
  /diagnose  -> debugging outside the big loop
  /handoff   -> handover to another agent or a fresh session
```

Rule of thumb for process weight:

| Task | Process |
|---|---|
| Typo, one-liner, CSS tweak | No skill. Work directly. |
| Small feature, bugfix with uncertainty | `/grill-me` or `/diagnose`, then directly |
| Feature with design decisions | Full Superpowers loop |
| Feature with external stakeholders | Spec-Kit + Superpowers combo |

---

## Security rules for skill installs

The skill ecosystem has a documented supply-chain problem. Snyk's ToxicSkills audit (February 5, 2026, 3,984 agent skills from ClawHub and skills.sh examined) found:

- **36% (1,467 skills)** have at least one security flaw
- **13.4% (534 skills)** contain at least one *critical*-level security issue
- **76 confirmed malicious payloads** (human-verified): credential theft, backdoors, data exfiltration
- 100% of confirmed malicious skills contain malicious code patterns; **91% also employ prompt injection** — a code scanner alone will not catch it

Source: https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/

### Scan skills before you install them

A skill is executable instruction code with access to your file system, shell, and API keys. Audit third-party skills with a dedicated scanner:

| Tool | What it does | Type | Link |
|---|---|---|---|
| **skill-security-auditor** | Static analysis of a skill (code-execution risks, prompt injection in docs, dependency supply-chain, filesystem boundaries) → PASS/WARN/FAIL verdict | Claude skill (MIT) | [Source](https://github.com/alirezarezvani/claude-skills) |
| **Cisco Skill Scanner** | Open-source CLI: signature + LLM-as-judge + behavioral dataflow detection of prompt injection, data exfiltration, and malicious patterns; SARIF/HTML/JSON output | CLI tool (open source) | [Source](https://github.com/cisco-ai-defense/skill-scanner) |
| **Snyk Agent Scan** | Scanning extended to skills alongside agents and MCP servers | Commercial service | [Source](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) |

Five rules follow for this repo:

1. **Vetted sources only.** Install exclusively from large, actively maintained repos (obra, mattpocock, anthropics, github) or official plugin marketplaces. Every skill in this document meets that bar.
2. **Read `SKILL.md` before installing.** Red flags: hidden bash calls, `curl`/`wget` to foreign domains, access to `.env`, credentials or SSH keys, instructions to ignore previous instructions.
3. **No permission bypasses on your work machine.** Use `--dangerously-skip-permissions` / `bypassPermissions` only in isolated containers or VMs, as Anthropic's deployment guidance prescribes.
4. **Worktrees by default.** Superpowers' `using-git-worktrees` isolates agent work from the main branch and limits the blast radius of misguided actions.
5. **Treat updates like dependencies.** Review skill updates by diff before they land globally. A skill is executable instruction code with access to the file system, shell, and API keys.

---

## Full install (copy-paste)

```bash
# 1. Superpowers (foundation) — run inside Claude Code:
#    /plugin marketplace add obra/superpowers-marketplace
#    /plugin install superpowers@superpowers-marketplace

# 2. Pocock selection
npx -y skills add mattpocock/skills --skill grill-with-docs --agent claude-code
npx -y skills add mattpocock/skills --skill caveman --agent claude-code
npx -y skills add mattpocock/skills --skill diagnose --agent claude-code

# 3. Skill-creator (official) — inside Claude Code:
#    /plugin install skill-creator@claude-plugins-official

# 4. Restart Claude Code, then per repo:
#    /setup-matt-pocock-skills

# 5. Optional, if needed: Spec-Kit
uv tool install specify-cli
```

---

## Sources

- obra/superpowers: https://github.com/obra/superpowers
- Superpowers in the Claude plugin directory: https://claude.com/plugins/superpowers
- mattpocock/skills: https://github.com/mattpocock/skills
- anthropics/skills: https://github.com/anthropics/skills
- GitHub Spec-Kit: https://github.com/github/spec-kit
- SDD-Skill: https://github.com/SpillwaveSolutions/sdd-skill
- Field report on mattpocock/skills (1 week): https://devtalk.com/t/anyone-tried-mattpocock-skills-for-claude-code-here-is-what-i-found-after-a-week/244771
- Caveman benchmark: https://aiagentsfirst.com/mattpocock-skills-claude-code-framework
- Framework comparison Superpowers vs. Spec Kit vs. BMAD: https://www.datacamp.com/tutorial/spec-driven-development-with-claude-code
- Snyk ToxicSkills audit: https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/
- Claude Code security docs: https://code.claude.com/docs/en/security
