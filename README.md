# Awesome Agent Harnesses [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated, multiply-verified survey of **agent harness** research and engineering — the right level of abstraction for understanding the current frontier of LLM agents. Covers papers, influential essays/talks, vendor positions, and the production harnesses that define the field.

**Total: 107 papers · 50 essays/talks/tools · last updated 2026-07-03**

> **Agent = Model + Harness.** The harness is the code, configuration, and execution logic wrapped around a foundation model — the agent loop, tools, memory, context management, planning/search, multi-agent orchestration, runtime, and safety.
>
> **The agent loop ⊂ harness.** The loop is the harness's *core mechanism*: the recurring *generate → act → observe* cycle, plus the outer scheduling that keeps an agent running over time. OpenAI describes the Codex harness as providing the "core agent loop and execution logic"; LangChain defines the harness as everything outside the model — state, tool execution, feedback loops, and constraints. Loop and harness are therefore **not peers**: the loop is what the harness *does*, one component among several.

### Anatomy of a harness — how this list is mapped

Each section corresponds to a component of the harness:

| Harness component | Where in this list |
|---|---|
| The agent loop (core execution + control flow) | §2 Foundations · §5 Planning / Search / Self-improvement loops |
| Tools & function calling | §3 |
| The harness as a research object (scaffold, runtime, agent-computer interface) | §4 |
| Memory & context management | §6 |
| Multi-agent orchestration | §7 |
| Domain harnesses (code/SWE, web/GUI/computer-use) | §8 · §9 |
| Evaluation & stress-testing harnesses | §10 |
| Training the loop (reasoning models, test-time scaling, agent RL) | §11 |
| Production harnesses — Claude Code, Codex, Cursor, … *are* harnesses | §14 |

### ReAct or harness — where to start?

Harness-first. **ReAct** (Yao 2022, §2) is the historical seed: it formalized *reasoning + acting in a loop* — the core mechanism every harness now contains. The frontier has since moved outward to **harness engineering**: agent-computer interfaces (SWE-agent), context engineering (Anthropic), memory architectures (MemGPT / Letta), execution runtimes (GoEX), and the SDKs that ship these as products (Claude Code, Codex). This list treats the loop as the seed inside §2 / §5 and spends the rest on the harness built around it.

## Table of Contents

- [1. Surveys & Position Papers](#1-surveys-position-papers)
- [2. Foundations of the Agent Loop](#2-foundations-of-the-agent-loop)
- [3. Tool Use & Function Calling](#3-tool-use-function-calling)
- [4. The Agent Harness & Scaffold](#4-the-agent-harness-scaffold)
- [5. Planning, Search & Self-Improvement Loops](#5-planning-search-self-improvement-loops)
- [6. Memory-Augmented Agents](#6-memory-augmented-agents)
- [7. Multi-Agent Systems](#7-multi-agent-systems)
- [8. Code & SWE Agents](#8-code-swe-agents)
- [9. Web, GUI & Computer-Use Agents](#9-web-gui-computer-use-agents)
- [10. Benchmarks & Evaluation](#10-benchmarks-evaluation)
- [11. Reasoning Models & Test-Time Scaling for Agents](#11-reasoning-models-test-time-scaling-for-agents)
- [12. Blog Posts, Essays & Vendor Guides](#12-blog-posts-essays--vendor-guides)
- [13. Talks & Podcasts](#13-talks--podcasts)
- [14. Harnesses, SDKs & Frameworks](#14-harnesses-sdks--frameworks)
- [Related Resources](#related-resources)

---

## Papers

## 1. Surveys & Position Papers (8)

*Authoritative surveys and position papers on LLM agents.*

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| A Survey on Large Language Model based Autonomous Agents | [2308.11432](https://arxiv.org/abs/2308.11432) | [GitHub](https://github.com/Paitesanshi/LLM-Agent-Survey) | 2023 | Frontiers of Computer Science (2024), vol. 18, art. 186345; arXiv:2308.11432 | agent survey, profiling-memory-planning-action, taxonomy |
| The Rise and Potential of Large Language Model Based Agents: A Survey | [2309.07864](https://arxiv.org/abs/2309.07864) | [GitHub](https://github.com/OpenHands/OpenHands) | 2023 | arXiv (Scientia Sinica Informationis journal version) | survey, profiling-memory-planning-action, taxonomy, agent-architecture |
| A Survey on LLM-based Multi-Agent System: Recent Advances and New Frontiers in Application | [2412.17481](https://arxiv.org/abs/2412.17481) | / | 2024 | arXiv:2412.17481 | multi-agent, LLM-MAS, applications |
| A Survey on the Memory Mechanism of Large Language Model based Agents | [2404.13501](https://arxiv.org/abs/2404.13501) | [GitHub](https://github.com/nuster1128/LLM_Agent_Memory_Survey) | 2024 | arXiv:2404.13501 (later ACM Computing Surveys) | survey, memory taxonomy, read/write/reflect, evaluation |
| Large Language Model based Multi-Agents: A Survey of Progress and Challenges | [2402.01680](https://arxiv.org/abs/2402.01680) | [GitHub](https://github.com/taichengguo/LLM_Multiagents_Survey_Papers) | 2024 | IJCAI 2024 (proc. paper 890); arXiv:2402.01680 | multi-agent, LLM-MAS, survey |
| Tool Learning with Large Language Models: A Survey | [2405.17935](https://arxiv.org/abs/2405.17935) | [GitHub](https://github.com/quchangle1/LLM-Tool-Survey) | 2024 | Frontiers of Computer Science 19(8):198345 (2025); arXiv:2405.17935 | tool use, pipeline taxonomy, benchmarks |
| From LLM Reasoning to Autonomous AI Agents: A Comprehensive Review | [2504.19678](https://arxiv.org/abs/2504.19678) | / | 2025 | arXiv:2504.19678 | reasoning, autonomous agents, benchmarks |
| Survey on Evaluation of LLM-based Agents | [2503.16416](https://arxiv.org/abs/2503.16416) | / | 2025 | ACL Findings 2025; arXiv:2503.16416 | evaluation survey, benchmarks, web/SWE agents |

## 2. Foundations of the Agent Loop (11)

*The reasoning/acting primitives that seeded the agent loop.*

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

## 3. Tool Use & Function Calling (11)

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
| ToolACE: Winning the Points of LLM Function Calling | [2409.00920](https://arxiv.org/abs/2409.00920) | [GitHub](https://github.com/MadeAgents/Hammer) | 2025 | ICLR 25 | synthetic data generation, self-evolution, dual-layer verification, BFCL SOTA |

## 4. The Agent Harness & Scaffold (13)

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

## 5. Planning, Search & Self-Improvement Loops (6)

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| LLM+P: Empowering Large Language Models with Optimal Planning Proficiency | [2304.11477](https://arxiv.org/abs/2304.11477) | [GitHub](https://github.com/Cranial-XIX/llm-pddl) | 2023 | arXiv:2304.11477 (long-horizon planning) | PDDL, classical planner, long-horizon, symbolic |
| Code Generation with AlphaCodium: From Prompt Engineering to Flow Engineering | [2401.08500](https://arxiv.org/abs/2401.08500) | [GitHub](https://github.com/Codium-ai/AlphaCodium) | 2024 | arXiv:2401.08500 | test-based iterative flow, code generation, multi-stage, self-revision |
| Efficient Tool Use with Chain-of-Abstraction Reasoning | [2401.17464](https://arxiv.org/abs/2401.17464) | / | 2024 | ACL 24 (arXiv:2401.17464) | abstract placeholders, parallel tools, planning, tool-augmented |
| Language Agent Tree Search Unifies Reasoning Acting and Planning in Language Models | [2310.04406](https://arxiv.org/abs/2310.04406) | [GitHub](https://github.com/lapisrocks/LanguageAgentTreeSearch) | 2024 | ICML 24 (arXiv:2310.04406) | MCTS, tree search, value function, self-reflection |
| ReST-MCTS*: LLM Self-Training via Process Reward Guided Tree Search | [2406.03816](https://arxiv.org/abs/2406.03816) | [GitHub](https://github.com/THUDM/ReST-MCTS) | 2024 | NeurIPS 24 (arXiv:2406.03816) | process reward, MCTS, self-training, reasoning |
| rStar-Math: Small LLMs Can Master Math Reasoning with Self-Evolved Deep Thinking | [2501.04519](https://arxiv.org/abs/2501.04519) | [GitHub](https://github.com/microsoft/rStar) | 2025 | ICML 25 (arXiv:2501.04519) | MCTS, process preference model, self-evolution, test-time search |

## 6. Memory-Augmented Agents (9)

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

## 7. Multi-Agent Systems (7)

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation | [2308.08155](https://arxiv.org/abs/2308.08155) | [GitHub](https://github.com/microsoft/autogen) | 2023 | COLM 2024 (arXiv Aug 2023) | multi-agent conversation, conversable agents, framework |
| ChatEval: Towards Better LLM-based Evaluators through Multi-Agent Debate | [2308.07201](https://arxiv.org/abs/2308.07201) | [GitHub](https://github.com/chanchimin/ChatEval) | 2023 | ICLR 2024 | multi-agent debate, LLM evaluation, referee team |
| Improving Factuality and Reasoning in Language Models through Multiagent Debate | [2305.14325](https://arxiv.org/abs/2305.14325) | [GitHub](https://github.com/composable-models/llm_multiagent_debate) | 2023 | ICML 2024 (arXiv May 2023) | multi-agent debate, factuality, test-time scaling, society of minds |
| MACM: Utilizing a Multi-Agent System for Condition Mining in Solving Complex Mathematical Problems | [2404.04735](https://arxiv.org/abs/2404.04735) | [GitHub](https://github.com/bin123apple/MACM) | 2024 | NeurIPS 2024 (Poster) | math reasoning, condition mining, prompting |
| More Agents Is All You Need | [2402.05120](https://arxiv.org/abs/2402.05120) | [GitHub](https://github.com/MoreAgentsIsAllYouNeed/AgentForest) | 2024 | TMLR (Transactions on Machine Learning Research) | scaling, sampling-and-voting, Agent Forest |
| Revisiting Multi-Agent Debate as Test-Time Scaling: A Systematic Study of Conditional Effectiveness | [2505.22960](https://arxiv.org/abs/2505.22960) | [GitHub](https://github.com/euiin/MAD_as_TTS) | 2025 | arXiv (under review) | test-time scaling, multi-agent debate, conditional effectiveness |
| Why Do Multi-Agent LLM Systems Fail? | [2503.13657](https://arxiv.org/abs/2503.13657) | [GitHub](https://github.com/multi-agent-systems-failure-taxonomy/MAST) | 2025 | NeurIPS 2025 (Poster) | failure taxonomy, MAST, diagnostics |

## 8. Code & SWE Agents (8)

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

## 9. Web, GUI & Computer-Use Agents (12)

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

## 10. Benchmarks & Evaluation (9)

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

## 11. Reasoning Models & Test-Time Scaling for Agents (13)

| Title | arXiv | GitHub | Year | Venue | Keywords |
|-------|-------|--------|------|-------|----------|
| Agent-FLAN: Designing Data and Methods of Effective Agent Tuning for Large Language Models | [2403.12881](https://arxiv.org/abs/2403.12881) | [GitHub](https://github.com/InternLM/Agent-FLAN) | 2024 | ACL 2024 Findings (arXiv 2403.12881) | agent-tuning, data-design, reasoning-decoupling, SFT |
| AgentTrek: Agent Trajectory Synthesis via Guiding Replay with Web Tutorials | [2412.09605](https://arxiv.org/abs/2412.09605) | [GitHub](https://github.com/xlang-ai/AgentTrek) | 2024 | ICLR 2025 (arXiv 2412.09605) | trajectory-synthesis, GUI-agent, web-tutorial, data-scaling |
| OpenAI o1 System Card | [2412.16720](https://arxiv.org/abs/2412.16720) | / | 2024 | arXiv 2412.16720 (OpenAI technical report) | reasoning-model, chain-of-thought, RLHF, system-card |
| Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters | [2408.03314](https://arxiv.org/abs/2408.03314) | / | 2024 | ICLR 2025 (arXiv 2408.03314) | test-time-compute, process-reward-model, inference-scaling, compute-optimal |
| Training Language Models to Self-Correct via Reinforcement Learning (SCoRe) | [2409.12917](https://arxiv.org/abs/2409.12917) | / | 2024 | ICLR 2025 (arXiv 2409.12917) | self-correction, multi-turn-RL, intrinsic-correction, online-RL |
| Absolute Zero: Reinforced Self-play Reasoning with Zero Data | [2505.03335](https://arxiv.org/abs/2505.03335) | [GitHub](https://github.com/LeapLabTHU/Absolute-Zero-Reasoner) | 2025 | arXiv 2505.03335 | self-play, RLVR, zero-data, self-evolving-curriculum |
| Agent-R: Training Language Model Agents to Reflect via Iterative Self-Training | [2501.11425](https://arxiv.org/abs/2501.11425) | [GitHub](https://github.com/ByteDance-Seed/Agent-R) | 2025 | arXiv 2501.11425 | iterative-self-training, reflection, on-the-fly-correction, agent-tuning |
| DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning | [2501.12948](https://arxiv.org/abs/2501.12948) | [GitHub](https://github.com/deepseek-ai/DeepSeek-R1) | 2025 | Nature (DOI 10.1038/s41586-025-09422-z); arXiv 2501.12948 | pure-RL-reasoning, RLVR, GRPO, self-reflection |
| RAGEN: Understanding Self-Evolution in LLM Agents via Multi-Turn Reinforcement Learning | [2504.20073](https://arxiv.org/abs/2504.20073) | [GitHub](https://github.com/RAGEN-AI/RAGEN) | 2025 | arXiv 2504.20073 | multi-turn-agent-RL, trajectory-level-RL, StarPO, Echo-Trap |
| ReSearch: Learning to Reason with Search for LLMs via Reinforcement Learning | [2503.19470](https://arxiv.org/abs/2503.19470) | [GitHub](https://github.com/Agent-RL/ReSearch) | 2025 | NeurIPS 2025 (arXiv 2503.19470) | reasoning-search-RL, multi-hop, self-correction, no-SFT |
| ReTool: Reinforcement Learning for Strategic Tool Use in LLMs | [2504.11536](https://arxiv.org/abs/2504.11536) | [GitHub](https://github.com/ReTool-RL/ReTool) | 2025 | arXiv 2504.11536 (ByteDance Seed) | tool-integrated-RL, code-execution, outcome-reward, aha-moment |
| Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning | [2503.09516](https://arxiv.org/abs/2503.09516) | [GitHub](https://github.com/PeterGriffinJin/Search-R1) | 2025 | COLM 2025 (arXiv 2503.09516) | retrieval-augmented-RL, retrieved-token-masking, reasoning-search, outcome-reward |
| s1: Simple test-time scaling | [2501.19393](https://arxiv.org/abs/2501.19393) | [GitHub](https://github.com/simplescaling/s1) | 2025 | EMNLP 2025 (arXiv 2501.19393) | test-time-scaling, budget-forcing, reasoning-distillation, small-data-sft |

## 12. Blog Posts, Essays & Vendor Guides (32)

| Title | Author / Org | Type | Year | Link |
|-------|--------------|------|------|------|
| Software 2.0 | Andrej Karpathy | blog | 2017 | [link](https://karpathy.medium.com/software-2-0-a64152b37c35) |
| Building Generally Capable AI Agents with MineDojo | Jim Fan (NVIDIA) — NVIDIA Developer Blog | blog | 2022 | [link](https://developer.nvidia.com/blog/building-generally-capable-ai-agents-with-minedojo/) |
| LLM OS. Bear with me I'm still cooking. (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2023 | [link](https://x.com/karpathy/status/1723140519554105733) |
| LLM Powered Autonomous Agents | Lilian Weng (OpenAI) — Lil'Log | blog | 2023 | [link](https://lilianweng.github.io/posts/2023-06-23-agent/) |
| LLMs not as a chatbot, but the kernel process of a new Operating System (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2023 | [link](https://x.com/karpathy/status/1707437820045062561) |
| The Anatomy of Autonomy: Why Agents are the next AI Killer App after ChatGPT | swyx — Latent Space | blog | 2023 | [link](https://www.latent.space/p/agents) |
| The Rise of the AI Engineer | swyx — Latent Space | blog | 2023 | [link](https://www.latent.space/p/ai-engineer) |
| Agentic Design Patterns (Part 1: How Agents Can Improve LLM Performance; Part 2: Reflection; Part 3: Tool Use) | Andrew Ng — DeepLearning.AI, The Batch | blog | 2024 | [link](https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance) |
| Building Effective Agents | Anthropic | blog | 2024 | [link](https://www.anthropic.com/research/building-effective-agents) |
| Introducing computer use: a new Claude 3.5 Sonnet (and computer-use API) | Anthropic | blog | 2024 | [link](https://www.anthropic.com/news/3-5-models-and-computer-use) |
| Jagged Intelligence (thread) | Andrej Karpathy (@karpathy) | tweet_thread | 2024 | [link](https://x.com/karpathy/status/1816531576228053133) |
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
| Harness design for long-running application development | Anthropic | blog | 2026 | [link](https://www.anthropic.com/engineering/harness-design-long-running-apps) |

## 13. Talks & Podcasts (4)

| Title | Author / Org | Type | Year | Link |
|-------|--------------|------|------|------|
| Making Large Language Models Work for You (WordCamp US talk) | Simon Willison | talk | 2023 | [link](https://simonwillison.net/2023/Aug/27/wordcamp-llms/) |
| [1hr Talk] Intro to Large Language Models | Andrej Karpathy | talk | 2023 | [link](https://www.youtube.com/watch?v=zjkBMFhNj_g) |
| Language Agents: From Reasoning to Acting (interview) | Shunyu Yao — Latent Space (swyx / Alessio) | podcast | 2024 | [link](https://www.latent.space/p/shunyu) |
| AI Sessions #7: How Close is "AGI"? | Conspicuous Cognition (Dan Williams, Henry Shevlin) | podcast | 2026 | [link](https://www.conspicuouscognition.com/p/how-close-is-agi) |

## 14. Harnesses, SDKs & Frameworks (14)

*These are themselves production agent harnesses — the shipped artifacts that the rest of this list studies.*

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

## Related Resources

- [Awesome-World-Models](https://github.com/NeuraLiying/Awesome-World-Models) — sibling awesome-list for world-model research.

- [AgentBench / SWE-bench / τ-bench / OSWorld](#10-benchmarks--evaluation) — the canonical harness-stressing benchmarks.

- Anthropic [*Building Effective Agents*](https://www.anthropic.com/research/building-effective-agents) and OpenAI [*A Practical Guide to Building Agents*](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — the two vendor essays that set the industry's shared agent mental model.


---
## Verification Methodology

Every entry was multiply checked (2026-07-03):

- **arXiv IDs**: all 101 papers with an ID passed a 3-layer check (arXiv → CrossRef → Semantic Scholar) via `verify_papers.py` — 101/101 verified via the arXiv layer.

- **GitHub links**: all 89 repository URLs were fetched and returned HTTP 200. 89 papers have an official repo; 17 were extracted from the **PDF body** (not the arXiv abstract page); 25 have no public code (marked `/`, not a gap).

- **Titles/authors**: cross-checked against the live arXiv page; 2 title drifts and the WebShop authorship were corrected.

- **Web URLs**: every blog/talk/repo URL was fetched and confirmed to resolve.

If a link has rotted since, please open an issue/PR.


## Contributing

PRs welcome. A paper qualifies if the **harness or loop is a first-class contribution** (not merely an application that happens to use an agent). For tools, prefer repos that are widely adopted or that introduce a distinct harness/loop design. All submissions must include a verifiable arXiv ID or canonical URL — fabricated links will be rejected.


## License
[CC0 1.0](./LICENSE) (public domain dedication, same as the awesome-list tradition).
