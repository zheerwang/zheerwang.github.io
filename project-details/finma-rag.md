---
layout: zw-research-project
title: "FinMA-RAG"
description: "Agentic Retrieval & Reasoning for Financial Reports"
permalink: /project/finma-rag/
nav: false
technologies: ["Python", "LangGraph", "FAISS", "BM25", "ColBERT-v2", "RAG"]
project_image: /assets/img/research/finma-rag.svg
image_caption: "Structure-aware ingestion, hybrid retrieval, reranking, and agent reasoning support financial QA."
resources: [{"label": "Poster \u00b7 PDF", "url": "/assets/pdf/research/finma-rag-poster.pdf", "local": true}, {"label": "Paper \u00b7 PDF", "url": "/assets/pdf/research/finma-rag-paper.pdf", "local": true}]
# Optional: add github_url or demo_url when you have the real URLs.
---

## Overview

Financial question answering requires more than finding a relevant paragraph. A system must recover tables, identify the right fiscal period and line item, extract numerical inputs, and perform the correct calculation.

**FinMA-RAG** combines retrieval-augmented generation with specialized agents to answer questions over SEC 10-K and 10-Q filings. The workflow separates evidence retrieval, financial interpretation, deterministic arithmetic, and final answer synthesis.

**Team:** Ava (Zheer) Wang, Ruishu Cao, Minghao Zheng, and Devansh Khunteta · Georgia Institute of Technology.

## System design

**Document ingestion.** The pipeline uses PyMuPDF4LLM to preserve document structure and financial tables in Markdown. The poster describes ingestion from **369 PDFs**, followed by Markdown-aware chunking and embedding.

**Query rewriting and retrieval.** An LLM query rewriter adds relevant financial terminology and fiscal-year context. Hybrid search combines BM25 with FAISS dense retrieval, and ColBERT-v2 reranks candidate evidence before it reaches the reasoning stage.

**Agent orchestration.** LangGraph coordinates four components:

| Component | Responsibility |
| :--- | :--- |
| Retriever | Refine the query and locate relevant financial evidence. |
| Analyst | Identify line items, fiscal years, and numerical inputs. |
| Calculator | Execute financial arithmetic through deterministic tools. |
| Synthesis | Combine the evidence and computed values into a final answer. |

Iterative verification and recomputation help the workflow revisit intermediate reasoning. Tool-based calculation reduces reliance on the language model for arithmetic, while correct evidence selection and interpretation remain essential.

## Evaluation & results

The project evaluated **150 FinanceBench financial QA questions**, with GPT-4o-mini judging final answers as correct or incorrect. Logs included retrieved context, intermediate agent outputs, tool calls, final answers, and latency.

Embedding selection had a substantial effect on retrieval:

| Embedding model | Recall@5 | MRR |
| :--- | :--- | :--- |
| BGE-base-en-v1.5 | 0.53 | 0.31 |
| BGE-large-en-v1.5 | 0.59 | 0.35 |
| E5-large-v2 | **0.76** | **0.54** |

| End-to-end system | FinanceBench judged accuracy |
| :--- | :--- |
| Vanilla RAG | 19.3% |
| FinMA-RAG | **44.0%** |

The final result represents a **24.7 percentage-point increase**, or approximately **2.3×** the vanilla RAG accuracy.

## My contributions

- Built structure-aware ingestion and table-preserving chunking.
- Developed hybrid retrieval, query rewriting, and ColBERT-v2 reranking.
- Orchestrated retrieval, analysis, calculation, and synthesis with LangGraph.
- Evaluated embedding choices, retrieval quality, and downstream answer accuracy.

## Findings & limitations

Preserving tables recovered evidence that naive parsing could miss. Stronger embeddings improved recall, while hybrid retrieval and reranking improved the order and relevance of the context passed to the agents.

Remaining challenges include mixed-format chunking, redundant chunks, combining sparse and dense retrieval effectively, and the limited diversity of a single embedding index. The reported accuracy reflects LLM-judged results on the evaluated question set.

## Paper & poster

The **poster** presents the FinMA-RAG architecture and experiments. The accompanying **paper**, *Retrieval-Augmented Generation: Architecture, Evaluation, and Future Directions*, is the team's broader RAG survey, covering architecture, evaluation, RAG versus fine-tuning, applications, and open challenges.
