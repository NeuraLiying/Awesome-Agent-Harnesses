# Awesome Agent Harnesses [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated, multiply-verified survey of **agent harness** research and engineering — the right level of abstraction for understanding the current frontier of LLM agents.

**Total: 207 papers · 66 production harnesses / essays / talks · last updated 2026-10-06**

## What is an agent harness?

The harness is the layer *around* the model that turns it into an agent — the agent loop plus tools, memory, context, runtime, and safety. A few authoritative definitions:

> "You can also define an agent as: **agent = model + harness**. The harness is the scaffolding around the model that connects it to the real world."

> — LangChain, [*How to Build a Custom Agent Harness*](https://www.langchain.com/blog/how-to-build-a-custom-agent-harness) (2026-06-03)


> "This post focuses on the **Codex harness**, which provides the **core agent loop and execution logic** that underlies all Codex experiences and is surfaced through the Codex CLI."

> — OpenAI, [*Unrolling the Codex agent loop*](https://openai.com/index/unrolling-the-codex-agent-loop/) (2026-05-27)


> "Agents can handle sophisticated tasks, but their implementation is often straightforward. They are typically just **LLMs using tools based on environmental feedback in a loop**."

> — Anthropic, [*Building Effective Agents*](https://www.anthropic.com/research/building-effective-agents) (2024-12)


The agent loop is therefore a *component* of the harness — its core execution mechanism — not a peer of it. This list is organised by harness component.

### Anatomy of a harness — how this list is mapped

| Harness component | Where |
|---|---|
| Production harnesses — Claude Code, Codex, Cursor, … *are* harnesses | [§1](#1-production-harnesses-sdks--frameworks) |
| Influential essays, blogs & talks | [§2](#2-influential-essays-blogs--talks) |
| The agent loop (core execution + control flow) | [§4](#4-foundations-of-the-agent-loop-20222023) · [§7](#7-planning-search-self-improvement-loops) |
| Tools & function calling | [§5](#5-tool-use--function-calling) |
| The harness as a research object (scaffold, runtime, agent-computer interface) | [§6](#6-the-agent-harness--scaffold) |
| Memory & context management | [§8](#8-memory-augmented-agents) |
| Multi-agent orchestration | [§9](#9-multi-agent-systems) |
| Domain harnesses (code/SWE, web/GUI) | [§10](#10-code--swe-agents) · [§11](#11-web-gui--computer-use-agents) |
| Evaluation & stress-testing | [§12](#12-benchmarks--evaluation) |
| Training the loop (reasoning models, test-time scaling, agent RL) | [§13](#13-reasoning-models--test-time-scaling-for-agents) |

## Table of Contents

- [1. Production Harnesses, SDKs & Frameworks](#1-production-harnesses-sdks--frameworks)
- [2. Influential Essays, Blogs & Talks](#2-influential-essays-blogs--talks)
- [3. Surveys & Position Papers](#3-surveys-position-papers)
- [4. Foundations of the Agent Loop (2022–2023)](#4-foundations-of-the-agent-loop-20222023)
- [5. Tool Use & Function Calling](#5-tool-use-function-calling)
- [6. The Agent Harness & Scaffold](#6-the-agent-harness-scaffold)
- [7. Planning, Search & Self-Improvement Loops](#7-planning-search-self-improvement-loops)
- [8. Memory-Augmented Agents](#8-memory-augmented-agents)
- [9. Multi-Agent Systems](#9-multi-agent-systems)
- [10. Code & SWE Agents](#10-code-swe-agents)
- [11. Web, GUI & Computer-Use Agents](#11-web-gui-computer-use-agents)
- [12. Benchmarks & Evaluation](#12-benchmarks-evaluation)
- [13. Reasoning Models & Test-Time Scaling for Agents](#13-reasoning-models-test-time-scaling-for-agents)
- [Related Resources](#related-resources)

---

## 1. Production Harnesses, SDKs & Frameworks (23)

*These shipped products ARE agent harnesses — the artifact the rest of this list studies. Ordered by year.*

| Name | URL | Year | Org | What it is |
|------|-----|------|-----|------------|
| continuedev/continue | [repo](https://github.com/continuedev/continue) | 2023 | Continue | Continue — open-source AI coding agent as a VS Code / JetBrains extension, fully local-model friendly. ~34.6k stars. Lon |
| microsoft/autogen | [repo](https://github.com/microsoft/autogen) | 2023 | Microsoft Research | AutoGen — programming framework for building multi-agent conversational systems. ~59.4k stars. Originated the conversati |
| paul-gauthier/aider | [repo](https://github.com/Aider-AI/aider) | 2023 | Paul Gauthier | Aider — AI pair programming in the terminal, git-aware by design. ~47k stars (canonical org: Aider-AI/aider). Predates a |
| OpenHands/OpenHands | [repo](https://github.com/All-Hands-AI/OpenHands) | 2024 | All-Hands-AI | OpenHands (formerly OpenDevin) — open-source platform for autonomous software development with browser, terminal, and co |
| SWE-agent/SWE-agent | [repo](https://github.com/SWE-agent/SWE-agent) | 2024 | Princeton NLP / SWE-agent | SWE-agent — agent-computer-interface (ACI) framework that takes a GitHub issue and autonomously fixes it with any LM. ~1 |
| aaif-goose/goose | [repo](https://github.com/aaif-goose/goose) | 2024 | Block (fka Square) | Goose — Block's open-source, extensible AI agent that goes beyond code suggestions to install, execute, edit, and test c |
| cline/cline | [repo](https://github.com/cline/cline) | 2024 | Cline | Cline (formerly Claude Dev) — autonomous coding agent shipped as VS Code extension, SDK, and CLI. ~64k stars. The most-s |
| crewAIInc/crewAI | [repo](https://github.com/crewAIInc/crewAI) | 2024 | CrewAI | CrewAI — framework for orchestrating role-playing, collaborative autonomous AI agents (crew, task, tool). ~54.8k stars.  |
| langchain-ai/langgraph | [repo](https://github.com/langchain-ai/langgraph) | 2024 | LangChain | LangGraph — library for building stateful, resilient multi-actor agent workflows as graphs (nodes, edges, checkpointing, |
| anthropics/claude-code | [repo](https://github.com/anthropics/claude-code) | 2025 | Anthropic | Claude Code — Anthropic's official agentic terminal coding tool. Understands the codebase, runs tools, edits files, driv |
| nanochat: The best ChatGPT that $100 can buy | [repo](https://github.com/karpathy/nanochat) | 2025 | Andrej Karpathy | Karpathy's self-described 'simplest experimental harness for training LLMs' — a single, minimal, hackable codebase cover |
| openai/codex — Lightweight coding agent that runs in your terminal | [repo](https://github.com/openai/codex) | 2025 | OpenAI | Codex CLI, OpenAI's terminal-based coding agent: runs locally, integrates with VS Code/Cursor, and exposes the agent loo |
| openai/openai-agents-python (GitHub repository) | [repo](https://github.com/openai/openai-agents-python) | 2025 | OpenAI | Source repository for the OpenAI Agents SDK: a lightweight, multi-provider framework for building agentic workflows in P |
| wanshuiyin/Auto-claude-code-research-in-sleep | [repo](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) | 2025 | wanshuiyin | ARIS (Auto-Research-In-Sleep) — lightweight Markdown-only skill suite turning Claude Code into an autonomous ML-research |
| sandbaseai/sandbase-harness | [repo](https://github.com/sandbaseai/sandbase-harness) | 2026 | SandBase | Local-first agent runtime with sandboxed sessions, MCP tools, memory, credentials, audit, and replay. |
| AxisAgentic — extensible runtime & trajectory-collection framework for long-horizon agents | [repo](https://github.com/XYZ-AI-Lab/AxisAgentic) | 2026 | XYZ AI Lab (xyz-lab.ai) | Extensible runtime for long-horizon agents that executes multi-turn tool orchestration with context budgeting/. ~1120 stars.
| dots — OpenAI's always-on personal agent (cloud workspaces, proactive research loop) | [site](https://openai.com/index/introducing-dots/) | 2026 | OpenAI | OpenAI's launch of Dots (Dev Day, 2026-09-29): always-on personal agents where each dot runs continuously in its own protected cloud workspace.
| FrontierAgent — Apodex agent runtime, TUI & evaluation suite | [repo](https://github.com/ApodexAI/FrontierAgent) | 2026 | ApodexAI (Apodex AI, apodex.ai) | Open-source agent runtime, terminal TUI, and evaluation suite released alongside Apodex 1.1: a stateful ReAct. ~5127 stars.
| fx — tiny, open, embeddable, native coding agent in Zig | [repo](https://github.com/vercel-labs/fx) | 2026 | Vercel (vercel-labs) | Tiny open-source Apache-2.0 coding-agent CLI written in Zig: a model-agnostic native binary with a Unix-shell-. ~3309 stars.
| Graft — open-source context layer for coding agents | [repo](https://github.com/trailhq/Graft) | 2026 | Trail (trailhq; ex-NanoNets) | Open-source context layer for coding agents: builds a per-repo knowledge graph (tree-sitter symbol graph + LLM. ~9615 stars.
| grok-build — xAI's terminal coding agent harness & TUI | [repo](https://github.com/xai-org/grok-build) | 2026 | xAI | xAI/SpaceXAI's production terminal coding-agent harness: fullscreen mouse-interactive Rust TUI with a dedicate. ~27231 stars.
| qm — multiplayer agent harness for work (Slack + web) | [repo](https://github.com/yc-software/qm) | 2026 | Y Combinator (yc-software) | Open-source multiplayer agent harness for organizations: a headless core runs pluggable agent loops (Pi, OpenC. ~15348 stars.
| ZCode — Z.ai's coding agent harness (desktop, web & terminal) | [repo](https://github.com/zai-org/ZCode) | 2026 | Z.ai (Zhipu AI) — official org "zai-org" (verified via GitHub API: hosts ChatGLM, GLM-4/5, AutoGLM, CogVideoX, CodeGeeX) | Open-source monorepo of Z.ai's production coding agent harness: Electron desktop, web, and terminal (TUI/CLI). ~7453 stars.

## 2. Influential Essays, Blogs & Talks (43)

*High-impact, often more influential than an average paper. Long-form only.*

| Title | Author / Org | Type | Year | Link |
|-------|--------------|------|------|------|
| Software 2.0 | Andrej Karpathy | blog | 2017 | [link](https://karpathy.medium.com/software-2-0-a64152b37c35) |
| Building Generally Capable AI Agents with MineDojo | Jim Fan (NVIDIA) — NVIDIA Developer Blog | blog | 2022 | [link](https://developer.nvidia.com/blog/building-generally-capable-ai-agents-with-minedojo/) |
| LLM OS. Bear with me I'm still cooking. (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2023 | [link](https://x.com/karpathy/status/1723140519554105733) |
| LLM Powered Autonomous Agents | Lilian Weng (OpenAI) — Lil'Log | blog | 2023 | [link](https://lilianweng.github.io/posts/2023-06-23-agent/) |
| LLMs not as a chatbot, but the kernel process of a new Operating System (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2023 | [link](https://x.com/karpathy/status/1707437820045062561) |
| Making Large Language Models Work for You (WordCamp US talk) | Simon Willison | talk | 2023 | [link](https://simonwillison.net/2023/Aug/27/wordcamp-llms/) |
| The Anatomy of Autonomy: Why Agents are the next AI Killer App after ChatGPT | swyx — Latent Space | blog | 2023 | [link](https://www.latent.space/p/agents) |
| The Rise of the AI Engineer | swyx — Latent Space | blog | 2023 | [link](https://www.latent.space/p/ai-engineer) |
| [1hr Talk] Intro to Large Language Models | Andrej Karpathy | talk | 2023 | [link](https://www.youtube.com/watch?v=zjkBMFhNj_g) |
| Agentic Design Patterns (Part 1: How Agents Can Improve LLM Performance; Part 2: Reflection; Part 3: Tool Use) | Andrew Ng — DeepLearning.AI, The Batch | blog | 2024 | [link](https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance) |
| Building Effective Agents | Anthropic | blog | 2024 | [link](https://www.anthropic.com/research/building-effective-agents) |
| Introducing computer use: a new Claude 3.5 Sonnet (and computer-use API) | Anthropic | blog | 2024 | [link](https://www.anthropic.com/news/3-5-models-and-computer-use) |
| Jagged Intelligence (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2024 | [link](https://x.com/karpathy/status/1816531576228053133) |
| Language Agents: From Reasoning to Acting (interview) | Shunyu Yao — Latent Space (swyx / Alessio) | podcast | 2024 | [link](https://www.latent.space/p/shunyu) |
| OpenAI o1 System Card | OpenAI | doc | 2024 | [link](https://openai.com/index/openai-o1-system-card/) |
| The Second Half | Shunyu Yao (Princeton / OpenAI) | blog | 2024 | [link](https://ysymyth.github.io/The-Second-Half/) |
| Writing effective tools for AI agents — using AI agents | Anthropic | blog | 2024 | [link](https://www.anthropic.com/engineering/writing-tools-for-agents) |
| A Practical Guide to Building Agents (PDF) | OpenAI | doc | 2025 | [link](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) |
| A Practical Guide to Building Agents (landing page) | OpenAI | doc | 2025 | [link](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/) |
| Agents are models using tools in a loop | Simon Willison | blog | 2025 | [link](https://simonwillison.net/2025/May/22/tools-in-a-loop/) |
| Building agents with the Claude Agent SDK | Anthropic | blog | 2025 | [link](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) |
| Claude Code: Best practices for agentic coding | Anthropic | blog | 2025 | [link](https://code.claude.com/docs/en/best-practices) |
| Computer-Using Agent | OpenAI | blog | 2025 | [link](https://openai.com/index/computer-using-agent/) |
| Demystifying evals for AI agents | Anthropic | blog | 2025 | [link](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) |
| Effective Context Engineering for AI Agents | Anthropic (Applied AI team) | blog | 2025 | [link](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) |
| How we built our multi-agent research system | Anthropic | blog | 2025 | [link](https://www.anthropic.com/engineering/multi-agent-research-system) |
| I think "agent" may finally have a widely enough agreed upon definition | Simon Willison | blog | 2025 | [link](https://simonwillison.net/2025/Sep/18/agents/) |
| Introducing Operator | OpenAI | blog | 2025 | [link](https://openai.com/index/introducing-operator/) |
| Introducing deep research | OpenAI | blog | 2025 | [link](https://openai.com/index/introducing-deep-research/) |
| New tools for building agents (Agents SDK + Responses API announcement) | OpenAI | blog | 2025 | [link](https://openai.com/index/new-tools-for-building-agents/) |
| OpenAI Agents SDK (openai-agents-python) — documentation site | OpenAI | doc | 2025 | [link](https://openai.github.io/openai-agents-python/) |
| OpenAI o3 and o4-mini System Card | OpenAI | doc | 2025 | [link](https://openai.com/index/o3-o4-mini-system-card/) |
| There's a new kind of coding I call "vibe coding" (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2025 | [link](https://x.com/karpathy/status/1886192184808149383) |
| 2026 Agentic Coding Trends Report | Anthropic | doc | 2026 | [link](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf) |
| AI Sessions #7: How Close is "AGI"? | Conspicuous Cognition (Dan Williams, Henry Shevlin) | podcast | 2026 | [link](https://www.conspicuouscognition.com/p/how-close-is-agi) |
| Harness design for long-running application development | Anthropic | blog | 2026 | [link](https://www.anthropic.com/engineering/harness-design-long-running-apps) |
| Agentic test processes, LLM benchmarks, and other notes on agentic coding from Galapagos Island | danluu.com (Dan Luu, personal blog) | blog | 2026 | [link](https://danluu.com/ai-coding/) |
| Claude Code Sends 4.7x More Tokens Than OpenCode Before Reading Your Prompt | Systima (systima.ai) | blog | 2026 | [link](https://systima.ai/blog/claude-code-vs-opencode-token-overhead) |
| Claude Code's Next Era — Thariq Shihipar, Anthropic | Anthropic (Thariq Shihipar, Claude Code) on Latent Space (swyx) | podcast | 2026 | [link](https://www.latent.space/p/thariq) |
| Harness Engineering for Self-Improvement | Lilian Weng (Lil'Log; ex-OpenAI) | blog | 2026 | [link](https://lilianweng.github.io/posts/2026-07-04-harness) |
| HarnessTax: How Much Does the Harness Matter for Coding Agents? | UC Berkeley (Sky Computing Lab) + Arena Intelligence Inc. (LMArena) | study | 2026 | [link](https://harnesstax.github.io) |
| The new rules of context engineering for Claude 5 generation models | Anthropic | blog | 2026 | [link](https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models) |
| Why Software Factories Fail (or: harness engineering is not enough) | HumanLayer (Dex Horthy) | essay | 2026 | [link](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/wsff.md) |

## 3. Surveys & Position Papers (12)

*Authoritative surveys and position papers on LLM agents.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| A Survey on Large Language Model based Autonomous Agents | [2308.11432](https://arxiv.org/abs/2308.11432) | [GitHub](https://github.com/Paitesanshi/LLM-Agent-Survey) | 2023 | Frontiers of Computer Science (2024), vol. 18, art. 186345; arXiv:2308.11432 | agent survey, profiling-memory-planning-action, taxonomy |
| The Rise and Potential of Large Language Model Based Agents: A Survey | [2309.07864](https://arxiv.org/abs/2309.07864) | [GitHub](https://github.com/WooooDyy/LLM-Agent-Paper-List) | 2023 | arXiv (Scientia Sinica Informationis journal version) | survey, profiling-memory-planning-action, taxonomy, agent-architecture |
| A Survey on LLM-based Multi-Agent System: Recent Advances and New Frontiers in Application | [2412.17481](https://arxiv.org/abs/2412.17481) | / | 2024 | arXiv:2412.17481 | multi-agent, LLM-MAS, applications |
| A Survey on the Memory Mechanism of Large Language Model based Agents | [2404.13501](https://arxiv.org/abs/2404.13501) | [GitHub](https://github.com/nuster1128/LLM_Agent_Memory_Survey) | 2024 | arXiv:2404.13501 (later ACM Computing Surveys) | survey, memory taxonomy, read/write/reflect, evaluation |
| Large Language Model based Multi-Agents: A Survey of Progress and Challenges | [2402.01680](https://arxiv.org/abs/2402.01680) | [GitHub](https://github.com/taichengguo/LLM_Multiagents_Survey_Papers) | 2024 | IJCAI 2024 (proc. paper 890); arXiv:2402.01680 | multi-agent, LLM-MAS, survey |
| Tool Learning with Large Language Models: A Survey | [2405.17935](https://arxiv.org/abs/2405.17935) | [GitHub](https://github.com/quchangle1/LLM-Tool-Survey) | 2024 | Frontiers of Computer Science 19(8):198345 (2025); arXiv:2405.17935 | tool use, pipeline taxonomy, benchmarks |
| From LLM Reasoning to Autonomous AI Agents: A Comprehensive Review | [2504.19678](https://arxiv.org/abs/2504.19678) | / | 2025 | arXiv:2504.19678 | reasoning, autonomous agents, benchmarks |
| Survey on Evaluation of LLM-based Agents | [2503.16416](https://arxiv.org/abs/2503.16416) | / | 2025 | ACL Findings 2025; arXiv:2503.16416 | evaluation survey, benchmarks, web/SWE agents |
| Code as Agent Harness | [2605.18747](https://arxiv.org/abs/2605.18747) | [GitHub](https://github.com/YennNing/Awesome-Code-as-Agent-Harness-Papers) | 2026 | arXiv (preprint; HF #1 Paper of the Day) | survey, code-as-harness, harness taxonomy, multi-agent harness |
| Model or Harness? An Interaction-Centric Taxonomy for Localizing Agent Failures | [2607.28802](https://arxiv.org/abs/2607.28802) | / | 2026 | arXiv (preprint) | failure taxonomy, model-vs-harness attribution, agent evaluation, diagnosis |
| Multi-Agent Debate Strategies: Survey, Taxonomy, and Challenges | [2607.26212](https://arxiv.org/abs/2607.26212) | [GitHub](https://github.com/nlp4se/MAD-rep-package) | 2026 | arXiv (preprint) | multi-agent debate, survey, taxonomy, multi-agent harness |
| The Agent Loop: A Survey of Control Strategies, Skills, and Harnesses for LLM Agents | / | [GitHub](https://github.com/js-lee-AI/awesome-agent-loop-papers) | 2026 | SSRN preprint (2026-07) | survey, agent loop, harness, control strategies |

## 4. Foundations of the Agent Loop (2022–2023) (11)

*The 2022–2023 papers that established the reasoning+acting loop as a recognisable pattern. This is the foundational era — recent (2024–2026) work on searching and training the loop lives in [§7](#7-planning-search-self-improvement-loops) and [§13](#13-reasoning-models-test-time-scaling-for-agents).*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| Chain-of-Thought Prompting Elicits Reasoning in Large Language Models | [2201.11903](https://arxiv.org/abs/2201.11903) | / | 2022 | NeurIPS 2022 | chain-of-thought, few-shot prompting, reasoning |
| Large Language Models are Zero-Shot Reasoners | [2205.11916](https://arxiv.org/abs/2205.11916) | [GitHub](https://github.com/kojima-takeshi188/zero_shot_cot) | 2022 | NeurIPS 2022 | zero-shot, let's think step by step, prompting |
| MRKL Systems: A modular, neuro-symbolic architecture that combines large language models, external knowledge sources and discrete reasoning | [2205.00445](https://arxiv.org/abs/2205.00445) | / | 2022 | arXiv | neuro-symbolic, router, modular agents |
| Measuring and Narrowing the Compositionality Gap in Language Models (Self-Ask) | [2210.03350](https://arxiv.org/abs/2210.03350) | [GitHub](https://github.com/ofirpress/self-ask) | 2022 | TACL 2023 (arXiv Oct 2022) | question decomposition, multi-hop, follow-up sub-questions |
| ReAct: Synergizing Reasoning and Acting in Language Models | [2210.03629](https://arxiv.org/abs/2210.03629) | [GitHub](https://github.com/ysymyth/ReAct) | 2022 | ICLR 2023 | reasoning+action loop, tool use, agent |
| Self-Consistency Improves Chain of Thought Reasoning in Language Models | [2203.11171](https://arxiv.org/abs/2203.11171) | / | 2022 | ICLR 2023 | decoding, majority vote, ensemble |
| Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models | [2305.04091](https://arxiv.org/abs/2305.04091) | [GitHub](https://github.com/AGI-Edgerunners/Plan-and-Solve-Prompting) | 2023 | ACL 2023 | zero-shot, planning, decomposition |
| Reflexion: Language Agents with Verbal Reinforcement Learning | [2303.11366](https://arxiv.org/abs/2303.11366) | [GitHub](https://github.com/noahshinn/reflexion) | 2023 | NeurIPS 2023 | self-reflection, verbal RL, episodic memory |
| Self-Refine: Iterative Refinement with Self-Feedback | [2303.17651](https://arxiv.org/abs/2303.17651) | [GitHub](https://github.com/madaan/self-refine) | 2023 | NeurIPS 2023 | self-feedback, iterative refine, loop |
| Tool Learning with Foundation Models | [2304.08354](https://arxiv.org/abs/2304.08354) | / | 2023 | ACM Computing Surveys 57(4):1-40, 2024 (DOI 10.1145/3704435); arXiv:2304.08354 | tool use, tool-learning survey, foundation models |
| Tree of Thoughts: Deliberate Problem Solving with Large Language Models | [2305.10601](https://arxiv.org/abs/2305.10601) | [GitHub](https://github.com/princeton-nlp/tree-of-thought-llm) | 2023 | NeurIPS 2023 | tree search, self-evaluation, deliberation |

## 5. Tool Use & Function Calling (18)

*How a harness connects the model to external tools, APIs, and function calls.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| API-Bank: A Comprehensive Benchmark for Tool-Augmented LLMs | [2304.08244](https://arxiv.org/abs/2304.08244) | / | 2023 | EMNLP 23 | benchmark, API retrieval, planning+calling, evaluation |
| Gorilla: Large Language Model Connected with Massive APIs | [2305.15334](https://arxiv.org/abs/2305.15334) | [GitHub](https://github.com/ShishirPatil/gorilla) | 2023 | NeurIPS 2024 (arXiv 2023) | API calling, tool use, retrieval |
| NexusRaven: A Commercially-Permissive Language Model for Function Calling | / | [GitHub](https://github.com/nexusflowai/NexusRaven) | 2023 | NeurIPS 23 FM4DM Workshop | zero-shot function calling, nested/parallel calls, CodeLLaMA-13B, open-source |
| RestGPT: Connecting Large Language Models with Real-World RESTful APIs | [2306.06624](https://arxiv.org/abs/2306.06624) | [GitHub](https://github.com/Yifan-Song793/RestGPT) | 2023 | EMNLP 24 (arXiv 2023) | RESTful APIs, coarse-to-fine planning, RestBench, inference-time |
| TPTU: Large Language Model-based AI Agents for Task Planning and Tool Usage | [2308.03427](https://arxiv.org/abs/2308.03427) | / | 2023 | NeurIPS 23 FM4DM Workshop | task planning, tool usage, one-step/sequential agents, framework |
| Toolformer: Language Models Can Teach Themselves to Use Tools | [2302.04761](https://arxiv.org/abs/2302.04761) | / | 2023 | NeurIPS 2023 | tool learning, self-supervised, API calls |
| AnyTool: Self-Reflective, Hierarchical Agents for Large-Scale API Calls | [2402.04253](https://arxiv.org/abs/2402.04253) | [GitHub](https://github.com/dyabel/AnyTool) | 2024 | ICML 24 | hierarchical API retriever, self-reflection, AnyToolBench, 16000 APIs |
| ToolLLM: Facilitating Large Language Models to Master 16000+ Real-World APIs | [2307.16789](https://arxiv.org/abs/2307.16789) | [GitHub](https://github.com/OpenBMB/ToolBench) | 2024 | ICLR 24 | ToolBench dataset, DFSDT, instruction tuning, Rapid API |
| Hammer: Robust Function-Calling for On-Device Language Models via Function Masking | [2410.04587](https://arxiv.org/abs/2410.04587) | [GitHub](https://github.com/MadeAgents/Hammer) | 2025 | ACL 25 (Findings) | on-device, function masking, robustness, small models |
| The Berkeley Function Calling Leaderboard (BFCL): From Tool Use to Agentic Reasoning | / | [GitHub](https://github.com/ShishirPatil/gorilla/tree/main/berkeley-function-call-leaderboard) | 2025 | ICML 25 | benchmark, AST evaluation, parallel/multi-turn calls, de facto standard |
| ToolACE: Winning the Points of LLM Function Calling | [2409.00920](https://arxiv.org/abs/2409.00920) | / | 2025 | ICLR 25 | synthetic data generation, self-evolution, dual-layer verification, BFCL SOTA |
| Is Bash All You Need? An Empirical Study of Tool Interfaces for Enterprise Digital Worker Agents | [2609.11999](https://arxiv.org/abs/2609.11999) | / | 2026 | arXiv (preprint) | agent-computer interface, tool interfaces, empirical study, enterprise agents |
| MCPEvol-Bench: Benchmarking LLM Agent Performance Across Dynamic Evolutions of MCP Servers | [2607.14642](https://arxiv.org/abs/2607.14642) | [GitHub](https://github.com/Octobrist/MCPEvol-Bench) | 2026 | arXiv (preprint) | MCP, tool evolution, agent benchmark, agent-computer interface |
| Scalable LLM Agent Tool Access in the Cloud | [2607.15593](https://arxiv.org/abs/2607.15593) | / | 2026 | arXiv (preprint) | MCP, agent-server architecture, tool-access gateway, production deployment |
| SkillSeek: Revisiting Agent Skill Retrieval at Marketplace Scale | [2609.38822](https://arxiv.org/abs/2609.38822) | [GitHub](https://github.com/guanqun-yang/SkillSeek) | 2026 | AACL-IJCNLP 2026 | skill retrieval, agent-computer interface, MCP, harness evaluation |
| Speculate While You Reason: Teaching Agents to Predict Their Next Tool Call via Joint Agent-Speculator RL | [2607.25816](https://arxiv.org/abs/2607.25816) | / | 2026 | arXiv (preprint) | tool-call speculation, harness-aware training, latency hiding, agentic RL |
| The Bitter Lesson of Tool Calling | [2608.06370](https://arxiv.org/abs/2608.06370) | / | 2026 | arXiv (preprint) | tool-calling interface, agent-computer interface, empirical study, BFCL v4 |
| ToolSearcher: Optimizing Tool Selection at Scale via Reinforcement Learning | [2609.30906](https://arxiv.org/abs/2609.30906) | [GitHub](https://github.com/zhenlongDai/ToolSearcher) | 2026 | NeurIPS 2026 | tool selection, agentic RL, search loop, harness-aware training |

## 6. The Agent Harness & Scaffold (32)

*Papers where the harness itself — the agent-computer interface, scaffold, runtime, or context architecture — is the contribution. The conceptual core of this list.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors in Agents | [2308.10848](https://arxiv.org/abs/2308.10848) | [GitHub](https://github.com/OpenBMB/AgentVerse) | 2023 | ICLR 24 | multi-agent, dynamic-composition, recruitment, task-solving |
| CAMEL: Communicative Agents for 'Mind' Exploration of Large Language Model Society | [2303.17760](https://arxiv.org/abs/2303.17760) | [GitHub](https://github.com/camel-ai/camel) | 2023 | NeurIPS 23 | role-playing, inception-prompting, multi-agent, framework |
| ChatDev: Communicative Agents for Software Development | [2307.07924](https://arxiv.org/abs/2307.07924) | [GitHub](https://github.com/OpenBMB/ChatDev) | 2023 | ACL 24 | multi-agent, software-company-sim, chat-powered, role-phase |
| Generative Agents: Interactive Simulacra of Human Behavior | [2304.03442](https://arxiv.org/abs/2304.03442) | [GitHub](https://github.com/joonspk-research/generative_agents) | 2023 | UIST 23 (ACM) | memory-stream, reflection, planning, agent-architecture |
| MetaGPT: Meta Programming for A Multi-Agent Collaborative Framework | [2308.00352](https://arxiv.org/abs/2308.00352) | [GitHub](https://github.com/geekan/MetaGPT) | 2023 | ICLR 24 (Oral) | multi-agent, SOP, role-specialization, software-engineering |
| Voyager: An Open-Ended Embodied Agent with Large Language Models | [2305.16291](https://arxiv.org/abs/2305.16291) | [GitHub](https://github.com/MineDojo/Voyager) | 2023 | arXiv (NeurIPS 23 Agent Learning in Open-Endedness workshop, Spotlight) | skill-library, automatic-curriculum, lifelong-learning, code-as-skill |
| AgentScope: A Flexible yet Robust Multi-Agent Platform | [2402.14034](https://arxiv.org/abs/2402.14034) | [GitHub](https://github.com/modelscope/agentscope) | 2024 | arXiv 2024 (Alibaba) | multi-agent platform, fault-tolerant runtime, distributed harness, message hub |
| An Open Platform for AI Software Developers as Generalist Agents (OpenHands / fka OpenDevin) | [2407.16741](https://arxiv.org/abs/2407.16741) | [GitHub](https://github.com/OpenHands/OpenHands) | 2024 | arXiv (OpenReview) | open-platform, generalist-agent, code-web-browser, harness-platform |
| Perspectives and Designs Towards a Runtime for Autonomous LLM-Powered Applications (GoEX) | [2404.06921](https://arxiv.org/abs/2404.06921) | [GitHub](https://github.com/ShishirPatil/gorilla) | 2024 | arXiv (UC Berkeley / a16z) | agent runtime, execution engine, safety, permissioned actions |
| SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering | [2405.15793](https://arxiv.org/abs/2405.15793) | [GitHub](https://github.com/swe-agent/swe-agent) | 2024 | NeurIPS 24 | agent-computer-interface, software-engineering, scaffold, SWE-bench |
| Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models (ACE) | [2510.04618](https://arxiv.org/abs/2510.04618) | [GitHub](https://github.com/ace-agent/ace) | 2025 | ICLR 2026 (arXiv preprint Oct 2025) | context engineering, evolving playbooks, system prompt, agent memory |
| Meta-Harness: End-to-End Optimization of Model Harnesses | [2603.28052](https://arxiv.org/abs/2603.28052) | / | 2026 | arXiv (preprint, Stanford/MIT) | harness optimization, outer-loop search, agentic proposer, code optimization |
| Natural-Language Agent Harnesses | [2603.25723](https://arxiv.org/abs/2603.25723) | / | 2026 | arXiv (preprint) | harness representation, natural language policy, harness ablation, runtime |
| Harnessing LLM Agents with Skill Programs (HASP) | [2605.17734](https://arxiv.org/abs/2605.17734) | / | 2026 | arXiv | skill-programs, executable-guardrails, agent-loop-intervention, self-improvement |
| From Agent Loops to Structured Graphs: A Scheduler-Theoretic Framework (SGH) | [2604.11378](https://arxiv.org/abs/2604.11378) | / | 2026 | arXiv position paper | scheduler-theoretic, structured-graph-harness, static-DAG, 70-system-survey |
| Training Agents to Evolve with Their Harness: TaoLive Digital Avatar Agent Technical Report | [2608.15763](https://arxiv.org/abs/2608.15763) | / | 2026 | arXiv | harness-aware training, harness overfitting, runtime adaptation, agent RL |
| Can Agent Harnesses and Inference Engines Hear Each Other? The HEAR Protocol for Agentic LLM Serving | [2610.06597](https://arxiv.org/abs/2610.06597) | / | 2026 | arXiv (preprint) | harness-engine interface, agentic LLM serving, KV-cache coordination, serving protocol |
| Causal Improvement Graph for Agentic Harness Optimization | [2610.05039](https://arxiv.org/abs/2610.05039) | / | 2026 | arXiv (preprint) | harness optimization, meta-harness, agentic runtime, graph-governed search loop |
| DREvo: Distilling Recalibrated Historical Experience for Harness Self-Evolution | [2607.26722](https://arxiv.org/abs/2607.26722) | / | 2026 | arXiv (preprint) | harness self-evolution, experience recalibration, scaffold search, LLM agents |
| EvolveNet: Collaborative Harness Evolution for Agent Self-Improvement | [2608.04968](https://arxiv.org/abs/2608.04968) | [GitHub](https://github.com/junnie00/EvolveNet) | 2026 | arXiv (preprint) | harness evolution, collaborative self-improvement, program aggregation, multi-agent |
| Harness Evolution as Learning: Approximation, Generalization, and Optimization Limits of Self-Improving Personal Agents | [2609.36892](https://arxiv.org/abs/2609.36892) | [GitHub](https://github.com/ZyGan1999/self-evolving-harness-as-learning) | 2026 | arXiv (preprint) | self-evolving harness, personal agents, harness evaluation benchmark, learning theory (approximation/generalization/optimization) |
| Harness Learning Enables Generalizable Test-Time Adaptation | [2609.35738](https://arxiv.org/abs/2609.35738) | / | 2026 | arXiv (preprint) | harness learning, test-time adaptation, meta-learning over executable programs, reinforcement learning for agent scaffolds |
| Harness-Zero: Harness Distillation via Agent-as-Harness | [2609.24974](https://arxiv.org/abs/2609.24974) | [GitHub](https://github.com/metaevo-ai/harness-zero) | 2026 | arXiv (preprint) | harness-aware training, harness distillation, agent-as-harness, agent-computer interface |
| Learning from Research: Toward Lifelong Agent Harness Evolution | [2609.40169](https://arxiv.org/abs/2609.40169) | [GitHub](https://github.com/UCSB-NLP-Chang/ScholarEvolve) | 2026 | arXiv (preprint) | harness evolution, automated agent design, lifelong adaptation, agent scaffold |
| Loop Engineering: Building Blocks, Adoption, and Impact | [2608.21884](https://arxiv.org/abs/2608.21884) | / | 2026 | arXiv (preprint) | loop engineering, harness engineering, autonomous agent loops, empirical mining study |
| MESH-Harness: Self-Improving Agent Harnesses via Bandit-Guided Compositional Evolution | [2610.05300](https://arxiv.org/abs/2610.05300) | / | 2026 | arXiv (preprint) | agent harness optimization, compositional evolution, LinUCB bandits, evaluation-budget-constrained search |
| Mixture of Self-Improving Branches For Agent Harness Optimization | [2609.37834](https://arxiv.org/abs/2609.37834) | / | 2026 | arXiv (preprint) | harness optimization, recursive self-improvement, branch-and-router, agentic coding |
| OneDayAgent: Towards a Long-Horizon Harness for Autonomous Agents | [2608.05013](https://arxiv.org/abs/2608.05013) | [GitHub](https://github.com/zjunlp/OneDayAgent) | 2026 | arXiv (preprint) | long-horizon harness, agent scaffold, execution memory, harness-vs-model attribution |
| RRSI: Regularized Recursive Self-Improvement of Agent Harnesses | [2609.24972](https://arxiv.org/abs/2609.24972) | [GitHub](https://github.com/google-research/rrsi) | 2026 | arXiv (preprint) | agent harness, recursive self-improvement, harness evolution regularization, agent evaluation |
| TTHE: Test-Time Harness Evolution | [2607.08124](https://arxiv.org/abs/2607.08124) | [GitHub](https://github.com/junnie00/TTHE) | 2026 | arXiv (preprint) | test-time adaptation, harness evolution, scaffold, agentic search |
| VERSE: Verified Self-Evolving Optimizer for Agent Harnesses | [2610.02616](https://arxiv.org/abs/2610.02616) | [GitHub](https://github.com/wzekai/VERSE) | 2026 | arXiv (preprint) | harness evolution, self-evolving optimizer, execution-based verification, SWE agent evaluation |
| What Does a Harness Repair? A Preregistered Study of Visibility, Baseline Adequacy and Evaluation Defects | [2610.05533](https://arxiv.org/abs/2610.05533) | / | 2026 | arXiv (preprint) | harness search, GEPA, evaluation defects, preregistered evaluation |

## 7. Planning, Search & Self-Improvement Loops (10)

*Improving the loop itself via search, planning, self-reflection, and self-improvement over multi-turn trajectories.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| LLM+P: Empowering Large Language Models with Optimal Planning Proficiency | [2304.11477](https://arxiv.org/abs/2304.11477) | [GitHub](https://github.com/Cranial-XIX/llm-pddl) | 2023 | arXiv:2304.11477 (long-horizon planning) | PDDL, classical planner, long-horizon, symbolic |
| Agent Q: Advanced Reasoning and Learning for Autonomous AI Agents | [2408.07199](https://arxiv.org/abs/2408.07199) | / | 2024 | ICLR 2025 | agent loop, MCTS, self-critique, DPO |
| Code Generation with AlphaCodium: From Prompt Engineering to Flow Engineering | [2401.08500](https://arxiv.org/abs/2401.08500) | [GitHub](https://github.com/Codium-ai/AlphaCodium) | 2024 | arXiv:2401.08500 | test-based iterative flow, code generation, multi-stage, self-revision |
| Efficient Tool Use with Chain-of-Abstraction Reasoning | [2401.17464](https://arxiv.org/abs/2401.17464) | / | 2024 | ACL 24 (arXiv:2401.17464) | abstract placeholders, parallel tools, planning, tool-augmented |
| Language Agent Tree Search Unifies Reasoning Acting and Planning in Language Models | [2310.04406](https://arxiv.org/abs/2310.04406) | [GitHub](https://github.com/lapisrocks/LanguageAgentTreeSearch) | 2024 | ICML 24 (arXiv:2310.04406) | MCTS, tree search, value function, self-reflection |
| ReST-MCTS*: LLM Self-Training via Process Reward Guided Tree Search | [2406.03816](https://arxiv.org/abs/2406.03816) | [GitHub](https://github.com/THUDM/ReST-MCTS) | 2024 | NeurIPS 24 (arXiv:2406.03816) | process reward, MCTS, self-training, reasoning |
| ToRA: A Tool-Integrated Reasoning Agent for Mathematical Problem Solving | [2309.17452](https://arxiv.org/abs/2309.17452) | [GitHub](https://github.com/microsoft/ToRA) | 2024 | ICLR 2024 | tool-integrated reasoning loop, code execution, outcome RL |
| Search-o1: Agentic Search-Enhanced Large Reasoning Models | [2501.05366](https://arxiv.org/abs/2501.05366) | [GitHub](https://github.com/RUC-NLPIR/Search-o1) | 2025 | arXiv 2501.05366 | reasoning-search loop, inference-time, agentic search |
| SiriuS: Self-improving Multi-agent Systems via Bootstrapped Reasoning | [2502.04780](https://arxiv.org/abs/2502.04780) | [GitHub](https://github.com/zou-group/sirius) | 2025 | NeurIPS 2025 | self-improvement loop, reasoning library, multi-agent |
| rStar-Math: Small LLMs Can Master Math Reasoning with Self-Evolved Deep Thinking | [2501.04519](https://arxiv.org/abs/2501.04519) | [GitHub](https://github.com/microsoft/rStar) | 2025 | ICML 25 (arXiv:2501.04519) | MCTS, process preference model, self-evolution, test-time search |

## 8. Memory-Augmented Agents (19)

*Memory and context management — how a harness carries state across turns and sessions.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| MemGPT: Towards LLMs as Operating Systems | [2310.08560](https://arxiv.org/abs/2310.08560) | [GitHub](https://github.com/cpacker/MemGPT) | 2023 | arXiv:2310.08560 (COLM 2024) | virtual memory, OS-inspired, context management, multi-session chat |
| MemoryBank: Enhancing Large Language Models with Long-Term Memory | [2305.10250](https://arxiv.org/abs/2305.10250) | [GitHub](https://github.com/zhongwanjun/MemoryBank-SiliconFriend) | 2023 | arXiv:2305.10250 (AAAI 2024) | long-term memory, Ebbinghaus forgetting, personality, companion chatbot |
| Evaluating Very Long-Term Conversational Memory of LLM Agents (LoCoMo) | [2402.17753](https://arxiv.org/abs/2402.17753) | [GitHub](https://github.com/snap-research/locomo) | 2024 | ACL 2024 (arXiv:2402.17753) | benchmark, long-term dialogue, temporal reasoning, event graph |
| Letta (formerly MemGPT): open-source framework for stateful, self-editing-memory LLM agents | / | [GitHub](https://github.com/letta-ai/letta) | 2024 | Open-source framework (software; not a paper) | self-editing memory, memory blocks, stateful agents, tool-calling |
| LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory | [2410.10813](https://arxiv.org/abs/2410.10813) | [GitHub](https://github.com/xiaowu0162/LongMemEval) | 2024 | arXiv:2410.10813 (ICLR 2025) | benchmark, indexing-retrieval-reading, knowledge update, abstention |
| Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach | [2407.16833](https://arxiv.org/abs/2407.16833) | [GitHub](https://github.com/xiaowu0162/LongMemEval) | 2024 | EMNLP 2024 industry track (arXiv:2407.16833) | RAG vs long-context, Self-Route, cost-performance, self-reflection routing |
| A-MEM: Agentic Memory for LLM Agents | [2502.12110](https://arxiv.org/abs/2502.12110) | [GitHub](https://github.com/WujiangXu/A-mem) | 2025 | arXiv:2502.12110 | Zettelkasten, dynamic linking, memory evolution, agentic memory |
| Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory | [2504.19413](https://arxiv.org/abs/2504.19413) | [GitHub](https://github.com/mem0ai/mem0) | 2025 | ECAI 2025 (arXiv:2504.19413) | memory layer, graph memory, LOCOMO benchmark, production |
| Memory in the Age of AI Agents | [2512.13564](https://arxiv.org/abs/2512.13564) | [GitHub](https://github.com/Shichun-Liu/Agent-Memory-Paper-List) | 2025 | arXiv:2512.13564 | survey, forms/functions/dynamics, taxonomy, self-evolving |
| AgenticSTS: A Bounded-Memory Testbed for Long-Horizon LLM Agents | [2607.02255](https://arxiv.org/abs/2607.02255) | [GitHub](https://github.com/AlayaLab/AgenticSTS) | 2026 | arXiv (EMNLP 2026 ARR, under review) | memory architecture, context engineering, long-horizon agents, benchmark |
| BaRe-Mem: Bayesian Reliability Memory for Robust and Adaptive Agent Consultation | [2609.35551](https://arxiv.org/abs/2609.35551) | [GitHub](https://github.com/declare-lab/BaRe-Mem) | 2026 | arXiv (preprint) | memory architecture, multi-agent harness, reliability estimation, bayesian |
| ERRAND: Budgeted Maintenance of Agent Memory | [2609.29545](https://arxiv.org/abs/2609.29545) | / | 2026 | arXiv (preprint) | memory maintenance, action budget, staleness revalidation, agent loop |
| Ground Truth First: A Longitudinal Evaluation Instrument for Agent Memory, and the Tenure Crossover in Memory-Architecture Rankings | [2607.21962](https://arxiv.org/abs/2607.21962) | [GitHub](https://github.com/veracium-ai/Veracium) | 2026 | arXiv (preprint) | agent memory, benchmark, evaluation methodology, longitudinal |
| LeanMem: Simple and Efficient Long-Term Memory for LLM Agents | [2608.03463](https://arxiv.org/abs/2608.03463) | / | 2026 | arXiv (preprint) | long-term memory, memory architecture, efficiency, conversational QA |
| Learn Now, Use Next, Trust Later: Prequential Test-Time Learning for LLM Agents | [2609.35911](https://arxiv.org/abs/2609.35911) | / | 2026 | arXiv (preprint) | agent memory architecture, test-time learning, experience reuse, non-parametric harness |
| MemFold: Learning Compact Soft Memory for Long-Context Personalization via On-Policy Optimization | [2609.36435](https://arxiv.org/abs/2609.36435) | [GitHub](https://github.com/Johnny221B/memfold) | 2026 | arXiv (preprint) | soft memory, memory architecture, on-policy training, personalization |
| PM-Bench: Evaluating Prospective Memory in LLM Agents | [2607.12385](https://arxiv.org/abs/2607.12385) | [GitHub](https://github.com/genglinliu/PMBench) | 2026 | COLM 2026 | memory benchmark, prospective memory, agent scaffolds, evaluation |
| Self-Designed Evaluators and Warm Memory for Long-Horizon Agents | [2609.33717](https://arxiv.org/abs/2609.33717) | / | 2026 | arXiv (preprint) | agent memory architecture, self-designed evaluators, retry loop, label-free self-improvement |
| When Should Agents Check External State? Budgeting Observations for Stored Intentions | [2609.37125](https://arxiv.org/abs/2609.37125) | / | 2026 | arXiv (preprint) | memory architecture, prospective memory, observation budgeting, harness policy |

## 9. Multi-Agent Systems (15)

*Orchestrating multiple agents that debate, collaborate, or specialise.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation | [2308.08155](https://arxiv.org/abs/2308.08155) | [GitHub](https://github.com/microsoft/autogen) | 2023 | COLM 2024 (arXiv Aug 2023) | multi-agent conversation, conversable agents, framework |
| ChatEval: Towards Better LLM-based Evaluators through Multi-Agent Debate | [2308.07201](https://arxiv.org/abs/2308.07201) | [GitHub](https://github.com/chanchimin/ChatEval) | 2023 | ICLR 2024 | multi-agent debate, LLM evaluation, referee team |
| Improving Factuality and Reasoning in Language Models through Multiagent Debate | [2305.14325](https://arxiv.org/abs/2305.14325) | [GitHub](https://github.com/composable-models/llm_multiagent_debate) | 2023 | ICML 2024 (arXiv May 2023) | multi-agent debate, factuality, test-time scaling, society of minds |
| MACM: Utilizing a Multi-Agent System for Condition Mining in Solving Complex Mathematical Problems | [2404.04735](https://arxiv.org/abs/2404.04735) | [GitHub](https://github.com/bin123apple/MACM) | 2024 | NeurIPS 2024 (Poster) | math reasoning, condition mining, prompting |
| More Agents Is All You Need | [2402.05120](https://arxiv.org/abs/2402.05120) | [GitHub](https://github.com/MoreAgentsIsAllYouNeed/AgentForest) | 2024 | TMLR (Transactions on Machine Learning Research) | scaling, sampling-and-voting, Agent Forest |
| Revisiting Multi-Agent Debate as Test-Time Scaling: A Systematic Study of Conditional Effectiveness | [2505.22960](https://arxiv.org/abs/2505.22960) | [GitHub](https://github.com/euiin/MAD_as_TTS) | 2025 | arXiv (under review) | test-time scaling, multi-agent debate, conditional effectiveness |
| Why Do Multi-Agent LLM Systems Fail? | [2503.13657](https://arxiv.org/abs/2503.13657) | [GitHub](https://github.com/multi-agent-systems-failure-taxonomy/MAST) | 2025 | NeurIPS 2025 (Poster) | failure taxonomy, MAST, diagnostics |
| Agensh: Scaling Organizational Intelligence to 1,024 Agents | [2609.26781](https://arxiv.org/abs/2609.26781) | / | 2026 | arXiv (preprint) | multi-agent harness, self-organization, agent scaling, shared context |
| AgentWorld: Benchmarking Long-Horizon Collaboration of Multi-agent LLMs | [2609.31590](https://arxiv.org/abs/2609.31590) | [GitHub](https://github.com/openagents-org/agentworld) | 2026 | COLM 2026 | multi-agent benchmark, long-horizon collaboration, sandbox environment, collaboration metric |
| Group Perspective Matters: Regulating Debate Relationships Can Mitigate Blind Conformity in Multi-Agent Debate | [2608.03648](https://arxiv.org/abs/2608.03648) | / | 2026 | arXiv (preprint) | multi-agent debate, dynamic communication topology, RL-learned orchestration, blind conformity |
| Pay for the Fault, Not the Flow: Label-Free In-Flow Multi-Agent Workflow Optimization | [2610.01017](https://arxiv.org/abs/2610.01017) | / | 2026 | arXiv (preprint) | multi-agent workflow optimization, label-free cost model, in-flow fault correction, multi-agent benchmark |
| ProgRouter: Online Progress-Guided Orchestration for Multi-Agent LLM Workflows under Quality-Cost Tradeoffs | [2608.25992](https://arxiv.org/abs/2608.25992) | / | 2026 | EMNLP 2026 Findings | multi-agent orchestration, LLM routing, task-progress prediction, quality-cost tradeoff |
| SwarmBench: Can Large Language Models Act as Agent Swarm Orchestrators? | [2608.30661](https://arxiv.org/abs/2608.30661) | [GitHub](https://github.com/ying1973/SwarmBench) | 2026 | EMNLP 2026 Findings | multi-agent orchestration, benchmark, LLM-as-orchestrator, experience replay |
| Two Calls Beat Five Agents: Evaluating Multi-Agent Pipelines Against Self-Refinement for Local Language Models | [2607.26922](https://arxiv.org/abs/2607.26922) | / | 2026 | arXiv (preprint) | multi-agent pipelines, self-refinement, local/small models, harness evaluation |
| Who Broke the System? Failure Localization in LLM-Based Multi-Agent Systems | [2607.07989](https://arxiv.org/abs/2607.07989) | [GitHub](https://github.com/YufeiXIA/AgentLocate) | 2026 | COLM 2026 | multi-agent failure localization, LLM-as-judge verification loop, MAST failure taxonomy, harness diagnostics |

## 10. Code & SWE Agents (15)

*Domain harnesses for software engineering — the cleanest measurable testbed for harness design.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| Aider (AI pair programming CLI tool) | / | [GitHub](https://github.com/Aider-AI/aider) | 2024 | Tool / open-source project (no arXiv paper) | pair-programming, cli-tool, leaderboard, edit-formats |
| AutoCodeRover: Autonomous Program Improvement | [2404.05427](https://arxiv.org/abs/2404.05427) | [GitHub](https://github.com/AutoCodeRoverSG/auto-code-rover) | 2024 | ISSTA 2024 | AST-search, fault-localization, program-repair, issue-resolution |
| CodeR: Issue Resolving with Multi-Agent and Task Graphs | [2406.01304](https://arxiv.org/abs/2406.01304) | [GitHub](https://github.com/NL2Code/CodeR) | 2024 | arXiv 2024 (preprint) | multi-agent, task-graphs, issue-resolution, repository |
| Devon (open-source Devin alternative) | / | [GitHub](https://github.com/vunderkind/devon) | 2024 | Tool / open-source project (no arXiv paper) | open-source, software-engineer-agent, devin-alternative, cli |
| Executable Code Actions Elicit Better LLM Agents (CodeAct) | [2402.01030](https://arxiv.org/abs/2402.01030) | [GitHub](https://github.com/xingyaoww/code-act) | 2024 | ICML 2024 | action-space, code-as-action, interpreter, agent-finetuning |
| Moatless Tools | / | [GitHub](https://github.com/aorwall/moatless-tools) | 2024 | Tool / open-source project (no arXiv paper) | context-retrieval, code-search, issue-resolution, swe-bench |
| Agentless: Demystifying LLM-based Software Engineering Agents | [2407.01489](https://arxiv.org/abs/2407.01489) | [GitHub](https://github.com/OpenAutoCoder/Agentless) | 2025 | ICSE/FSE 2025 | localization, repair, interpretability, no-agent |
| Training Software Engineering Agents and Verifiers with SWE-Gym | [2412.21139](https://arxiv.org/abs/2412.21139) | [GitHub](https://github.com/SWE-Gym/SWE-Gym) | 2025 | ICML 2025 | training-environment, fine-tuning, verifier, inference-scaling |
| An Empirical Study of Harness Design for Coding Agents | [2609.20804](https://arxiv.org/abs/2609.20804) | / | 2026 | arXiv (preprint) | coding-agent harness, component-level empirical evaluation, context management, planning and action-space ablation |
| Failure as a Process: An Anatomy of CLI Coding Agent Trajectories | [2607.09510](https://arxiv.org/abs/2607.09510) | [GitHub](https://github.com/xz-Sean/cli_trajectory_analysis) | 2026 | arXiv (preprint) | empirical study, coding-agent failures, scaffold comparison, trajectory benchmark |
| Harness or Model? Isolating the Harness Effect in Agentic Coding with a Contamination-Controlled Private Suite | [2609.11987](https://arxiv.org/abs/2609.11987) | / | 2026 | arXiv (preprint) | agentic coding, harness effect, benchmark/study, contamination control |
| Harness-of-Harness: Multi-Day Autonomous Software Development with Continual Improvement | [2609.01481](https://arxiv.org/abs/2609.01481) | [GitHub](https://github.com/Flesymeb/HarnessOfHarness) | 2026 | arXiv (preprint) | meta-harness, coding-agent scaffold, planning-coding-testing loop, long-horizon autonomous SWE |
| KAT-Coder-V2.5 Technical Report | [2607.05471](https://arxiv.org/abs/2607.05471) | / | 2026 | arXiv (industry technical report) | harness-aware training, agentic RL, SWE agent, verifiable environments |
| Mid-Harness: Scaling Actions Between Model and Harness for Terminal Agents | [2609.39982](https://arxiv.org/abs/2609.39982) | / | 2026 | arXiv (preprint) | test-time scaling, action verification, terminal agent, harness scaffold |
| openJiuwen: Beyond Static Harnesses for Long-Horizon Coding Agents | [2608.27969](https://arxiv.org/abs/2608.27969) | [GitHub](https://github.com/openJiuwen-ai/jiuwenswarm) | 2026 | arXiv (preprint) | agent harness, coding agents, multi-agent orchestration, SWE-bench |

## 11. Web, GUI & Computer-Use Agents (23)

*Domain harnesses for the web, desktop GUIs, and computer use.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| WebShop: Towards Scalable Real-World Web Interaction with Grounded Language Agents | [2207.01206](https://arxiv.org/abs/2207.01206) | [GitHub](https://github.com/princeton-nlp/WebShop) | 2022 | NeurIPS 2022 | foundational web benchmark, interactive shopping, instruction following, grounded agent |
| Mind2Web: Towards a Generalist Agent for the Web | [2306.06070](https://arxiv.org/abs/2306.06070) | [GitHub](https://github.com/OSU-NLP-Group/Mind2Web) | 2023 | NeurIPS 2023 (Datasets and Benchmarks) | web dataset, generalist agent, element grounding, 137 websites |
| WebArena: A Realistic Web Environment for Building Autonomous Agents | [2307.13854](https://arxiv.org/abs/2307.13854) | [GitHub](https://github.com/web-arena-x/webarena) | 2023 | arXiv (CMU/CMU-affiliated); widely cited, ICLR-era | web benchmark, autonomous agent, self-hosted websites, functional correctness |
| AndroidWorld: A Dynamic Benchmarking Environment for Autonomous Agents | [2405.14573](https://arxiv.org/abs/2405.14573) | [GitHub](https://github.com/google-research/android_world) | 2024 | arXiv 2024 (Google DeepMind) | Android benchmark, dynamic tasks, programmatic reward, mobile agent |
| GPT-4V(ision) is a Generalist Web Agent, if Grounded (SeeAct) | [2401.01614](https://arxiv.org/abs/2401.01614) | [GitHub](https://github.com/OSU-NLP-Group/SeeAct) | 2024 | ICML 2024 | LMM web agent, GPT-4V, visual grounding, screenshot agent |
| OS-ATLAS: A Foundation Action Model for Generalist GUI Agents | [2410.23218](https://arxiv.org/abs/2410.23218) | [GitHub](https://github.com/OS-Copilot/OS-Atlas) | 2024 | ICLR 2025 (arXiv Oct 2024) | GUI grounding foundation model, cross-platform, 13M elements dataset, OOD generalization |
| OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments | [2404.07972](https://arxiv.org/abs/2404.07972) | [GitHub](https://github.com/xlang-ai/OSWorld) | 2024 | NeurIPS 2024 | computer-use benchmark, real OS environment, multimodal agent, GUI grounding |
| OmniACT: A Dataset and Benchmark for Enabling Multimodal Generalist Autonomous Agents for Desktop and Web Automation | [2402.17553](https://arxiv.org/abs/2402.17553) | / | 2024 | arXiv 2024 (CMU-affiliated) | desktop+web automation, executable programs, multimodal benchmark, generalist agent |
| ShowUI: One Vision-Language-Action Model for GUI Visual Agent | [2411.17465](https://arxiv.org/abs/2411.17465) | [GitHub](https://github.com/showlab/ShowUI) | 2024 | CVPR 2025 (arXiv Nov 2024) | vision-language-action, GUI grounding, UI token selection, 2B model |
| VisualWebArena: Evaluating Multimodal Agents on Realistic Visual Web Tasks | [2401.13649](https://arxiv.org/abs/2401.13649) | [GitHub](https://github.com/web-arena-x/visualwebarena) | 2024 | ACL 2024 | multimodal web benchmark, visually grounded tasks, WebArena extension, 910 tasks |
| WebVoyager: Building an End-to-End Web Agent with Large Multimodal Models | [2401.13919](https://arxiv.org/abs/2401.13919) | [GitHub](https://github.com/MinorJerry/WebVoyager) | 2024 | ACL 2024 | LMM web agent, end-to-end, real websites, rubric evaluation |
| An Illusion of Progress? Assessing the Current State of Web Agents | [2504.01382](https://arxiv.org/abs/2504.01382) | [GitHub](https://github.com/OSU-NLP-Group/Online-Mind2Web) | 2025 | arXiv 2025 (Apr 2025) | online web benchmark, realistic evaluation, progress skepticism, Mind2Web successor |
| Benchmarking General Mobile Assistants in Challenging Real-World Scenarios | [2608.27477](https://arxiv.org/abs/2608.27477) | [GitHub](https://github.com/Tongyi-Zhiwen/GMA) | 2026 | arXiv (preprint) | mobile GUI agent benchmark, harness ablation, context retention, explicit state tracking |
| CAP: A Scalable Benchmark for Evaluating Cross-Site Browser Agents with Complex Actions and Perception | [2608.08392](https://arxiv.org/abs/2608.08392) | [GitHub](https://github.com/WarriorXu0302/CAP-Bench) | 2026 | COLM 2026 | browser-agent benchmark, cross-site workflows, complex UI actions, visual perception |
| DevicesWorld: Benchmarking Cross-Device Agents in Heterogeneous Environments | [2607.13465](https://arxiv.org/abs/2607.13465) | [GitHub](https://github.com/AgenticOrgLab/DevicesWorld) | 2026 | arXiv (preprint) | benchmark, GUI agents, agent-computer interface, cross-device |
| Interactive Reward Agent: GUI Task Evaluation via Environment-State Verification | [2607.25904](https://arxiv.org/abs/2607.25904) | [GitHub](https://github.com/Kendrick-Stein/InteractiveRewardAgent-OfficialRepo) | 2026 | arXiv (preprint) | GUI agent evaluation, reward model, computer-use, verification loop |
| KnowAct-GUIClaw: Know Deeply, Act Perfectly, Personal GUI Assistant with Self-Evolving Memory and Skill | [2607.12625](https://arxiv.org/abs/2607.12625) | [GitHub](https://github.com/HITsz-TMG/KnowAct) | 2026 | arXiv (preprint) | GUI agent, skill library, memory architecture, multi-agent scaffold |
| macOS Harness (browser-use/macos-harness) | / | [GitHub](https://github.com/browser-use/macos-harness) | 2026 | Tool / open-source project (no arXiv paper) | agent-computer interface, computer-use harness, GUI automation, macOS |
| OSWorld 2.0: Benchmarking Computer Use Agents on Long-Horizon Real-World Tasks | [2606.29537](https://arxiv.org/abs/2606.29537) | [GitHub](https://github.com/xlang-ai/OSWorld-V2) | 2026 | arXiv (preprint) | computer-use agent, agent-computer interface, long-horizon benchmark, evaluation environment runtime |
| Qwen-UI-Agent Technical Report: Toward Next-Generation Real-World Centric Foundation GUI Agents | [2607.28227](https://arxiv.org/abs/2607.28227) | [GitHub](https://github.com/Tongyi-MAI/Qwen-UI-Agent) | 2026 | arXiv (industry technical report) | GUI agent, agent-computer interface, harness layer, harness-aware training |
| WebMCP-Phalanx: Enforcing and Characterizing Trust Boundaries for Browser-Integrated LLM Agents | [2608.24017](https://arxiv.org/abs/2608.24017) | / | 2026 | arXiv (preprint) | agent runtime, agent-computer interface, WebMCP browser agents, prompt-injection defense |
| WebRetriever: A Large-Scale Comprehensive Benchmark for Efficient Web Agent Evaluation | [2607.06118](https://arxiv.org/abs/2607.06118) | [GitHub](https://github.com/Mininglamp-AI/WebRetriever) | 2026 | arXiv (preprint) | web-agent benchmark, evaluation harness, LLM-as-judge, browser agent |
| Wuying-Browser-Agent: Real-World Centric Fundamental Long-Horizon Browser Agents | [2608.17319](https://arxiv.org/abs/2608.17319) | / | 2026 | arXiv (preprint) | browser agent, agent-computer interface, harness-aware training, web benchmark |

## 12. Benchmarks & Evaluation (19)

*Evaluation suites that stress-test agent harnesses.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| AgentBench: Evaluating LLMs as Agents | [2308.03688](https://arxiv.org/abs/2308.03688) | [GitHub](https://github.com/THUDM/AgentBench) | 2024 | ICLR 2024 | agent benchmark, LLM-as-agent, multi-environment, evaluation |
| AgentBoard: An Analytical Evaluation Board of Multi-turn LLM Agents | [2401.13178](https://arxiv.org/abs/2401.13178) | [GitHub](https://github.com/StonyBrookNLP/appworld) | 2024 | NeurIPS 2024 (Oral, Datasets and Benchmarks) | analytical evaluation, progress rate, multi-turn, fine-grained metrics |
| AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents | [2407.18901](https://arxiv.org/abs/2407.18901) | [GitHub](https://github.com/StonyBrookNLP/appworld) | 2024 | ACL 2024 (Long) | interactive coding, API tools, multi-app, state-based unit tests |
| GAIA: a benchmark for General AI Assistants | [2311.12983](https://arxiv.org/abs/2311.12983) | / | 2024 | NeurIPS 2024 (Datasets and Benchmarks) | general assistant, tool-use, multi-modal, real-world QA |
| SWE-bench: Can Language Models Resolve Real-World GitHub Issues? | [2310.06770](https://arxiv.org/abs/2310.06770) | [GitHub](https://github.com/swe-bench/SWE-bench) | 2024 | ICLR 2024 | benchmark, software-engineering, issue-resolution, github |
| tau-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains | [2406.12045](https://arxiv.org/abs/2406.12045) | [GitHub](https://github.com/sierra-research/tau2-bench) | 2024 | arXiv (NeurIPS 2025) | tool-use, policy adherence, pass^k metric, multi-turn |
| BrowseComp: A Simple Yet Challenging Benchmark for Browsing Agents | [2504.12516](https://arxiv.org/abs/2504.12516) | [GitHub](https://github.com/openai/simple-evals) | 2025 | arXiv (OpenAI) | browsing agent, hard-to-find information, short-answer verification, web search |
| Evaluation and Benchmarking of LLM Agents: A Survey | [2507.21504](https://arxiv.org/abs/2507.21504) | [GitHub](https://github.com/Asaf-Yehudai/LLM-Agent-Evaluation-Survey) | 2025 | arXiv | evaluation taxonomy, survey, reliability, metrics |
| tau^2-Bench: Evaluating Conversational Agents in a Dual-Control Environment | [2506.07982](https://arxiv.org/abs/2506.07982) | [GitHub](https://github.com/sierra-research/tau2-bench) | 2025 | arXiv | dual-control, Dec-POMDP, user coordination, compositional tasks |
| Evo-Bench: Can Language Models Improve Agent Harness? | [2608.09096](https://arxiv.org/abs/2608.09096) | [GitHub](https://github.com/RUCAIBox/Evo-Bench) | 2026 | arXiv (preprint) | benchmark, agent harness, harness improvement, LLM agents |
| EvoHarnessBench: Can Your Agents Keep Pace with an Evolving Harness? | [2609.04280](https://arxiv.org/abs/2609.04280) | / | 2026 | arXiv (preprint) | benchmark, harness evolution, harness-induced forgetting, agent retention/adaptation |
| Grounded Checklist Partial Credit for Agent Skill Trajectories | [2608.27487](https://arxiv.org/abs/2608.27487) | / | 2026 | arXiv (preprint) | agent evaluation, partial-credit scoring, agent skills (SKILL.md), SkillsBench |
| HarnessOpt-Bench: Evaluating LLMs at Harness Optimization | [2608.06301](https://arxiv.org/abs/2608.06301) | / | 2026 | arXiv (preprint) | benchmark, harness-optimization, trusted-execution, agent-evaluation |
| HarnessSafe: Evaluating Safety Across Persistent Carriers in Agent Harnesses | [2608.06984](https://arxiv.org/abs/2608.06984) | / | 2026 | arXiv (preprint) | safety benchmark, harness evaluation, persistent carriers, cross-harness containment |
| Long-Horizon-Terminal-Bench: Testing the Limits of Agents on Long-Horizon Terminal Tasks with Dense Reward-Based Grading | [2607.08964](https://arxiv.org/abs/2607.08964) | [GitHub](https://github.com/zli12321/LHTB) | 2026 | arXiv (preprint) | benchmark, long-horizon agents, terminal agents, dense reward grading |
| Rethinking the Evaluation of Harness Evolution for Agents | [2607.12227](https://arxiv.org/abs/2607.12227) | [GitHub](https://github.com/rethinking-harness-evolution/code) | 2026 | arXiv (preprint) | harness evolution, evaluation methodology, test-time scaling, benchmark study |
| SWE Refactor Bench: Can Coding Agents Complete a Long-Horizon, Whole-Repository Stack Migration? | [2608.23564](https://arxiv.org/abs/2608.23564) | [GitHub](https://github.com/Einsia/SWE-Refactor-Bench) | 2026 | arXiv (preprint) | SWE benchmark, long-horizon whole-repo migration, agentic multi-agent verification, reward hacking |
| SWE-bench Science: Can Coding Agents Resolve Engineering Tasks in Science? | [2608.19799](https://arxiv.org/abs/2608.19799) | [GitHub](https://github.com/OpenMOSS/SWE-bench-Science) | 2026 | arXiv (preprint) | SWE-bench-family benchmark, coding agents, scientific software engineering, failure analysis |
| UniClawBench: A Universal Benchmark for Proactive Agents on Real-World Tasks | [2607.08768](https://arxiv.org/abs/2607.08768) | [GitHub](https://github.com/HKU-MMLab/UniClawBench) | 2026 | arXiv (preprint) | benchmark, harness-vs-model study, proactive agents, real-world environments |

## 13. Reasoning Models & Test-Time Scaling for Agents (33)

*Training the loop: reasoning models, test-time scaling, and multi-turn RL for agents.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| Agent-FLAN: Designing Data and Methods of Effective Agent Tuning for Large Language Models | [2403.12881](https://arxiv.org/abs/2403.12881) | [GitHub](https://github.com/InternLM/Agent-FLAN) | 2024 | ACL 2024 Findings (arXiv 2403.12881) | agent-tuning, data-design, reasoning-decoupling, SFT |
| AgentTrek: Agent Trajectory Synthesis via Guiding Replay with Web Tutorials | [2412.09605](https://arxiv.org/abs/2412.09605) | [GitHub](https://github.com/xlang-ai/AgentTrek) | 2024 | ICLR 2025 (arXiv 2412.09605) | trajectory-synthesis, GUI-agent, web-tutorial, data-scaling |
| AutoAct: Automatic Agent Learning from Scratch for QA via Self-Planning | [2401.05268](https://arxiv.org/abs/2401.05268) | [GitHub](https://github.com/zjunlp/AutoAct) | 2024 | ACL 2024 | self-planning loop, trajectory synthesis, distillation |
| OpenAI o1 System Card | [2412.16720](https://arxiv.org/abs/2412.16720) | / | 2024 | arXiv 2412.16720 (OpenAI technical report) | reasoning-model, chain-of-thought, RLHF, system-card |
| Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters | [2408.03314](https://arxiv.org/abs/2408.03314) | / | 2024 | ICLR 2025 (arXiv 2408.03314) | test-time-compute, process-reward-model, inference-scaling, compute-optimal |
| Training Language Models to Self-Correct via Reinforcement Learning (SCoRe) | [2409.12917](https://arxiv.org/abs/2409.12917) | / | 2024 | ICLR 2025 (arXiv 2409.12917) | self-correction, multi-turn-RL, intrinsic-correction, online-RL |
| Watch Every Step! LLM Agent Learning via Iterative Step-Level Process Refinement | [2406.11176](https://arxiv.org/abs/2406.11176) | [GitHub](https://github.com/WeiminXiong/IPR) | 2024 | EMNLP 2024 | step-level reward, process refinement, loop training |
| WebRL: Training LLM Web Agents via Self-Evolving Online Curriculum Reinforcement Learning | [2411.02337](https://arxiv.org/abs/2411.02337) | [GitHub](https://github.com/THUDM/WebRL) | 2024 | ICLR 2025 | self-evolving loop, online curriculum, web agent RL |
| Absolute Zero: Reinforced Self-play Reasoning with Zero Data | [2505.03335](https://arxiv.org/abs/2505.03335) | [GitHub](https://github.com/LeapLabTHU/Absolute-Zero-Reasoner) | 2025 | arXiv 2505.03335 | self-play, RLVR, zero-data, self-evolving-curriculum |
| Agent-R: Training Language Model Agents to Reflect via Iterative Self-Training | [2501.11425](https://arxiv.org/abs/2501.11425) | [GitHub](https://github.com/ByteDance-Seed/Agent-R) | 2025 | arXiv 2501.11425 | iterative-self-training, reflection, on-the-fly-correction, agent-tuning |
| Agent0: Unleashing Self-Evolving Agents from Zero Data via Tool-Integrated Reasoning | [2511.16043](https://arxiv.org/abs/2511.16043) | [GitHub](https://github.com/aiming-lab/Agent0) | 2025 | arXiv 2511.16043 | self-evolution loop, zero-data, tool-integrated reasoning |
| AgentEvolver: Towards Efficient Self-Evolving Agent System | [2511.10395](https://arxiv.org/abs/2511.10395) | [GitHub](https://github.com/modelscope/AgentEvolver) | 2025 | arXiv 2511.10395 | self-evolution loop, self-questioning, self-attributing |
| DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning | [2501.12948](https://arxiv.org/abs/2501.12948) | [GitHub](https://github.com/deepseek-ai/DeepSeek-R1) | 2025 | Nature (DOI 10.1038/s41586-025-09422-z); arXiv 2501.12948 | pure-RL-reasoning, RLVR, GRPO, self-reflection |
| RAGEN: Understanding Self-Evolution in LLM Agents via Multi-Turn Reinforcement Learning | [2504.20073](https://arxiv.org/abs/2504.20073) | [GitHub](https://github.com/RAGEN-AI/RAGEN) | 2025 | arXiv 2504.20073 | multi-turn-agent-RL, trajectory-level-RL, StarPO, Echo-Trap |
| ReSearch: Learning to Reason with Search for LLMs via Reinforcement Learning | [2503.19470](https://arxiv.org/abs/2503.19470) | [GitHub](https://github.com/Agent-RL/ReSearch) | 2025 | NeurIPS 2025 (arXiv 2503.19470) | reasoning-search-RL, multi-hop, self-correction, no-SFT |
| ReTool: Reinforcement Learning for Strategic Tool Use in LLMs | [2504.11536](https://arxiv.org/abs/2504.11536) | [GitHub](https://github.com/ReTool-RL/ReTool) | 2025 | arXiv 2504.11536 (ByteDance Seed) | tool-integrated-RL, code-execution, outcome-reward, aha-moment |
| Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning | [2503.09516](https://arxiv.org/abs/2503.09516) | [GitHub](https://github.com/PeterGriffinJin/Search-R1) | 2025 | COLM 2025 (arXiv 2503.09516) | retrieval-augmented-RL, retrieved-token-masking, reasoning-search, outcome-reward |
| s1: Simple test-time scaling | [2501.19393](https://arxiv.org/abs/2501.19393) | [GitHub](https://github.com/simplescaling/s1) | 2025 | EMNLP 2025 (arXiv 2501.19393) | test-time-scaling, budget-forcing, reasoning-distillation, small-data-sft |
| CLIFT: Conformal Self-Verification for Web Agent Training and Test-Time Scaling | [2610.06829](https://arxiv.org/abs/2610.06829) | / | 2026 | arXiv (preprint) | web-agent RL training, conformal self-verification, judge-free test-time scaling, trajectory selection |
| Cross-Rollout Bellman Closure for Long-Horizon Agentic Reinforcement Learning | [2609.35082](https://arxiv.org/abs/2609.35082) | / | 2026 | arXiv (preprint) | step-level credit assignment, multi-turn agentic RL, GRPO, Bellman closure |
| CUA-Sandbox: Efficient Environments for Computer-Use Agent Reinforcement Learning | [2609.32750](https://arxiv.org/abs/2609.32750) | [GitHub](https://github.com/windskyyx/Cua-Sandbox) | 2026 | arXiv (preprint) | environment-for-agent-RL, computer-use agent, sandbox runtime, RL rollout infrastructure |
| Explore More, Drift Less: Outcome-Only Reinforcement Learning Can Suffice for Long-Horizon Interactive Agents | [2609.01245](https://arxiv.org/abs/2609.01245) | [GitHub](https://github.com/AlibabaResearch/SignalCoverageRL) | 2026 | arXiv (preprint) | outcome-only agentic RL, long-horizon interactive agents, on-policy loop training, test-time interaction budget |
| From RLVR to RLSVR: Task Transformation Induces Self-Verifiable Rewards for Open-Ended LLM Self-Improvement | [2607.23802](https://arxiv.org/abs/2607.23802) | [GitHub](https://github.com/wangqinsi1/RLSVR) | 2026 | COLM 2026 | self-play RL environment, self-verifiable rewards, multi-agent harness, LLM self-improvement |
| HarnessBandit: Joint Learnability–Transferability Scheduling for Multi-Harness Agentic Reinforcement Learning | [2609.13739](https://arxiv.org/abs/2609.13739) | / | 2026 | arXiv (preprint) | harness-aware training, multi-harness scheduling, agentic RL / GRPO, agent-computer interface |
| OpenForgeRL: Train Harness-native Agents in Any Environment | [2607.21557](https://arxiv.org/abs/2607.21557) | [GitHub](https://github.com/MSR-Orchard/OpenForge-RL) | 2026 | arXiv (preprint) | harness-aware RL training, agent rollout orchestration, tool/GUI agents, training-in-the-harness |
| Scaling Verifiable Environments for Long-horizon Work Agents | [2610.04906](https://arxiv.org/abs/2610.04906) | / | 2026 | arXiv (preprint) | verifiable environments, agent RL post-training, long-horizon work agents, environment synthesis |
| SHARPO: Segment-Level Credit Assignment for Agentic Reinforcement Learning | [2610.00838](https://arxiv.org/abs/2610.00838) | / | 2026 | arXiv (preprint) | agentic RL, segment-level credit assignment, multi-turn agent training, self-distillation |
| T2SPO: Trajectory-to-Step Policy Optimization for Agentic Reinforcement Learning | [2610.00388](https://arxiv.org/abs/2610.00388) | / | 2026 | arXiv (preprint) | agentic RL, step-level credit assignment, multi-turn RL, trajectory-based reward shaping |
| ThunderSyncRL: Lossless Acceleration of Agentic Reinforcement Learning | [2610.05935](https://arxiv.org/abs/2610.05935) | [GitHub](https://github.com/seilk/thundersync) | 2026 | arXiv (preprint) | agentic RL training, harness-aware training, gradient streaming, actor-learner scheduling |
| ToolVerse: Unlocking Massive Environments and Long-Horizon Tasks for Agentic Reinforcement Learning | [2607.15660](https://arxiv.org/abs/2607.15660) | / | 2026 | arXiv (preprint) | environment-for-agent-RL, MCP agent-computer interface, long-horizon task synthesis, turn-level credit assignment |
| VACE: Validation-Gated Alternating Co-Evolution of Agent Models and Harnesses | [2609.37105](https://arxiv.org/abs/2609.37105) | / | 2026 | arXiv (preprint) | harness-aware training, agentic reinforcement learning, model-harness co-evolution, validation gating |
| WeEnv: The Environment for Agentic Reinforcement Learning at WeChat | [2609.30766](https://arxiv.org/abs/2609.30766) | / | 2026 | arXiv (preprint) | environment-for-agent-RL, agent-computer interface, RL training infrastructure, elastic provisioning |
| WEFT: Scaling Tool-Use Post-Training for General-Purpose Agents | [2609.36887](https://arxiv.org/abs/2609.36887) | / | 2026 | arXiv (preprint) | harness-aware training, tool-use post-training, self-evolution loop, agent runtime (MegaMCP) |

## Related Resources

- The two essays that set the industry's shared agent mental model: Anthropic [*Building Effective Agents*](https://www.anthropic.com/research/building-effective-agents) and OpenAI [*A Practical Guide to Building Agents*](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf).


---
## Verification Methodology

Every entry was multiply checked (last refreshed 2026-10-06):

- **Refresh pipeline (2026-07-01 → 2026-10-06 window, plus landmark pre-window misses)**: a 12-angle sweep (harness-core, agent-RL, tools/MCP, memory, multi-agent, SWE, web/GUI, benchmarks, surveys, production harnesses, essays/talks, orthogonal) surfaced ~250 candidates; each candidate passed an independent identity/date/qualification/duplicate verification, then an adversarial re-check tasked with **refuting** it (default-refute) across four axes — identity (page exists, title matches, ID re-derived from the page), date (v1 in window; pre-window items admitted only as landmark misses), qualification (harness/loop first-class), and duplicate (against the existing list). A final completeness critic re-swept the window and its finds were run through the same refute gate. Result: **103 additions** (88 papers, 8 production harnesses, 7 essays/talks); ~150 candidates were rejected along the way.

- **Influence bar for essays/blogs/talks (§2)** and **production repos (§1)**: entries must be major-lab/canonical-author work (Anthropic, OpenAI, Lilian Weng, Dan Luu, Latent Space tier) or show verified traction (HN front page with substantial points, confirmed via the Algolia API; or multi-thousand-star adoption for repos, confirmed via the GitHub API). Merely on-topic long-form posts and low-traction framework repos were excluded.

- **arXiv IDs**: all 86 new paper IDs added this round passed the 3-layer check (arXiv → CrossRef → Semantic Scholar) via `verify_papers.py` (verdict PASS, 0.0 hallucination rate), on top of the 112 previously verified.

- **GitHub links**: all 53 new repository URLs return HTTP 200 and were spot-checked for author correspondence; one stale link (SWE-Refactor-Bench) was corrected to the canonical `Einsia/SWE-Refactor-Bench` repo. Repos with no public code are marked `/`, not a gap.

- **Pre-window policy**: items dated 2026-01..06 were accepted only as landmark-grade misses — this round: OSWorld 2.0 (2606.29537) and Code as Agent Harness (2605.18747, HF #1 Paper of the Day). Other strong pre-window candidates (WildClawBench, the QA→Task-Completion survey) were deliberately held out.

- Definitions in *What is an agent harness?* are verbatim quotes, each with source + date + link.

If a link has rotted since, please open an issue/PR.

## Contributing

PRs welcome. A paper qualifies if the **harness or loop is a first-class contribution** (not merely an application that uses an agent). For tools, prefer widely-adopted harnesses or ones with a distinct harness/loop design. Submissions must include a verifiable arXiv ID or canonical URL — fabricated links will be rejected. See [CONTRIBUTING.md](./CONTRIBUTING.md).


## License
[MIT](./LICENSE).
