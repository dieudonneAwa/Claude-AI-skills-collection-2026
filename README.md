# 📦 Claude Skills Collection

**A curated collection of official and community-built Claude Skills.**

Anthropic Skills are modular tools that extend the capabilities of Claude AI — unlocking workflows for coding, document creation, design, data analysis, research, and more.

This repository gathers and organizes publicly available Claude Skills, including both official tools by Anthropic and creative contributions from the community. Browse by category, explore capabilities, and kickstart your own Skill creation.

![Skills](https://img.shields.io/badge/skills-94-blue) ![Categories](https://img.shields.io/badge/categories-15-green) ![Links checked](https://img.shields.io/badge/links%20checked-Jul%202026-brightgreen) ![Standard](https://img.shields.io/badge/Agent%20Skills-open%20standard-orange)

> 💡 **Note:** Skills require Claude Pro, Max, Team, or Enterprise access with code execution enabled.
> Since December 2025, Agent Skills are also an **open standard** ([agentskills.io](https://agentskills.io)) — a skill you build for Claude can, in principle, run on any platform that adopts the spec.

*Last reviewed: July 2026 · 94 skills across 15 categories · all source links verified against the GitHub API.*

---
## ⭐ Featured: Agentic Engineering Starter-Stack

**The recommended skill stack for professional, agentic software development — with structure and discipline.**

Coding agents write a lot of code, fast. The real problem sits *before* the first prompt: unclear requirements, no plan, no tests, no review. This curated stack enforces discipline at exactly those points, turning coding agents into a repeatable software-engineering process.

| Phase | Recommended skills | Source |
|---|---|---|
| **Clarify requirements** | `brainstorming`, `/grill-with-docs` | obra, mattpocock |
| **Specify & plan** | `writing-plans`, optional Spec-Kit | obra, GitHub |
| **Implement** | `test-driven-development`, `/tdd` | obra, mattpocock |
| **Debug & review** | `systematic-debugging`, subagent review, `/diagnose` | obra, mattpocock |

```
Idea
 └─> brainstorm ─> (grill-with-docs) ─> write-plan ─> git-worktree
       └─> execute-plan: TDD (Red→Green→Refactor) + cold-read review subagent
             └─> code-review vs. spec ─> Merge
 cross-cutting:  /caveman (fewer tokens) · /diagnose (debug) · /handoff (agent handover)
```

> 📖 **[Read the full guide → AGENTIC-STACK.md](AGENTIC-STACK.md)** — install commands, every skill explained, the optional Spec-Kit module, and security rules for installing third-party skills.

---
## 🛡️ Skill Safety & Auditing

**A skill is executable instruction code with access to your file system, shell, and API keys — treat it like a dependency, not a document.** A [Snyk ToxicSkills audit](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) (Feb 2026, 3,984 skills) found **36% (1,467) with at least one security flaw**, **13.4% (534) with critical issues**, and **76 human-confirmed malicious payloads** (credential theft, backdoors, data exfiltration). Every entry here links to its original source so you can inspect it first — but source sizes vary, so scan before you install, especially for smaller repos.

| Tool | What it does | Type | Link |
|------|-------------|------|------|
| **skill-security-auditor** | Static analysis of a skill (code-execution risks, prompt injection in docs, dependency supply-chain, filesystem boundaries) → PASS/WARN/FAIL verdict | Claude skill (MIT) | [Source](https://github.com/alirezarezvani/claude-skills) |
| **Cisco Skill Scanner** | Open-source CLI combining signature, LLM-as-judge, and behavioral dataflow detection; SARIF/HTML/JSON output | CLI tool (open source) | [Source](https://github.com/cisco-ai-defense/skill-scanner) |
| **Snyk Agent Scan** | Scanning extended to skills alongside agents and MCP servers | Commercial service | [Source](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) |

**Five rules before installing any skill:** (1) vetted sources only, (2) read the `SKILL.md` first, (3) no permission bypasses outside a sandbox, (4) run agents in isolated git worktrees, (5) review skill updates by diff like dependencies. → [Full rationale in AGENTIC-STACK.md](AGENTIC-STACK.md#security-rules-for-skill-installs)

---
## 📚 Table of Contents
- [⭐ Featured: Agentic Engineering Starter-Stack](AGENTIC-STACK.md)
- [🛡️ Skill Safety & Auditing](#-skill-safety--auditing)
- [What Are Claude Skills?](#what-are-claude-skills)
- [📄 Document Skills](#-document-skills)
- [🎨 Creative & Design](#-creative--design)
- [💻 Development & Code Tools](#-development--code-tools)
- [📊 Data & Analysis](#-data--analysis)
- [🔬 Scientific & Research Tools](#-scientific--research-tools)
- [📝 Writing & Research](#-writing--research)
- [📚 Learning & Knowledge](#-learning--knowledge)
- [🎥 Media & Content](#-media--content)
- [🤝 Collaboration & Project Management](#-collaboration--project-management)
- [🔐 Security & Testing](#-security--testing)
- [⚙️ Utility & Automation](#-utility--automation)
- [🤖 AI & Machine Learning](#-ai--machine-learning)
- [☁️ Cloud & Infrastructure](#-cloud--infrastructure)
- [💼 Business & Marketing](#-business--marketing)
- [📈 Productivity & Organization](#-productivity--organization)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [License](#license)

---
## What Are Claude Skills?
Claude **Skills** are specialized modules that Claude can use to perform structured, multi-step tasks. Each skill is a lightweight folder built around a required `SKILL.md` file, and optionally includes Python code, templates, reference docs, and assets.

Skills allow Claude to:
- Create and edit documents (Word, Excel, PowerPoint, PDF)
- Parse and analyze structured data
- Write and debug code
- Generate creative visual assets
- Automate research, testing, or collaboration tasks

**How they load:** Skills use *progressive disclosure*. At the start of a session Claude reads only each skill's name and description (~100 tokens). The full instructions, scripts, and reference files load only when a task actually matches — so a skill can bundle extensive documentation without costing context until it is needed.

Official Skills are created by Anthropic and auto-invoked when relevant. You can also install or build custom skills to match your own workflow. Skills work identically across Claude.ai, Claude Code, and the Claude API.

---
## 📄 Document Skills
*6 skills*

| Name | Description | Link |
|------|-------------|------|
| **docx** | Create and edit Microsoft Word documents with formatting, comments, and tracked changes | [Source](https://github.com/anthropics/skills/tree/main/skills/docx) |
| **pdf** | Extract content from PDFs, split/merge documents, or create new ones | [Source](https://github.com/anthropics/skills/tree/main/skills/pdf) |
| **pptx** | Generate and edit PowerPoint presentations | [Source](https://github.com/anthropics/skills/tree/main/skills/pptx) |
| **xlsx** | Manipulate Excel files, formulas, tables, and charts | [Source](https://github.com/anthropics/skills/tree/main/skills/xlsx) |
| **revealjs-skill** | Generate polished, professional presentations using the Reveal.js HTML framework | [Source](https://github.com/ryanbbrown/revealjs-skill/tree/main) |
| **Markdown to EPUB Converter** | Convert markdown documents and chat summaries into professional EPUB ebooks (and parse/analyze existing EPUBs) *(updated 2025)* | [Source](https://github.com/smerchek/claude-epub-skill) |

---
## 🎨 Creative & Design
*6 skills*

| Name | Description | Link |
|------|-------------|------|
| **algorithmic-art** | Create generative art using p5.js | [Source](https://github.com/anthropics/skills/tree/main/skills/algorithmic-art) |
| **canvas-design** | Render layout-based visual designs in PNG/PDF using design principles | [Source](https://github.com/anthropics/skills/tree/main/skills/canvas-design) |
| **slack-gif-creator** | Generate Slack-optimized animated GIFs | [Source](https://github.com/anthropics/skills/tree/main/skills/slack-gif-creator) |
| **brand-guidelines** | Apply company branding (colors, typography) to outputs | [Source](https://github.com/anthropics/skills/tree/main/skills/brand-guidelines) |
| **theme-factory** | Create and apply visual themes for documents, slides, and artifacts | [Source](https://github.com/anthropics/skills/tree/main/skills/theme-factory) |
| **nano-banana-image-generation** | Create images using Nano Banana Pro *(updated 2025)* | [Source](https://github.com/livelabs-ventures/nano-skills/tree/main/skills/nano-image-generator) |

---
## 💻 Development & Code Tools
*16 skills*

| Name | Description | Link |
|------|-------------|------|
| **web-artifacts-builder** | Create elaborate, multi-component claude.ai HTML artifacts with React, Tailwind CSS, and shadcn/ui | [Source](https://github.com/anthropics/skills/tree/main/skills/web-artifacts-builder) |
| **MCP Server / Builder** | Build high-quality, Claude-compatible MCP servers to integrate APIs with LLMs | [Source](https://github.com/anthropics/skills/tree/main/skills/mcp-builder) |
| **Changelog Generator** | Create changelogs from commit history | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/changelog-generator) |
| **using-git-worktrees** | Manage feature branches safely in isolated Git worktrees | [Source](https://github.com/obra/superpowers/tree/main/skills/using-git-worktrees) |
| **test-driven-development** | Write tests before implementation to drive development | [Source](https://github.com/obra/superpowers/tree/main/skills/test-driven-development) |
| **subagent-driven-development** | Use multiple Claude subagents to coordinate complex implementations | [Source](https://github.com/obra/superpowers/tree/main/skills/subagent-driven-development) |
| **executing-plans** | Execute structured plans with checkpoints and verification steps | [Source](https://github.com/obra/superpowers/tree/main/skills/executing-plans) |
| **finishing-a-development-branch** | Complete development branches with testing and review flow | [Source](https://github.com/obra/superpowers/tree/main/skills/finishing-a-development-branch) |
| **preserving-productive-tensions** | Manage architectural decisions by preserving competing viewpoints ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/architecture/preserving-productive-tensions) |
| **feature-planning** | Break down feature requests into detailed, implementable plans | [Source](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/feature-planning) |
| **pypict-claude-skill** | Design comprehensive test cases using PICT for optimized test suites | [Source](https://github.com/omkamal/pypict-claude-skill) |
| **aws-skills** | AWS development with CDK best practices, cost optimization, and serverless/event-driven patterns | [Source](https://github.com/zxkane/aws-skills) |
| **AWS CDK Plugin** | AWS CDK development with an integrated MCP server for Infrastructure as Code | [Source](https://github.com/zxkane/aws-skills/tree/main/plugins/aws-iac) |
| **claude-starter** | Production-ready Claude Code configuration template with 40 auto-activating skills and TOON format support | [Source](https://github.com/raintree-technology/claude-starter) |
| **move-code-quality-skill** | Analyze Move language packages against the official Move Book Code Quality Checklist *(updated 2025)* | [Source](https://github.com/1NickPappas/move-code-quality-skill) |
| **claude-code-terminal-title** | Give each Claude Code terminal window a dynamic title describing the current work | [Source](https://github.com/bluzername/claude-code-terminal-title) |

---
## 📊 Data & Analysis
*3 skills*

| Name | Description | Link |
|------|-------------|------|
| **csv-data-summarizer** | Generate statistics and charts from CSVs *(updated 2025)* | [Source](https://github.com/coffeefuelbump/csv-data-summarizer-claude-skill) |
| **root-cause-tracing** | Trace and diagnose the source of data or logic errors | [Source](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/root-cause-tracing.md) |
| **postgres** | Execute safe read-only SQL queries against PostgreSQL databases with multi-connection support | [Source](https://github.com/sanjay3290/ai-skills/tree/main/skills/postgres) |

---
## 🔬 Scientific & Research Tools
*6 skills*

| Name | Description | Link |
|------|-------------|------|
| **claude-scientific-skills** | 125+ scientific skills for bioinformatics, cheminformatics, clinical research, and machine learning | [Source](https://github.com/K-Dense-AI/scientific-agent-skills) |
| **materials-simulation-skills** | Agent skills for computational materials science: numerical stability, time-stepping, linear solvers, and simulation validation | [Source](https://github.com/HeshamFS/materials-simulation-skills) |
| **Single-cell analysis (Scanpy)** | Analyze single-cell RNA-seq data with Scanpy and AnnData | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Molecular manipulation (RDKit)** | Handle molecular structures and predictions with RDKit | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Deep learning (PyTorch Lightning)** | Build and train ML models with PyTorch Lightning | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Clinical databases (ClinVar)** | Access and analyze clinical variant data from ClinVar | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |

---
## 📝 Writing & Research
*7 skills*

| Name | Description | Link |
|------|-------------|------|
| **article-extractor** | Extract full content from web articles | [Source](https://github.com/michalparkola/tapestry-skills/tree/main/article-extractor) |
| **Content Research Writer** | Research and write high-quality content with feedback, sources, and citations | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/content-research-writer) |
| **internal-comms** | Draft formal internal communications and reports using company formats | [Source](https://github.com/anthropics/skills/tree/main/skills/internal-comms) |
| **writing-plans** | Create structured written plans with clear milestones | [Source](https://github.com/obra/superpowers/tree/main/skills/writing-plans) |
| **writing-skills** | Enhance instructional and technical writing quality | [Source](https://github.com/obra/superpowers/tree/main/skills/writing-skills) |
| **brainstorming** | Facilitate creative idea generation sessions | [Source](https://github.com/obra/superpowers/tree/main/skills/brainstorming) |
| **family-history-research** | Plan family history and genealogy research projects | [Source](https://github.com/emaynard/claude-family-history-research-skill) |

---
## 📚 Learning & Knowledge
*8 skills*

| Name | Description | Link |
|------|-------------|------|
| **ship-learn-next** | Recommend next steps based on feedback loops | [Source](https://github.com/michalparkola/tapestry-skills/tree/main/ship-learn-next) |
| **using-superpowers** | Learn and apply best practices for Superpowers workflows | [Source](https://github.com/obra/superpowers/tree/main/skills/using-superpowers) |
| **collision-zone-thinking** | Combine unrelated concepts to find new creative or problem-solving connections ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/problem-solving/collision-zone-thinking) |
| **inversion-exercise** | Flip assumptions to uncover hidden insights and constraints ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/problem-solving/inversion-exercise) |
| **meta-pattern-recognition** | Identify patterns across domains to uncover universal principles ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/problem-solving/meta-pattern-recognition) |
| **scale-game** | Stress-test ideas at extreme scales to expose hidden weaknesses or truths ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/problem-solving/scale-game) |
| **simplification-cascades** | Reduce complexity by discovering insights that simplify multiple elements at once ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/problem-solving/simplification-cascades) |
| **tracing-knowledge-lineages** | Track how ideas evolve across iterations and influences ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/research/tracing-knowledge-lineages) |

---
## 🎥 Media & Content
*4 skills*

| Name | Description | Link |
|------|-------------|------|
| **youtube-transcript** | Summarize YouTube transcripts | [Source](https://github.com/michalparkola/tapestry-skills/tree/main/youtube-transcript) |
| **Video Downloader** | Download YouTube videos for use in Claude | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/video-downloader) |
| **Image Enhancer** | Improve resolution and clarity of screenshots and images | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/image-enhancer) |
| **imagen** | Generate images with Google Gemini's image API for UI mockups, icons, and visual assets | [Source](https://github.com/sanjay3290/ai-skills/tree/main/skills/imagen) |

---
## 🤝 Collaboration & Project Management
*11 skills*

| Name | Description | Link |
|------|-------------|------|
| **Meeting Insights Analyzer** | Analyze meeting transcripts for dynamics, communication patterns, and behavior | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/meeting-insights-analyzer) |
| **Notion Integration Skills** | Official Notion connectors for Claude | [Source](https://notiondevs.notion.site/Notion-Skills-for-Claude-28da4445d27180c7af1df7d8615723d0) |
| **receiving-code-review** | Process and apply code review feedback | [Source](https://github.com/obra/superpowers/tree/main/skills/receiving-code-review) |
| **requesting-code-review** | Request and manage structured code reviews | [Source](https://github.com/obra/superpowers/tree/main/skills/requesting-code-review) |
| **dispatching-parallel-agents** | Coordinate multiple Claude subagents on shared tasks | [Source](https://github.com/obra/superpowers/tree/main/skills/dispatching-parallel-agents) |
| **remembering-conversations** | Recall facts, insights, and context from past Claude Code sessions ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/collaboration/remembering-conversations) |
| **git-pushing** | Automate git operations and repository interactions | [Source](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/git-pushing) |
| **linear-claude-skill** | Manage Linear issues, projects, and teams with MCP tools and GraphQL fallbacks | [Source](https://github.com/wrsmith108/linear-claude-skill) |
| **linear-cli-skill** | Teach Claude to use linear-CLI as an alternative to the Linear MCP *(updated 2025)* | [Source](https://github.com/Valian/linear-cli-skill) |
| **review-implementing** | Evaluate code implementation plans and align them with specs | [Source](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/review-implementing) |
| **test-fixing** | Detect failing tests and propose patches or fixes | [Source](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/test-fixing) |

---
## 🔐 Security & Testing
*9 skills*

| Name | Description | Link |
|------|-------------|------|
| **webapp-testing** | UI test automation using Playwright to verify local web apps | [Source](https://github.com/anthropics/skills/tree/main/skills/webapp-testing) |
| **ffuf_claude_skill** | Fuzz test web apps with FFUF + Claude *(updated 2025)* | [Source](https://github.com/jthack/ffuf_claude_skill) |
| **defense-in-depth** | Implement multi-layered testing and security best practices | [Source](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/defense-in-depth.md) |
| **systematic-debugging** | Structured debugging with hypothesis testing and validation | [Source](https://github.com/obra/superpowers/tree/main/skills/systematic-debugging) |
| **testing-anti-patterns** | Identify and prevent testing anti-patterns | [Source](https://github.com/obra/superpowers/blob/main/skills/test-driven-development/testing-anti-patterns.md) |
| **testing-skills-with-subagents** | Verify new skills using subagents and test cycles | [Source](https://github.com/obra/superpowers/blob/main/skills/writing-skills/testing-skills-with-subagents.md) |
| **verification-before-completion** | Run verification checks before closing tasks | [Source](https://github.com/obra/superpowers/tree/main/skills/verification-before-completion) |
| **condition-based-waiting** | Use logical conditions to control test flow timing | [Source](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/condition-based-waiting.md) |
| **varlock-claude-skill** | Secure environment-variable management so secrets never appear in sessions, terminals, logs, or git commits | [Source](https://github.com/wrsmith108/varlock-claude-skill) |

---
## ⚙️ Utility & Automation
*3 skills*

| Name | Description | Link |
|------|-------------|------|
| **skill-creator** | Build your own skill interactively | [Source](https://github.com/anthropics/skills/tree/main/skills/skill-creator) |
| **gardening-skills-wiki** | Maintain a skills wiki, ensuring naming consistency and metadata quality ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/meta/gardening-skills-wiki) |
| **pulling-updates-from-skills-repository** | Sync and pull the latest skill updates from repositories ⚠️ *(archived)* | [Source](https://github.com/obra/superpowers-skills/tree/main/skills/meta/pulling-updates-from-skills-repository) |

---
## 🤖 AI & Machine Learning
*6 skills*

| Name | Description | Link |
|------|-------------|------|
| **Deep learning (Transformers)** | Use Hugging Face Transformers for NLP tasks | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Graph ML (Torch Geometric)** | Build graph neural networks with PyTorch Geometric | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Bayesian methods (PyMC)** | Perform Bayesian inference and modeling | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Reinforcement learning (Stable Baselines3)** | Train RL agents with Stable Baselines3 | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **Model interpretability (SHAP)** | Explain ML model predictions with SHAP | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |
| **AWS Agentic AI Plugin** | Deploy and manage AI agents with AWS Bedrock | [Source](https://github.com/zxkane/aws-skills/tree/main/plugins/aws-agentic-ai) |

---
## ☁️ Cloud & Infrastructure
*3 skills*

| Name | Description | Link |
|------|-------------|------|
| **AWS Cost & Operations Plugin** | Cost optimization, monitoring, and operational excellence with MCP servers | [Source](https://github.com/zxkane/aws-skills/tree/main/plugins/aws-cost-ops) |
| **AWS Serverless & Event-Driven Architecture Plugin** | Serverless patterns based on the Well-Architected Framework | [Source](https://github.com/zxkane/aws-skills/tree/main/plugins/serverless-eda) |
| **Cloud compute (Modal)** | Integrate with Modal for cloud-based compute | [Source](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/docs/skills.md) |

---
## 💼 Business & Marketing
*3 skills*

| Name | Description | Link |
|------|-------------|------|
| **Competitive Ads Extractor** | Extract and analyze competitors' ads | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/competitive-ads-extractor) |
| **Domain Name Brainstormer** | Generate domain ideas and check availability | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/domain-name-brainstormer) |
| **Lead Research Assistant** | Identify and qualify leads with outreach strategies | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/lead-research-assistant) |
| **mailtrap-skills** | Agent skills for Mailtrap: email sending via API/SMTP, domain setup, and contacts management | [Source](https://github.com/mailtrap/mailtrap-skills) |

---
## 📈 Productivity & Organization
*3 skills*

| Name | Description | Link |
|------|-------------|------|
| **file-organizer** | Intelligently organize files and folders by context; clean up structures and rename documents | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/file-organizer) |
| **invoice-organizer** | Parse, categorize, and organize invoices for tax preparation | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/invoice-organizer) |
| **raffle-winner-picker** | Randomly select winners from lists or sheets using secure randomness | [Source](https://github.com/ComposioHQ/awesome-claude-skills/tree/master/raffle-winner-picker) |

---
## Getting Started
To use a skill:
1. Clone the [Anthropic Claude Skills](https://github.com/anthropics/skills) repo (or the specific repo linked in the table).
2. Enable Code Execution and Skill loading in Claude.
3. Upload the skill folder (or link to a Git repo containing a `SKILL.md`).
4. Ask Claude to activate or use the skill!

For building your own, start with **skill-creator** above.

---
## Contributing
Have a skill to add?
Open a pull request or submit your repo link in an issue with:
- Name of the skill
- Short description
- Category
- Link to the source

Please avoid duplicates — check whether the skill is already listed under another category first.

---
## License
This repository only lists and links to third-party skills, each published under its own license.
Refer to each linked repository for its specific license terms.
