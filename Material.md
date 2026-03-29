## AI Agents Core Workflow Loop

AI agents operate through a repeating **Observe-Think-Act** loop that enables autonomous task completion, independent of specific platforms.

- **Observe**: Agent ingests all available context, including files, previous tool calls, system prompts (e.g., `agents.md`, `claude.md`), research data, multimodal inputs (vision, audio), and conversation history. This builds environmental awareness before decision-making.
- **Think (Reason)**: Agent analyzes context against the high-level user goal to plan next steps. Modern platforms provide dedicated reasoning views for interpretability, allowing real-time steering and accountability.
- **Act**: Agent executes via tools (e.g., file edits, CLI commands, web searches, APIs). Results feed back into Observe, expanding context iteratively.

Loops typically run 3-4 times until **Definition of Done** (DoD)—explicit constraints signaling completion (e.g., "compile 10+ sources")—triggers a final formatted output. Poor DoD leads to underwhelming results; always define it explicitly. Context grows per loop (stacking tokens), but quality degrades with excessive length, necessitating management techniques.

## Demo: Multi-Agent Parallelization for Economic Value

Agents excel at **parallelization**, spawning multiple instances simultaneously to outperform single agents despite lower per-instance intelligence/speed. Demo: From a leads list (names, websites, LinkedIn), 5 Claude agents via Cloud Code open independent Chrome browsers, navigate sites, research via shared chat room, fill contact forms with personalized outreach—tasks that would take one agent hours.

Key insight: Agents are faster than humans at one-shots but less accurate; parallel runs test multiple approaches rapidly for superior net results. This scales economically (e.g., 1000 form fills in 40 minutes vs. 30 hours serially).

## Major AI Agent Platforms Setup

Three platforms dominate: **Codeex** (OpenAI), **Claude Code** (Anthropic), **Anti-Gravity** (Google). All enable agentic coding via desktop apps with similar UX (chat, thinking tabs, folder workspaces).

| Platform     | Owner     | Signup/Install                                                                  | Cost                                     | Example Task: Simple Portfolio Site                         |
| ------------ | --------- | ------------------------------------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------- |
| Codeex       | OpenAI    | chatgpt.openai.com → Download app (Mac/Win) → Drag to Applications → New folder | Free tier; API billed                    | Builds sleek site with design skills; auto-opens in browser |
| Claude Code  | Anthropic | claude.ai → Pro ($20/mo) → Download app → New project → Bypass permissions      | Paid Pro required (100-200x ROI claimed) | Minimalist site; thinking tab shows tool calls              |
| Anti-Gravity | Google    | gemini.google.com → Download (check chip: M/Intel)                              | Free (Gmail login)                       | Sexiest design (isomorphic glass); fast output              |

All support skills, MCP (Model Context Protocol) for tool integration, and similar prompting. Skip setup if familiar with one.

## Platform Strengths and Tradeoffs

Models are near-parity in intelligence (minor 1-5% edges); choose by task.

| Model/Platform        | Best At                                                  | Weaknesses                                     | Notes                      |
| --------------------- | -------------------------------------------------------- | ---------------------------------------------- | -------------------------- |
| Claude (Claude Code)  | Interpretable reasoning (steerable plans), orchestration | Slower (use fast mode), weaker frontend/design | Partner-like; consistent   |
| Gemini (Anti-Gravity) | Frontend/design, multimodal (video), fast output         | Least interpretable, inconsistent              | Upscale aesthetics         |
| GPT (Codeex)          | Backend/math, test-driven dev, ecosystem                 | Less interpretable/orchestrable                | Autonomous "missile" style |

**Multi-Agent MCP Orchestration** routes subtasks (e.g., Claude orchestrates: Gemini UI, Codeex backend/testing). Use API keys; boosts quality at frontier via specialization.

## Self-Modifying Agent Instructions via.md Files

Platforms prepend workspace files (`agents.md`/Codeex, `claude.md`/Claude Code, `gemini.md`/Anti-Gravity) as persistent system prompts. Build **self-modifying rules**: Meta-prompt instructs agent to append "learned rules" (e.g., "Never: dark mode") on user corrections/bugs/preferences.

- **Format**: Numbered imperatives ("1. Style: Never dark mode—user preference") under "Learned Rules" section.
- **Hierarchy**: Global `.md` (user-wide) → Local project `.md` → Inline prompt.
- **Benefit**: Errors drop over sessions as rules accumulate (high initial errors → near-zero). Demo: Agent builds site, user says "no dark mode" → Appends rule → Future sites comply.

## Agent Skills for Repeatable Workflows

**Skills** standardize vague LLM outputs into deterministic paths via YAML-frontmatter files (name, description, tools). Loaded selectively (only YAML until invoked) to save tokens. Examples: `algorithmic-art.md` generates consistent art via library steps. Copy-paste across platforms for validated SOPs.

## Advanced Prompting: Video-to-Action Pipelines

Agents learn from videos (human-like medium) via **Gemini API** (native video support): Claude receives YouTube URL → Delegates to Gemini → Extracts hyper-detailed steps (1 frame/sec, UI colors, sequences) → Claude executes (e.g., replicates n8n scraper flow via browser control). Demo: 21-min video → Step-by-step MD → Autonomous browser build.

## Stochastic Multi-Agent Consensus

Exploits LLM **stochasticity** (output variance on repeat prompts): Spawn n sub-agents (e.g., 10) with framing variations → Parallel ideation → Parent aggregates (mode/median/consensus/outliers).

- Traverses broader "search space" (all possible ideas) faster than serial queries.
- Parallel: 3x3-idea runs = 9 ideas in one run's time vs. 3x time serially.
- Demo: TikTok growth ideas → Consensus (e.g., hooks, fresh accounts), outliers (spark ads).

## Agent Chat Rooms for Debate

Spawn agents with personalities (e.g., Systems Thinker, Contrarian) in shared `chat.json` → Round-robin debate → Higher-quality nuanced outputs via challenge/assumption-testing. Demo: TikTok analysis → Sharper insights (e.g., "hook mismatch") than parallel consensus.

## Sub-Agent Verification Loops

Mitigates builder bias (sunk-cost blindness): Implementer → Fresh-context Reviewer (checks correctness/edges/simplification/security) → Resolver (fixes). Serial but objective; like peer review. Demo: Codebase review finds 22 issues missed by original agent.

## Prompt Contracts and Reverse Prompting

**Prompt Contracts**: Force DoD clarification pre-execution (goals/constraints/format/failures) via skill; user approves. Avoids vague tasks (e.g., "beautiful site"). Demo: Site contract specifies animations, <500 lines, no Bootstrap.

**Reverse Prompting**: Agent asks 5 clarifying questions (assumptions/edges/tastes) → Builds contract. Boosts one-shot accuracy. Demo: "Beautiful site" → Questions on goal/vibe/copy → Precise Linear-white build.

## Multi-Agent Chrome MCP Manager

Scales browser tasks: Orchestrator (Claude) spawns n agents → Each gets Chrome DevTools MCP server/workspace → Parallel actions (e.g., 4 sites for rentals: Craigslist/Padmapper/etc.). Shared chat for coordination; 10x speed vs. linear. Demo: Vancouver rentals (1-bed, AC, <2.5K) → Filtered list in minutes.

## Context Window Management (Iceberg Technique)

Context (200K-1M tokens ≈140K-700K words) degrades quality/bills with length; compaction auto-summarizes (drops tool outputs).

- **Above Water (Always Loaded, ~20-30%)**: `claude.md`/memory (rules/preferences), active files/task context.
- **Below (On-Demand Tools)**: Read/GP/Glob (selective file/code), web fetch, bash/history. Narrow progressively.

| Component | Naive (Full Load) | Strategic (Iceberg)       |
| --------- | ----------------- | ------------------------- |
| Codebase  | All files         | GP/Glob relevant snippets |
| Skills    | Full content      | YAML frontmatter only     |
| Tools     | Full outputs      | Summaries                 |

Visualize via `/context` (Claude: squares=2K tokens each). Start lean to delay degradation.

## Model Optimization and Token Pricing

**60/30/10 Rule**: Router (10% top-tier, e.g., Opus) delegates: 60% cheap/dumb (Haiku/Flash: classification/scraping), 30% mid (Sonnet: research/outreach). Saves ~60% cost (e.g., $120 vs. $450/mo for 1K leads).

| Tier | % Tokens | Models           | Use Case          | Price/M Tokens |
| ---- | -------- | ---------------- | ----------------- | -------------- |
| High | 10%      | Opus 4.6/GPT-5.4 | Routing/reasoning | $5-15          |
| Mid  | 30%      | Sonnet/GPT-4     | Research/enrich   | $2-3           |
| Low  | 60%      | Haiku/Flash      | Scraping/classify | $0.10-1        |

Batch APIs (24h turnaround) cut costs further via off-peak. Prioritize architecture/tools over raw intelligence.
