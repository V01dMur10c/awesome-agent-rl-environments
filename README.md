# Awesome Agent RL Environments [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of **training and evaluation environments for LLM / VLM agents**, with a focus on the era of multi-turn reinforcement learning (post-DeepSeek-R1, post-GPT-5-thinking).

If you train, evaluate, or build LLM agents, you've probably noticed the **explosion of "Gym for Agents"-style projects in 2024–2026** — SWE-Gym, GEM, RAGEN, VAGEN, AgentGym, verifiers, SkyRL, ART, prime-rl, WebRL, OSWorld, AndroidWorld, AppWorld, TheAgentCompany… Each of them ships its own task suite, its own RL trainer, its own evaluation harness. This list is here to keep track.

**Scope.** We only include projects that satisfy at least one of:

1. Provide an **interactive environment** where an LLM/VLM agent issues actions, receives observations, and gets a reward / verifiable signal.
2. Are explicitly designed for **training** agents via RL (PPO, GRPO, RLOO, DPO-on-trajectories, etc.) — not just evaluation.
3. Are a **gym-style framework** that wraps multiple environments behind a unified API.

We intentionally **exclude** pure Atari / MuJoCo / classic RL benchmarks, and we exclude single-turn evaluation benchmarks (e.g., MMLU, GSM8K) — those are well-covered elsewhere.

**Every entry below has a verified GitHub link.** PRs that add a missing project, fix a broken link, or report a benchmark number are all appreciated. See [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## Contents

- [TL;DR — pick the right framework](#tldr--pick-the-right-framework)
- [General RL-for-LLM Gyms (cross-task frameworks)](#general-rl-for-llm-gyms-cross-task-frameworks)
- [Coding & Repository Environments](#coding--repository-environments)
- [Web / Browser Environments](#web--browser-environments)
- [Operating System / Desktop / Mobile Environments](#operating-system--desktop--mobile-environments)
- [Tool-Use & Multi-Tool Environments](#tool-use--multi-tool-environments)
- [Scientific & Research Environments](#scientific--research-environments)
- [Game & Simulation Environments](#game--simulation-environments)
- [Safety / Adversarial Environments](#safety--adversarial-environments)
- [Surveys & Related Reading](#surveys--related-reading)
- [How to Contribute](#how-to-contribute)

---

## TL;DR — pick the right framework

| Framework | Best for | RL algorithms | Native envs | Repo |
|-----------|----------|---------------|-------------|------|
| **GEM** | Math, code, QA, games — anything you want a gym-style API for | PPO, GRPO, RLOO | Math, Code, Reasoning, QA, Games | [axon-rl/gem](https://github.com/axon-rl/gem) |
| **RAGEN** | Multi-turn reasoning agents in stochastic envs | StarPO (custom) | Sokoban, FrozenLake, WebShop, Lean, Sudoku, …(10 envs) | [RAGEN-AI/RAGEN](https://github.com/RAGEN-AI/RAGEN) |
| **VAGEN** | Vision-Language-Model agents with world-model RL | PPO + World-Modeling RL | Visual multi-turn tasks | [RAGEN-AI/VAGEN](https://github.com/RAGEN-AI/VAGEN) |
| **AgentGym / -RL** | Broadest task coverage (14 envs across web, tools, games, embodied) | PPO, GRPO, RLOO, REINFORCE++ | 14 envs, 89 tasks | [WooooDyy/AgentGym-RL](https://github.com/WooooDyy/AgentGym-RL) |
| **verifiers** | Trainer-agnostic env wrappers + reward verifiers | bring your own (SkyRL, Tinker, …) | env registry growing on Environments Hub | [PrimeIntellect-ai/verifiers](https://github.com/PrimeIntellect-ai/verifiers) |
| **SkyRL** | Long-horizon, real-world agent training at scale | full-stack (train + tx + agent) | plugs into verifiers envs | [NovaSky-AI/SkyRL](https://github.com/NovaSky-AI/SkyRL) |
| **prime-rl** | End-to-end SFT + RL + evals with verifiers integration | PPO, GRPO | SWE & agentic envs | [PrimeIntellect-ai/prime-rl](https://github.com/PrimeIntellect-ai/prime-rl) |
| **OpenPipe ART** | Single-GPU GRPO with ergonomic Python harness | GRPO | bring your own task | [OpenPipe/ART](https://github.com/OpenPipe/ART) |
| **verl-agent** | Extending veRL for agentic RL with GiGPO | Group-in-Group PO | WebShop, ALFWorld, AppWorld, … | [langfengQ/verl-agent](https://github.com/langfengQ/verl-agent) |
| **SWE-Gym** | Specifically training SWE agents on real GitHub issues | any (PPO/GRPO/SFT) | 2,438 Python tasks | [SWE-Gym/SWE-Gym](https://github.com/SWE-Gym/SWE-Gym) |

---

## General RL-for-LLM Gyms (cross-task frameworks)

> Frameworks that wrap *many* environments behind a unified API, so you can train once and roll out everywhere.

- **[GEM: A Gym for Agentic LLMs](https://github.com/axon-rl/gem)** *(ICLR 2026)* — General Experience Maker for LLMs. OpenAI-Gym-style API spanning math, code, general reasoning, QA, and games (Mastermind, Minesweeper, Hangman, …). 📄 [Paper](https://arxiv.org/abs/2510.01051)

- **[RAGEN](https://github.com/RAGEN-AI/RAGEN)** — Reasoning AGENt. Built around **StarPO** (State-Thinking-Actions-Reward Policy Optimization). 10 built-in envs: Sokoban, FrozenLake, WebShop, DeepCoder, SearchQA, Lean, Bandit, Countdown, MetaMathQA, Sudoku.

- **[VAGEN](https://github.com/RAGEN-AI/VAGEN)** — RAGEN's sibling for **VLM agents**. Proposes World-Modeling RL: explicitly supervises a VLM's world-model reasoning during multi-turn rollouts.

- **[AgentGym](https://github.com/WooooDyy/AgentGym)** *(ACL 2025)* — 14 environments across web navigation, text games, household tasks, digital games, embodied tasks, tool use, programming. Real-time concurrent agent interaction.

- **[AgentGym-RL](https://github.com/WooooDyy/AgentGym-RL)** — Multi-turn RL training extension of AgentGym. Supports PPO, GRPO, RLOO, REINFORCE++. 📄 [Paper](https://arxiv.org/abs/2509.08755)

- **[verifiers](https://github.com/PrimeIntellect-ai/verifiers)** — Originally by [@willccbb](https://github.com/willccbb), now stewarded by Prime Intellect. Trainer-agnostic environment wrappers + reward verifier protocols. Supported as a backend by SkyRL and Tinker.

- **[SkyRL](https://github.com/NovaSky-AI/SkyRL)** *(NovaSky-AI)* — Full-stack modular RL library: `skyrl-train` (training framework), `skyrl-tx` (Tinker-API backend), `skyrl-agent` (long-horizon agent layer). 📄 [SkyRL-Agent paper](https://arxiv.org/abs/2511.16108)

- **[prime-rl](https://github.com/PrimeIntellect-ai/prime-rl)** — Agentic RL training at scale. End-to-end SFT + RL + evals with native verifiers integration.

- **[OpenPipe ART (Agent Reinforcement Trainer)](https://github.com/OpenPipe/ART)** — Ergonomic Python harness for GRPO on Qwen3, GPT-OSS, Llama, and more. Designed for maximum efficiency on a single GPU; builds on Unsloth.

- **[verl-agent](https://github.com/langfengQ/verl-agent)** — Extends veRL for LLM/VLM agent RL. Official code for **Group-in-Group Policy Optimization (GiGPO)**. Includes WebShop, ALFWorld, AppWorld, and other interactive envs.

- **[AgentLab](https://github.com/ServiceNow/AgentLab)** *(ServiceNow)* — Open-source framework for developing, testing, and benchmarking web agents on diverse tasks. Used together with BrowserGym.

---

## Coding & Repository Environments

> Environments where the agent edits real codebases, runs tests, and gets binary pass/fail rewards.

- **[SWE-Gym](https://github.com/SWE-Gym/SWE-Gym)** *(ICML 2025)* — The first public training environment combining real-world GitHub issues with pre-installed dependencies and executable unit tests. **2,438 Python tasks.** SWE-agents trained on SWE-Gym reach 32.0% on SWE-Bench Verified (open-weights SOTA at release). 📄 [Paper](https://arxiv.org/abs/2412.21139)

- **[R2E-Gym](https://github.com/R2E-Gym/R2E-Gym)** *(COLM 2025)* — Procedural environment generation + hybrid verifiers for scaling open-weights SWE agents. Removes the bottleneck of hand-curated tasks. 📄 [Paper](https://arxiv.org/abs/2504.07164)

- **[SWE-Bench](https://github.com/SWE-bench/SWE-bench)** — The original "can your agent fix a real GitHub issue?" benchmark; its Verified split (500 human-validated tasks) is the de-facto standard. 📄 [Paper](https://arxiv.org/abs/2310.06770)

- **[Multi-SWE-Bench](https://github.com/multi-swe-bench/multi-swe-bench)** *(NeurIPS 2025 D&B)* — SWE-Bench across **7 languages** (Java, TypeScript, JavaScript, Go, Rust, C, C++). 1,632 expert-annotated instances. 📄 [Paper](https://arxiv.org/abs/2504.02605)

- **[SWE-Bench-Live](https://github.com/microsoft/SWE-bench-Live)** *(NeurIPS 2025 D&B, Microsoft)* — Continuously updated SWE-Bench. 1,319 tasks from real GitHub issues since 2024 across 93 repos; refreshed monthly via the RepoLaunch pipeline to prevent contamination. 📄 [Paper](https://arxiv.org/abs/2505.23419)

- **[SWE-rebench](https://nebius.com/blog/posts/introducing-swe-rebench)** *(Nebius)* — Continuously updated decontaminated SWE benchmark; **21,000+ Python tasks** suitable for RL of SWE agents. 📄 [Paper](https://arxiv.org/abs/2505.20411)

- **[SWE-Bench Pro](https://github.com/scaleapi/SWE-bench_Pro-os)** *(Scale AI)* — Enterprise-grade long-horizon tasks: 1,865 problems from 41 actively maintained repos. Top models score ~23% (vs. ~70% on Verified). 📄 [Paper](https://arxiv.org/abs/2509.16941)

---

## Web / Browser Environments

> Self-hosted realistic websites where agents must navigate, click, type, and complete multi-step tasks.

- **[WebArena](https://github.com/web-arena-x/webarena)** — The original realistic, reproducible web environment. Self-hosted instances of GitLab, Shopping, Reddit, Map, WikiCFM. 📄 [Paper](https://arxiv.org/abs/2307.13854)

- **[VisualWebArena](https://github.com/web-arena-x/visualwebarena)** — Multimodal extension: 910 visual web tasks over Classifieds, Shopping, Reddit. 📄 [Paper](https://arxiv.org/abs/2401.13649)

- **[BrowserGym](https://github.com/ServiceNow/BrowserGym)** *(ServiceNow)* — Unified Gym wrapper for WebArena, VisualWebArena, MiniWoB++, AssistantBench, and WorkArena. The de-facto standard for plugging your web agent into many envs at once.

- **[WebArena-Verified](https://github.com/ServiceNow/webarena-verified)** *(ServiceNow)* — Verified, version-controlled WebArena tasks with deterministic evaluators. Reproducible benchmarking.

- **[Mind2Web](https://github.com/OSU-NLP-Group/Mind2Web)** *(NeurIPS 2023 Spotlight)* — First generalist web-agent dataset/benchmark; later spawned Mind2Web 2 and Mind2Web Live for execution-based evaluation.

- **[WebRL](https://github.com/THUDM/WebRL)** *(THUDM)* — Self-evolving online curriculum RL for web agents. Llama-3.1-70B trained with WebRL hits **49.1% on WebArena-Lite**, beating GPT-4-Turbo (17.6%). 📄 [Paper](https://arxiv.org/abs/2411.02337)

- **[AssistantBench](https://github.com/oriyor/assistantbench)** — 214 realistic, time-consuming web tasks ("which gyms near me have classes on weekends before 7AM?"). State-of-the-art agents at release scored near zero. 📄 [Paper](https://arxiv.org/abs/2407.15711)

- **[WorkArena](https://github.com/ServiceNow/WorkArena)** *(ServiceNow)* — Enterprise SaaS workflows on the ServiceNow platform; **WorkArena-L1** has 19,912 instances of 33 atomic tasks; **WorkArena++** adds 682 compositional tasks.

- **[ClawBench](https://github.com/reacher-z/ClawBench)** *(arXiv 2026)* — Containerized live-web environment with 153 write-heavy tasks, final-request interception, and trace-grounded binary evaluation for browser agents. 📄 [Paper](https://arxiv.org/abs/2604.08523)

---

## Operating System / Desktop / Mobile Environments

> The agent controls a real OS (Ubuntu, Windows, macOS, Android) and must operate apps the way humans do.

- **[OSWorld](https://github.com/xlang-ai/OSWorld)** *(NeurIPS 2024)* — First-of-its-kind scalable real-computer environment. 369 desktop tasks across Ubuntu/Windows/macOS spanning file I/O, multi-app workflows, OS settings. Humans 72.4% vs. best agent ~12.2% at release. 📄 [Paper](https://arxiv.org/abs/2404.07972)

- **[AndroidWorld](https://github.com/google-research/android_world)** *(Google Research, ICLR 2025)* — Dynamic Android benchmark: 116 hand-crafted tasks across 20 apps, parameterized into millions of variations. Best agent at release ~30.6%. 📄 [Paper](https://arxiv.org/abs/2405.14573)

- **[Windows Agent Arena](https://github.com/microsoft/WindowsAgentArena)** *(Microsoft)* — 150+ Windows-specific tasks adapted from OSWorld. Real Windows OS with the full app ecosystem.

- **[Agent-S](https://github.com/simular-ai/Agent-S)** *(Simular AI)* — Open agentic framework that "uses computers like a human." Strong reference for production-style computer-use stacks.

---

## Tool-Use & Multi-Tool Environments

> Agents call external APIs / tools and chain them together. Reward is usually a verifier checking the final state or output.

- **[ToolBench](https://github.com/OpenBMB/ToolBench)** *(ICLR 2024 Spotlight, OpenBMB)* — 16,000+ real-world APIs over 3,451 tools. Both training data and evaluation harness; the canonical tool-learning corpus.

- **[AppWorld](https://github.com/StonyBrookNLP/appworld)** *(ACL 2024 Best Resource, Stony Brook NLP)* — Controllable simulated world of 9 apps (Amazon, Spotify, …) + 457 APIs + 100 simulated users. **750 day-to-day agent tasks.** First-class MCP support.

- **[τ-bench](https://github.com/sierra-research/tau-bench)** *(Sierra)* — Tool-Agent-User interaction in airline and retail customer-service domains. Measures **consistency** (success rate across 8 repeated runs), not just one-shot.

- **[τ²-bench](https://github.com/sierra-research/tau2-bench)** *(Sierra)* — Updated τ-bench with a banking domain, voice evaluation modality, and fixes to airline / retail tasks. Current recommended version.

- **[ToolSandbox](https://github.com/apple/ToolSandbox)** *(Apple)* — Stateful, conversational, interactive tool-use eval. Implicit state dependencies between tools + on-policy user simulator + dynamic milestone evaluation. 📄 [Paper](https://arxiv.org/abs/2408.04682)

- **[MINT-Bench](https://github.com/xingyaoww/mint-bench)** *(ICLR 2024)* — Multi-turn interaction with **tools + natural-language feedback**. 586 representative instances repurposed from 8 datasets across reasoning, code, decision-making. 📄 [Paper](https://arxiv.org/abs/2309.10691)

- **[AgentBoard](https://github.com/hkust-nlp/AgentBoard)** *(NeurIPS 2024 Oral, HKUST-NLP)* — Analytical evaluation board: 9 tasks, 1,013 environments. Fine-grained progress / sub-skill / trajectory inspection beyond final success rate.

- **[TheAgentCompany](https://github.com/TheAgentCompany/TheAgentCompany)** *(CMU)* — Self-contained simulated software company (internal sites, data, employees). Best agent ~30% on consequential business tasks. 📄 [Paper](https://arxiv.org/abs/2412.14161)

---

## Scientific & Research Environments

> Long-horizon tasks where the agent has to reason over papers, run experiments, and produce science-grade output.

- **[ScienceWorld](https://github.com/allenai/ScienceWorld)** *(Allen AI)* — Classic text-based science-experiment env: 10 interconnected locations, ~200 simulated lab objects. Still a tractable testbed for tool use + reasoning.

- **[DiscoveryWorld](https://github.com/allenai/discoveryworld)** *(Allen AI)* — Virtual environment for developing and evaluating automated scientific-discovery agents. Successor in spirit to ScienceWorld for the agent era. 📄 [Paper](https://arxiv.org/abs/2406.06769)

- **[AI Scientist-v2](https://github.com/SakanaAI/AI-Scientist-v2)** *(Sakana AI)* — Workshop-level automated scientific discovery via agentic tree search. Produced the **first fully AI-generated paper to pass workshop peer review** (ICLR 2025). 📄 [Paper](https://arxiv.org/abs/2504.08066)

- **[CodeScientist](https://github.com/allenai/codescientist)** *(Allen AI)* — Automated scientific discovery system for code-based experiments. End-to-end pipeline from hypothesis to executed experiment.

- **[MLE-Bench](https://github.com/openai/mle-bench)** *(ICLR 2025, OpenAI)* — 75 Kaggle-style ML engineering competitions with human Kaggle leaderboards as baselines. The standard ML-engineer agent benchmark. 📄 [Paper](https://arxiv.org/abs/2410.07095)

- **[PaperBench](https://github.com/openai/preparedness)** *(ICML 2025, OpenAI)* — Replicate **20 ICML 2024 Spotlight/Oral papers from scratch**, evaluated by 8,316 author-validated rubric sub-tasks. Best agent at release ~21%. 📄 [Paper](https://arxiv.org/abs/2504.01848)

- **[ResearcherBench](https://github.com/GAIR-NLP/ResearcherBench)** *(GAIR-NLP)* — 65 expert-curated frontier AI research questions across 35 subjects; dual rubric + factual evaluation for Deep Research systems. 📄 [Paper](https://arxiv.org/abs/2507.16280)

- **[DRBench](https://github.com/ServiceNow/drbench)** *(ServiceNow)* — Realistic enterprise deep-research benchmark.

- **[LiveResearchBench](https://github.com/SalesforceAIResearch/LiveResearchBench)** *(Salesforce AI Research)* — Live benchmark for open-ended deep research "in the wild."

- **[DeepResearch Bench](https://github.com/Ayanami0730/deep_research_bench)** — Comprehensive benchmark for deep-research agents.

---

## Game & Simulation Environments

> Constrained, verifier-friendly games used as RL playgrounds for LLMs. Several cross-task gyms above (notably **GEM** and **RAGEN**) also bundle game environments — see [General RL-for-LLM Gyms](#general-rl-for-llm-gyms-cross-task-frameworks).

- **[TextWorld](https://github.com/microsoft/TextWorld)** *(Microsoft)* — Sandbox text-game environment with controllable generation; still widely used to probe curriculum learning, generalization, and transfer in LLM agents. 📄 [Paper](https://arxiv.org/abs/1806.11532)

- **[ALFWorld](https://github.com/alfworld/alfworld)** — Aligns text-based TextWorld policies with the visual ALFRED benchmark. Standard baseline for embodied / household agents. 📄 [Paper](https://arxiv.org/abs/2010.03768)

- **[Crafter](https://github.com/danijar/crafter)** *(Danijar Hafner)* — Minecraft-inspired 2D open-world survival benchmark. Gym API; popular as a tractable open-ended task in LLM-agent papers.

---

## Safety / Adversarial Environments

> Environments specifically built to stress-test agent safety, prompt injection, and reward hacking.

- **[AgentDojo](https://github.com/ethz-spylab/agentdojo)** *(NeurIPS 2024, ETH Zürich SPyLab)* — Dynamic environment to evaluate prompt-injection attacks and defenses for tool-using LLM agents. Used by US/UK AI Safety Institutes to stress-test Claude. 📄 [Paper](https://arxiv.org/abs/2406.13352)

- **[InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent)** *(ACL 2024 Findings, UIUC)* — Benchmark for indirect prompt injection via tool outputs. 1,054 test cases / 17 user tools / 62 attacker tools. 📄 [Paper](https://arxiv.org/abs/2403.02691)

- **[ST-WebAgentBench](https://github.com/segev-shlomov/ST-WebAgentBench)** — Safety + trustworthiness for web agents. 222 tasks paired with 646 policy instances across 6 ST dimensions (consent, boundary, hierarchy, robustness, error handling). 📄 [Paper](https://arxiv.org/abs/2410.06703)

- **[ToolEmu](https://github.com/ryoungj/ToolEmu)** *(ICLR 2024 Spotlight)* — LM-based emulation of tool execution with an automatic safety evaluator. 36 toolkits / 311 tools / 144 test cases. Originally framed as a **risk-identification** sandbox that lets you stress-test agent failures without real APIs.

---

## Surveys & Related Reading

- 📄 [Evaluation and Benchmarking of LLM Agents: A Survey](https://arxiv.org/abs/2507.21504) — Comprehensive 2025 survey of the entire agent benchmark / environment landscape.
- 📝 [A Taxonomy of RL Environments for LLM Agents](https://leehanchung.github.io/blogs/2026/03/21/rl-environments-for-llm-agents/) — Practitioner-oriented map.
- ⭐ [Awesome-Agent-RL](https://github.com/0russwest0/Awesome-Agent-RL) — Sister list focused on *methods* (RL papers) rather than *environments*. Complementary to this list.

---

## How to Contribute

We love PRs. To keep quality high, please:

1. **One project per PR.** Smaller diffs review faster.
2. **Verify the GitHub link works** before submitting — every entry in this list has a confirmed, live repo.
3. **Use this row format** in the appropriate section:
   ```
   - **[Project Name](https://github.com/org/repo)** *(Venue Year, if any)* — One-sentence description that says what's distinctive. 📄 [Paper](https://arxiv.org/abs/XXXX)
   ```
4. **No closed, paywalled, or unavailable resources** unless they are uniquely important.
5. **No generic LLM frameworks** that aren't *environments* for agents.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for full guidelines. Open an issue with the label `suggest-env` if you're unsure whether something fits.

---

## License

[CC0 1.0](./LICENSE) — Public domain. Use it any way you like.

## Star History

If this list saves you time, please ⭐ the repo. It's the cheapest way to say thanks and helps others find it.
