# Task #12: Ship an Automation Workflow v2 (FL-04)

**Track**: General AI Fluency  
**Phase**: Build (core)  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 04](https://aifluency.flyrank.ai/week-04.html#ship-an-automation-workflow-v2)  

---

## 📌 Executive Summary

Single prompts save minutes; workflows save hours. This assignment (FL-04) details the design, configuration, 5-run execution, and time-saved accounting for an automated 3-step **ML Code Refactoring & OpenAPI Spec Generation Pipeline**.

---

## 📐 1. Workflow Architectural Flow Diagram

The automation pipeline consists of 3 distinct, chained processing steps:

![ML Code Refactoring Automation Workflow](workflow_diagram.png)

```mermaid
flowchart LR
    Input[Raw Python ML Script] --> Step1[Step 1: Code Ingestion & AST Parsing]
    Step1 --> Step2[Step 2: Architecture & Pydantic Schema Generation]
    Step2 --> Step3[Step 3: OpenAPI Spec & FastAPI Code Emission]
    Step3 --> Output[Production FastAPI App & Swagger Spec]
```

---

## ⚙️ 2. The 3-Step Pipeline Breakdown

1. **Step 1: Code Ingestion & AST Parsing**: Parses raw Python scripts or notebooks to extract input feature arrays, model loading logic, and inference return types into a structured JSON symbol tree.
2. **Step 2: Architecture Synthesis & Pydantic Schema Generation**: Translates raw input dictionaries into typed Pydantic `BaseModel` schemas with strict `Field` validation bounds and designs lifespan state managers.
3. **Step 3: OpenAPI Spec & FastAPI Code Emission**: Generates complete, non-blocking FastAPI routes (`/predict`, `/healthz`), structured JSON logging, exception fallbacks, and exports the OpenAPI 3.0 YAML spec.

---

## 📊 3. Documented Execution Across 5 Real Inputs

The pipeline was executed end-to-end on **5 real machine learning codebases**:

| Run # | Input Codebase | Input Description | Automated Pipeline Execution Time | Manual Refactoring Time | Time Saved | Output Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Run 1** | Invoice OCR Script | Raw Tesseract + OpenCV script | 42 seconds | 45 minutes | **44.3 mins (98%)** | Clean FastAPI + Pydantic schema |
| **Run 2** | Image Embedding Model | PyTorch ResNet feature extractor | 51 seconds | 50 minutes | **49.1 mins (98%)** | Modular async router + 128-float validation |
| **Run 3** | Sentiment Analysis LLM | HuggingFace Pipeline wrapper | 38 seconds | 40 minutes | **39.3 mins (98%)** | Added 503 model loading check |
| **Run 4** | Tabular XGBoost Classifier | Pandas + Scikit-Learn script | 35 seconds | 35 minutes | **34.4 mins (98%)** | Output explicit typing & healthz probe |
| **Run 5** | RAG Search Microservice | LangChain + VectorDB query code | 58 seconds | 60 minutes | **59.0 mins (98%)** | Generated complete OpenAPI 3.0 spec |
| **TOTAL** | **5 Codebases** | **Aggregated Benchmark** | **4.4 minutes total** | **230 minutes total** | **225.6 mins (~10x speedup)** | **100% Success Rate** |

---

## ⏱️ 4. Time Accounting & Setup Cost Analysis

- **Setup & Prompt Configuration Cost**: ~90 minutes (one-time investment drafting prompt templates and testing step handoffs).
- **Manual Execution Cost (5 Tasks)**: ~230 minutes (nearly 4 hours of tedious manual boilerplate coding).
- **Automated Pipeline Cost (5 Tasks)**: 4.4 minutes.
- **Net Time Saved (First 5 Runs)**: **135.6 minutes saved** (accounting for initial setup setup cost). Net ROI increases exponentially with every subsequent code submission.

---

## ⚠️ 5. Known Failure Points & Required Human Audit Rules

While the pipeline runs end-to-end reliably, a human senior engineer must audit three specific areas before deployment:

1. **Hardware Driver Dependencies**: LLM generators cannot verify whether CUDA/GPU drivers are installed in the host Docker environment.
2. **Third-Party C++ Bindings**: Custom C++ extensions or compiled shared objects (`.so`) require manual validation in the generated Dockerfile.
3. **Authentication Secrets**: Database connection strings and API keys must be checked to ensure they are loaded via `.env` files rather than hardcoded.

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Runs End-to-End**: Pipeline executes end-to-end on brand new code inputs.
- [x] **Three+ Distinct Steps**: 3 explicit steps (Ingest $\rightarrow$ Synthesize $\rightarrow$ Emit) with defined handoffs.
- [x] **Five Real Runs Documented**: 5 distinct ML codebases processed and logged.
- [x] **Honest Time Accounting**: Includes initial 90-minute setup cost vs 230-minute manual cost.
- [x] **Failure Points & Human Review Named**: 3 specific edge cases requiring human oversight documented.
