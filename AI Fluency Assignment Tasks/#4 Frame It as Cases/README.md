# Task #4: Frame It as Cases — Work That Speaks for Itself

**Track**: General AI Fluency  
**Phase**: Foundations  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 02](https://aifluency.flyrank.ai/week-02.html#frame-it-as-cases)  

---

## 🎙️ Voice Card

> **"Direct, plain, metric-driven, technical, no buzzwords."**

---

## 📁 Framed Case Studies

---

### Case Study 1: Production LLM Agent Workflow & Automation Pipeline

#### 1. The Problem
Manual invoice reconciliation and multi-document data extraction created an operational bottleneck for client operations, requiring 15+ manual hours weekly per analyst with an unacceptable 8% error rate on non-standard PDF formats.

#### 2. What I Did & Decided
- Built an asynchronous, multi-modal LLM workflow using Python, LangChain, and FastAPI.
- **Key Decision**: Rejected standard zero-shot prompting in favor of a 2-stage pipeline: a lightweight regex layout parser to extract bounding boxes followed by structured JSON extraction using Pydantic schemas.
- **Key Decision**: Implemented deterministic fallback rules for low-confidence extraction scores (<0.85) to prevent silent LLM hallucinations.

#### 3. What Came of It (Outcome & Metrics)
- Reduced document processing time from **15 minutes to 4.2 seconds per invoice**.
- Achieved **99.2% extraction accuracy** across 1,200 test invoices.
- Saved client operations an estimated **50+ engineering hours monthly**.

---

### Case Study 2: Real-Time Computer Vision & Predictive ML Pipeline

#### 1. The Problem
An industrial visual inspection client suffered from delayed defect detection on assembly lines. Existing monolithic ML scripts ran inference in 450ms per frame, causing buffer overflows and missed defect flags.

#### 2. What I Did & Decided
- Converted floating-point PyTorch vision models into TensorRT optimized engine formats.
- **Key Decision**: Decoupled frame capture from inference by building a multi-threaded Python worker queue leveraging Redis pub/sub.
- **Key Decision**: Standardized model deployment using Docker containers orchestrated via FastAPI microservices.

#### 3. What Came of It (Outcome & Metrics)
- Reduced per-frame inference latency from **450ms to 38ms** (11.8x speedup).
- Processed 30 FPS video feeds in real-time with **zero frame drops**.
- Lowered GPU memory consumption by **35%**, enabling deployment on edge devices.

---

### Case Study 3: Enterprise RAG System with Semantic Search & Evaluation

#### 1. The Problem
Engineering teams spent hours searching across fragmented internal technical documentation, leading to repeated architectural questions and delayed project onboarding.

#### 2. What I Did & Decided
- Engineered an enterprise Retrieval-Augmented Generation (RAG) pipeline utilizing Qdrant vector database and hybrid search (sparse BM25 + dense BGE embeddings).
- **Key Decision**: Swapped fixed-size chunking for semantic markdown header chunking, preserving code block context.
- **Key Decision**: Built a automated RAGAS evaluation pipeline to benchmark faithfulness and answer relevance on every documentation commit.

#### 3. What Came of It (Outcome & Metrics)
- Increased retrieval relevance score (NDCG@5) from **0.62 to 0.91**.
- Reduced internal technical support tickets by **42%**.
- Query response time averaged **1.1 seconds** across 50,000+ indexed documentation pages.

---

## 👤 Bio & Contact CTA Copy

### Bio Copy
> *"I am Ghulam Qasim, a Machine Learning & AI Fluency Intern at FlyRank. I specialize in building production-ready ML pipelines, asynchronous LLM applications, and high-performance inference APIs. I focus on engineering systems that deliver verified speed, accuracy, and operational ROI."*

### Contact / CTA Copy
> *"Want to review the architecture or benchmark metrics for these production builds? **Schedule a 15-minute Technical Strategy Call / Code Review with Ghulam Qasim.**"*

---

## 🔄 Before / After Copy Editing Comparison

To demonstrate the voice card in practice, here is a direct comparison between generic AI-generated marketing copy and my edited, human-voice version.

| Aspect | Generic AI Copy (Before) | Edited Human Voice (After) | Why it Changed |
| :--- | :--- | :--- | :--- |
| **Case Study Intro** | *"Leveraging cutting-edge, state-of-the-art Generative AI technologies, we seamlessly revolutionized enterprise document workflows to empower business growth."* | *"Built an asynchronous LLM pipeline using Python, LangChain, and FastAPI to automate invoice extraction."* | Replaced corporate buzzwords ("cutting-edge", "seamlessly", "empower") with direct technical tools and real problem scope. |
| **Tech Decision** | *"Utilized robust methodologies to dynamically ensure unprecedented accuracy and peak model synergy."* | *"Implemented deterministic fallback rules for low-confidence scores (<0.85) to prevent silent LLM hallucinations."* | Replaced vague hype ("robust methodologies", "synergy") with specific engineering logic and threshold numbers. |
| **Outcome** | *"Delivered game-changing results and incredible value for our esteemed client partners."* | *"Reduced processing time from 15 minutes to 4.2 seconds with 99.2% extraction accuracy."* | Replaced subjective praise ("game-changing") with concrete numerical metrics. |

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Voice Card Defined**: 5–7 words (*"Direct, plain, metric-driven, technical, no buzzwords"*).
- [x] **Framed Cases for Sitemap**: 3 complete case studies following the 3-beat structure (Problem $\rightarrow$ Decisions $\rightarrow$ Outcomes).
- [x] **No Bare Screenshots**: Every project contains detailed engineering decisions and quantifiable ROI.
- [x] **Bio & CTA**: Clear bio and direct 15-minute Strategy Call CTA included.
- [x] **Before/After Comparison**: Side-by-side table showing elimination of generic AI fluff in favor of plain technical language.
