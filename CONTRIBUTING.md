# Contributing to Awesome Agent RL Environments

Thanks for considering a contribution! This list lives or dies by community PRs.

## What belongs here

A project belongs in this list if it satisfies at least one of:

1. Provides an **interactive environment** where an LLM/VLM agent issues actions, receives observations, and gets a reward / verifiable signal.
2. Is explicitly designed for **training** agents via RL (PPO, GRPO, RLOO, DPO-on-trajectories, etc.).
3. Is a **gym-style framework** that wraps multiple environments behind a unified API.

## What does NOT belong here

- Pure Atari / MuJoCo / classic RL benchmarks.
- Single-turn evaluation benchmarks (MMLU, GSM8K, etc.).
- Generic LLM training libraries with no environment component.
- Closed-source products without a research artifact (paper / open repo / benchmark).
- Pure data-only resources (datasets that don't ship with an executable env).

## How to add a project

1. **Fork & branch** off `main`.
2. Add ONE project per PR.
3. Use this exact row format inside the appropriate section:
   ```
   - **[Project Name](https://github.com/org/repo)** *(Venue Year, if any)* — One-sentence description that says what's distinctive. 📄 [Paper](https://arxiv.org/abs/XXXX)
   ```
4. **Verify**:
   - the GitHub link resolves;
   - the paper link resolves;
   - the description is accurate at the date you submit (cite a release or commit if needed);
   - the project isn't a duplicate of an existing entry.
5. Open the PR with a title `Add: <Project Name>`.

## How to report a broken / dead project

Open an issue with the label `broken-link` and include:
- the entry's name and section
- what's broken (link 404, repo archived, paper retracted, etc.)
- whether you suggest removing or replacing it

## How to suggest a new section

For new categories (e.g., "Multi-agent collaboration environments"), open an issue with the label `new-section` and at least **three** candidate projects. Sections with <3 entries get folded into a parent category.

## Style notes

- Keep descriptions to **one sentence**. Detailed analysis goes in the linked paper.
- Use the exact venue name and year if accepted: `(NeurIPS 2025)`, `(ICLR 2026)`, `(COLM 2025)`. For preprints, omit the parenthetical or write `(arXiv 2025)`.
- Use markdown links, not raw URLs.
- Match capitalization to the project's own README.

## Review SLA

We aim to review PRs within 7 days. If a PR sits longer, ping with a `@<maintainer>` comment.

## Code of Conduct

Be kind. Critique the entry, not the contributor.
