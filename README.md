# Enterprise Compliance & Legal Audit Agent (Agentic RAG)

An enterprise-grade, asynchronous AI compliance auditing system that analyzes commercial contracts against legal frameworks and internal company policies using Hybrid Retrieval-Augmented Generation (Dense + Sparse BM25) and Multi-Stage LLM Reasoning.

---

## System Architecture

[Client / API Request]
│ (JSON Clauses)
▼
[FastAPI Asynchronous Gateway] ─── (Background Worker)
│
▼
[Hybrid RAG Engine]
├── Dense Vector Retrieval (Qdrant + MiniLM-L6-v2)
├── Sparse Keyword Retrieval (BM25Okapi)
└── Reciprocal Rank Fusion (RRF Ranking)
│
▼ (Retrieved Legal Context)
[Compliance Auditor Agent]
├── Automated Model Fallback & Exponential Backoff (Fault Tolerance)
└── Pydantic Structured Output Enforcement
│
▼
[Audit Report Output] (Risk Score 1-10, Violations, Actionable Remediations)

---

## Key Engineering Features

- **Hybrid Retrieval (Dense + BM25):** Combines semantic vector search with keyword matching via Reciprocal Rank Fusion (RRF) to eliminate missing domain-specific clauses.
- **Asynchronous Execution:** Non-blocking job processing via FastAPI background tasks, responding immediately with tracking Job IDs.
- **Enterprise Reliability & Fault Tolerance:** Implements exponential backoff retry and dynamic model fallback for resilient high-demand handling.
- **Strict Structured Outputs:** 100% type-safe JSON contracts using Pydantic schema validation.
- **Automated Evaluation Benchmark:** Built-in quantitative testing pipeline measuring Retrieval Precision and Reasoning Accuracy against golden datasets.

---

## Benchmark & Evaluation Results

Evaluated against the Golden Compliance Test Suite:

| Metric | Result | Target Benchmark |
|---|---|---|
| **Hybrid Retrieval Precision (Top-2)** | **100.0%** | > 85% |
| **Compliance Reasoning Accuracy** | **100.0%** | > 90% |
| **Schema Validation Success Rate** | **100.0%** | 100% |

---

## Tech Stack

- **Core & API:** Python 3.11+, FastAPI, Uvicorn, Pydantic v2
- **Vector Storage:** Qdrant (Docker Container)
- **Retrieval & NLP:** Sentence-Transformers (`all-MiniLM-L6-v2`), Rank-BM25
- **LLM Engine:** Google GenAI SDK (Gemini 2.5 Flash / Pro Fallbacks)
- **DevOps:** Docker, Docker Compose

---

## Quickstart

1.Start Qdrant Vector DB:
   docker compose up -d

2.Install Dependencies:
pip install -r requirements.txt

3.Run Automated Evaluation Benchmark
python -m tests.eval_benchmark

4.Start the Production API
uvicorn app.main:app --reload --port 8000
Interactive API documentation available at `http://localhost:8000/docs`.
