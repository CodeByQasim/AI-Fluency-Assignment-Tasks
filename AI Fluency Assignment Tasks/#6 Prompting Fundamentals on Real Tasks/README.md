# Task #6: Prompting Fundamentals on Real Tasks v2 (FL-02)

**Track**: General AI Fluency  
**Phase**: Foundations  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 02](https://aifluency.flyrank.ai/week-02.html#prompting-fundamentals-v2)  

---

## 📌 Executive Summary

This assignment (FL-02) applies core Anthropic and OpenAI prompt engineering techniques to a real engineering task audited in **FL-01**: *Refactoring monolithic Machine Learning scripts into production-ready, asynchronous FastAPI microservices*. Starting from a naive 1-line prompt, 5 incremental techniques were applied, evaluated across **Claude 3.5 Sonnet** and **ChatGPT (GPT-4o)**, and distilled into a reusable template.

---

## 🛠️ The Real FL-01 Task Selected

- **Task Name**: Refactoring Python ML Training & Inference Scripts into Asynchronous Web Microservices.
- **FL-01 Category**: Code Refactoring & MLOps Pipeline Optimization.
- **Production Objective**: Convert synchronous PyTorch/scikit-learn inference calls into non-blocking FastAPI endpoints with Pydantic validation and `/healthz` liveness probes.

---

## 🧪 Prompt Iteration Log (6 Runs Total)

### Run 0: Naive Pre-Course Version (Naive Baseline)
- **Prompt**:
  ```text
  Convert my python machine learning script into an API.
  ```
- **Output Snippet**:
  ```python
  from flask import Flask, request
  app = Flask(__name__)
  @app.route('/predict', methods=['POST'])
  def predict():
      return "prediction"
  ```
- **Observed Output Limitation**: Used legacy synchronous Flask without type hints, schemas, error handling, or model loading lifecycle management.

---

### Run 1: Applying Technique 1 — Role Assignment (System Persona)
- **Prompt**:
  ```text
  You are an expert MLOps Engineer and Python Technical Architect specializing in high-performance FastAPI microservices. 
  Convert my python machine learning script into a production-ready API.
  ```
- **Observed Output Difference**:
  - The model switched from Flask to `FastAPI` and introduced basic Pydantic schemas.
  - The code included clean docstrings and typed function signatures.

---

### Run 2: Applying Technique 2 — Context & Motivation
- **Prompt**:
  ```text
  You are an expert MLOps Engineer and Python Technical Architect specializing in high-performance FastAPI microservices.
  
  CONTEXT & MOTIVATION:
  Our client operates an industrial visual inspection line processing 200 image feature vectors (128-float embeddings) per second. The existing monolithic script runs synchronously, causing thread blocking and frame drops. We need to deploy this as an asynchronous microservice inside a Kubernetes cluster where liveness probes check service health.
  
  Convert my python machine learning script into a production-ready API.
  ```
- **Observed Output Difference**:
  - Output added asynchronous route definitions (`async def`).
  - Added specific input array length validation (`min_items=128, max_items=128`) tailored to the 128-float embedding context.

---

### Run 3: Applying Technique 3 — Few-Shot Examples (In-Context Demonstration)
- **Prompt**:
  ```text
  You are an expert MLOps Engineer and Python Technical Architect specializing in high-performance FastAPI microservices.
  
  CONTEXT & MOTIVATION:
  Our client operates an industrial visual inspection line processing 200 image feature vectors (128-float embeddings) per second. The existing monolithic script runs synchronously, causing thread blocking and frame drops. We need to deploy this as an asynchronous microservice inside a Kubernetes cluster where liveness probes check service health.
  
  FEW-SHOT EXAMPLE OF EXPECTED SCHEMAS:
  ```python
  from pydantic import BaseModel, Field
  from typing import List

  class FeatureVectorInput(BaseModel):
      embedding: List[float] = Field(..., min_items=128, max_items=128, description="128-dim normalized vision vector")
  ```
  
  Convert my python machine learning script into a production-ready API following this schema pattern.
  ```
- **Observed Output Difference**:
  - Output perfectly adopted the Pydantic `Field` description formatting and schema structure demonstrated in the few-shot block.
  - Added complete field documentation strings to the openAPI schema output.

---

### Run 4: Applying Technique 4 — Output Structure & Formatting Rules
- **Prompt**:
  ```text
  [Role & Context from Run 3...]
  
  OUTPUT STRUCTURE RULES:
  Format your response into exactly 3 code sections using Markdown headers:
  ### Section 1: Pydantic Validation Schemas
  ### Section 2: Model Lifespan Context Manager
  ### Section 3: FastAPI Router & Health Endpoints
  
  Do not include introductory commentary outside the code blocks.
  ```
- **Observed Output Difference**:
  - Output eliminated conversational chat intro text ("Sure, here is your code...").
  - Organized code strictly into the 3 requested markdown sections.
  - Added a clean `asynccontextmanager` `lifespan` function for loading ML models on startup and clearing memory on shutdown.

---

### Run 5: Applying Technique 5 — Step Decomposition (Chain-of-Thought Reasoning)
- **Prompt**:
  ```text
  [Role, Context, Few-Shot, and Structure from Run 4...]
  
  STEP DECOMPOSITION INSTRUCTIONS:
  Before generating the Python code, analyze the architecture step-by-step inside <thinking> tags:
  1. Identify potential async bottlenecks in model execution.
  2. Plan exception handling for 503 (Model Uninitialized) and 500 (Inference Exception).
  3. Design the `/healthz` readiness probe logic.
  Then generate the final sectioned code.
  ```
- **Observed Output Difference**:
  - The model performed explicit architectural reasoning inside `<thinking>` tags prior to generating code.
  - The resulting code included robust 503 fallback handling for uninitialized models, structured JSON logging, and a complete `/healthz` probe.

---

## 📊 Cross-Model Comparison: Claude 3.5 Sonnet vs. ChatGPT (GPT-4o)

The final engineered prompt (Run 5) was executed on both **Claude 3.5 Sonnet** and **ChatGPT (GPT-4o)**.

| Criteria | Claude 3.5 Sonnet | ChatGPT (GPT-4o) | Comparative Analysis |
| :--- | :--- | :--- | :--- |
| **Tone & Style** | Direct, plain, zero conversational filler. Started immediately with `<thinking>` block. | Polished, friendly. Added introductory summary text despite formatting instructions. | **Claude 3.5 Sonnet** adhered strictly to the "no intro" constraint. |
| **Technical Accuracy** | Flawlessly implemented Pydantic array bounds (`min_items=128`) and typed return models. | Implemented Pydantic models but omitted explicit `min_items`/`max_items` until prompted. | **Claude 3.5 Sonnet** demonstrated higher validation fidelity. |
| **Error Handling** | Implemented 503 readiness check, 500 fallback, and structured JSON logs. | Implemented generic `HTTPException(500)` without 503 readiness separation. | **Claude 3.5 Sonnet** produced superior Kubernetes-ready code. |
| **Generation Speed** | ~3.8 seconds | ~2.1 seconds | **ChatGPT (GPT-4o)** was ~45% faster. |

*Detailed benchmark available in [`cross_model_comparison.md`](cross_model_comparison.md).*

---

## 🛠️ Universal Reusable Prompt Template

```text
[SYSTEM PERSONA]
You are a Senior [Domain Role, e.g., MLOps Engineer & FastAPI Architect] specializing in production-grade software engineering.

[CONTEXT & MOTIVATION]
Context: [Describe operational environment, e.g., Asynchronous microservice processing 128-float embeddings under 200 requests/sec traffic in Kubernetes].
Problem to Solve: [Describe current bottleneck, e.g., Refactoring synchronous ML script to eliminate thread blocking].

[FEW-SHOT SCHEMA EXAMPLE]
```python
# Provide 1-2 few-shot code snippet patterns showing exact desired style
```

[OUTPUT STRUCTURE]
Provide the final code split into the following sections:
1. Pydantic Input/Output Validation Schemas
2. Lifecycle & Application State Manager
3. API Router & Health Check Endpoints

[STEP DECOMPOSITION]
Before outputting code, analyze the architecture step-by-step inside <thinking> tags:
1. Identify performance & async bottlenecks.
2. Design HTTP error fallbacks (503 / 500).
3. Plan liveness/readiness probe logic.
```

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Real FL-01 Task**: Applied to Python ML script refactoring to FastAPI microservices.
- [x] **Five+ Iterations Beyond Naive**: 6 total runs (Baseline + 5 named techniques: Persona, Context, Few-Shot, Output Structure, Step Decomposition).
- [x] **Output-Focused Difference Notes**: Every iteration documents specific changes in the generated *output*.
- [x] **Specific Cross-Model Comparison**: Detailed comparison table evaluating Claude vs ChatGPT across 5 specific dimensions.
- [x] **Universal Reusable Template**: Generalized template provided for any engineering task.
