
# Research: Fault-Tolerant Agentic RAG Architecture

This document summarizes the technical research and architectural decisions behind the **SIETK AI Chatbot**. For the full academic context, please refer to the [Full Research Preprint (PDF)](./Research_Paper.pdf).

## 🎯 Objective

To eliminate hallucinations in institutional AI assistants by implementing a strictly bounded, two-stage **Agentic Retrieval-Augmented Generation (RAG)** pipeline.

## 🏗️ Technical Architecture

Our system moves away from traditional vector databases to prioritize speed, security, and institutional accuracy.

* **In-Memory Storage:** Uses a local, serialized TypeScript knowledge base (`all-info-knowledge-base.ts`) to achieve $O(1)$ retrieval speeds and eliminate external database injection risks.
* **Two-Stage Retrieval:**
1. **Stage 1 (Deterministic):** Case-insensitive keyword matching against local data.
2. **Stage 2 (Agentic):** A **Groq-powered (Llama 3.1)** analyzer expands queries or triggers a real-time web search via the **Exa AI API**.


* **Hybrid Generation:** Responses are synthesized by **Gemini 1.5 Flash**, with an automated fallback to **Groq** to ensure high availability.

## 📊 Performance Benchmarks

We evaluated the system against a 20-query institutional benchmark.

| Metric | Baseline LLM | SIETK AI (This Project) |
| --- | --- | --- |
| **Institutional Accuracy** | ~35% | **90%** |
| **Hallucination Rate** | High | **Near Zero** |
| **End-to-End Latency** | ~1.5s | **2.0 - 3.0s** |

## 🛠️ Tech Stack

* **LLMs:** Google Gemini 1.5 Flash, Groq (Llama 3.1 8B)
* **Real-Time Search:** Exa AI API
* **Frontend:** React, Next.js, Tailwind CSS, Shadcn UI
* **Backend:** TypeScript, Node.js

## 📝 Citation

If you use this architecture or reference our findings, please cite:

> **Ali, J. Mohammad.** "SIETK AI: A Fault-Tolerant Agentic RAG Architecture for High-Fidelity Institutional Retrieval." (2026).
