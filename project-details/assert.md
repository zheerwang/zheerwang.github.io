---
layout: zw-research-project
title: "ASSERT"
description: "Auditing Implicit Assumptions in LLM-Based Coding Outputs"
permalink: /project/assert/
nav: false
technologies: ["Python", "LLM Agents", "Evaluation", "Software Engineering"]
project_image: /assets/img/research/assert.svg
image_caption: "The multi-agent monitor decomposes coding outputs, extracts assumptions, merges duplicates, and verifies findings against the prompt and code."
resources: [{"label": "Paper \u00b7 Google Drive", "url": "https://drive.google.com/file/d/1kzcLP1b9BxH9c_u6_R2zVzLHwBN2Siad/view?usp=sharing"}, {"label": "Report \u00b7 PDF", "url": "/assets/pdf/research/assert-report.pdf", "local": true}]
# Optional: add github_url or demo_url when you have the real URLs.
---

## Overview

LLM coding agents often resolve incomplete requests by choosing defaults, data formats, persistence mechanisms, error-handling rules, and interface behavior. **ASSERT** audits these implicit implementation assumptions after code generation, making the decisions easier for developers to inspect.

Given an underspecified prompt and its generated solution, the framework produces structured findings with **assumption content, category, code evidence, and rationale**.

**Team:** En-Chao Liu, Ava Zheer Wang, and Binyue Deng · Georgia Institute of Technology.

## Research approach

We compared three monitoring strategies:

| Strategy | Approach |
| :--- | :--- |
| Inline self-reporting | The coding agent reports its assumptions while generating the solution. |
| External auditing | A separate model audits the complete prompt and generated output together. |
| Multi-agent monitoring | A four-stage pipeline decomposes the output, extracts assumptions, merges duplicates, and verifies findings. |

The multi-agent monitor includes prompt-overlap checks during extraction and verification to distinguish decisions made by the agent from requirements already stated by the user.

## Benchmark & evaluation

The benchmark contains **22 coding tasks across five domains**: backend APIs, frontend web, data processing, DevOps/infrastructure, and general coding. Two levels of prompt redaction produce **60 evaluation records**: 38 with selected constraints removed and 22 reduced to a minimal high-level goal.

Evaluation separates two questions: whether an extracted assumption correctly describes an unstated code decision, and whether it recovers a predefined missing requirement or discovers an additional valid decision.

| Monitor | Precision | Targeted recall | Discoveries |
| :--- | :--- | :--- | :--- |
| Inline | 73.8% | 19.9% | 159 |
| External | **93.7%** | **46.7%** | **500** |
| Multi-agent | 79.2% | 44.0% | 481 |

*Results from Table 2 of the final report. Targeted recall measures recovery of predefined golden assumptions; discoveries are valid assumptions outside that set. Evaluation used GPT-4.1 judges; human cross-validation remained future work.*

## Findings

- **Full-context auditing performed best on this benchmark.** Keeping the prompt and code together helped distinguish stated requirements from implicit choices.
- **Decomposition introduced an alignment trade-off.** Multi-agent monitoring extracted more assumptions per record, but its prompt-overlap rate was 17.1%, compared with 5.5% for the external auditor.
- **Refining the multi-agent prompts improved discovery.** Prompt-overlap checks and verifier changes reduced overlap from 20.3% to 17.1% and increased discoveries from 213 to 481 (+126%).
- **Discovery matters alongside recall.** Roughly 58% of correct findings were outside the predefined assumption sets, revealing design decisions the benchmark authors had not anticipated.

## My contributions

- Designed frontend and backend prompt categories and contributed to task construction.
- Contributed to experimental pipeline planning and multi-agent monitor design.
- Collaborated on system architecture, experimental setup, monitor comparisons, and evaluation design.

The project shows why reliable coding-agent evaluation requires checking both generated behavior and its alignment with the user's original instructions.
