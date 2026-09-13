# Task #5: The Prompt Ladder — Systematic Prompt Engineering

**Track**: General AI Fluency  
**Phase**: Foundations  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 02](https://aifluency.flyrank.ai/week-02.html#the-prompt-ladder)  

---

## 📌 Executive Summary

The gap between a lazy prompt and an engineered one is the cheapest performance upgrade in AI. This assignment demonstrates the disciplined **Prompt Ladder**: starting with an embarrassing single-line baseline, adding **exactly one layer per iteration**, evaluating side-by-side output differences, and documenting both improvements and regressions.

---

## 🪜 The 6-Run Prompt Ladder Summary

| Run | Added Layer | Core Prompt Change | Primary Output Improvement | Identified Regression / Failure |
| :--- | :--- | :--- | :--- | :--- |
| **V0** | *Baseline* | `"Write python code for a machine learning model."` | Raw training script output | Completely unsuited for web serving or production |
| **V1** | **Clearer Goal** | Defined task: Asynchronous FastAPI microservice | Output shifted to FastAPI route handlers | Missing schemas & error handling |
| **V2** | **Defined Audience** | Persona: Senior MLOps Engineers | Added Pydantic `BaseModel` & HTTP errors | Model loaded globally without lifespan hooks |
| **V3** | **Real Context** | Context: 128-float embeddings @ 200 req/sec | Added length validation to arrays | **⚠️ Regression**: Added unused imports (`async_timeout`) cluttering code |
| **V4** | **Specified Output Format** | Structured 3-section layout + type hints | Clean lifespan context manager & typed models | Missing health check & logging |
| **V5** | **Constraints & Quality Criteria** | Added `/healthz` probe, JSON logging & fallback | Added 503 probes, JSON logs & zero global exceptions | Production-ready |

---

## 📋 Full Prompt Iterations & 4-Note Evaluations

### Version 0: Embarrassing Baseline
- **Prompt**: `"Write python code for a machine learning model."`
- **Output**: Generic 10-line scikit-learn script printing accuracy on a local CSV file.

---

### Version 1: Adding Layer 1 — Clearer Goal
- **Prompt**: `"Write python code to build an asynchronous FastAPI microservice that loads a trained Machine Learning model and serves real-time inference requests."`
- **Notes**:
  - *Prompt Change*: Added specific architectural goal.
  - *Output Improvement*: Switched from offline training script to an asynchronous web route (`@app.post("/predict")`).
  - *What Failed*: Input payload lacked schema validation.
  - *Next Step*: Add a target audience layer to enforce code quality.

---

### Version 2: Adding Layer 2 — Defined Audience
- **Prompt**: `"Write python code to build an asynchronous FastAPI microservice that loads a trained Machine Learning model and serves real-time inference requests. Target Audience: Senior MLOps Engineers who expect production-ready code with input validation and clean architecture."`
- **Notes**:
  - *Prompt Change*: Specified senior engineer persona.
  - *Output Improvement*: Introduced Pydantic `BaseModel` for payload parsing and HTTP exception handling.
  - *What Failed*: Model loading was executed top-level rather than inside context lifecycle managers.
  - *Next Step*: Inject real context regarding hardware environment and feature bounds.

---

### Version 3: Adding Layer 3 — Real Context
- **Prompt**: `"Write python code to build an asynchronous FastAPI microservice that loads a trained Machine Learning model and serves real-time inference requests. Target Audience: Senior MLOps Engineers who expect production-ready code with input validation and clean architecture. Real Context: The service processes computer vision feature vectors (128-float embeddings) under high traffic (200 requests/sec) in a Dockerized environment."`
- **Notes**:
  - *Prompt Change*: Added embedding dimensions, RPS traffic, and Docker deployment context.
  - *Output Improvement*: Added array length validation (`min_items=128, max_items=128`).
  - *⚠️ Honest Regression*: **Adding high-traffic context caused the AI to import unused libraries (`async_timeout`), adding unwanted dependency bloat without adding actual batch processing.**
  - *Next Step*: Specify explicit output format to clean up structure.

---

### Version 4: Adding Layer 4 — Specified Output Format
- **Prompt**: `"Write python code to build an asynchronous FastAPI microservice that loads a trained Machine Learning model and serves real-time inference requests. Target Audience: Senior MLOps Engineers who expect production-ready code with input validation and clean architecture. Real Context: The service processes computer vision feature vectors (128-float embeddings) under high traffic (200 requests/sec) in a Dockerized environment. Specified Output Format: Provide clean Python code split into 3 distinct sections: 1. Pydantic Schemas, 2. Lifespan Model Manager, 3. Router Endpoints. Include type hints for all parameters and return values."`
- **Notes**:
  - *Prompt Change*: Enforced a 3-part layout with explicit type annotations.
  - *Output Improvement*: Cleaned up unused imports, implemented FastAPI `lifespan` manager, and added `response_model` bindings.
  - *What Failed*: Lacked health check endpoints and structured logging.
  - *Next Step*: Add constraints for liveness probes and logging format.

---

### Version 5: Adding Layer 5 — Constraints & Quality Criteria
- **Prompt**: `"Write python code to build an asynchronous FastAPI microservice that loads a trained Machine Learning model and serves real-time inference requests. Target Audience: Senior MLOps Engineers who expect production-ready code with input validation and clean architecture. Real Context: The service processes computer vision feature vectors (128-float embeddings) under high traffic (200 requests/sec) in a Dockerized environment. Specified Output Format: Provide clean Python code split into 3 distinct sections: 1. Pydantic Schemas, 2. Lifespan Model Manager, 3. Router Endpoints. Include type hints for all parameters and return values. Constraints & Quality Criteria: Include a /healthz liveness probe endpoint, structured JSON logging, zero unhandled global exceptions, and zero third-party dependencies outside FastAPI, Pydantic, and NumPy."`
- **Notes**:
  - *Prompt Change*: Enforced `/healthz` probe, JSON logging, and dependency boundaries.
  - *Output Improvement*: Output included a complete Kubernetes-compliant `/healthz` route, 503 fallback handling, JSON logging, and clean try/except blocks.
  - *What Failed*: None—the code is modular, fully typed, production-ready, and error-resilient.
  - *Next Step*: Distill into a universal reusable template.

---

## 🛠️ Final Reusable Engineered Prompt Template

```text
[GOAL]
Build a production-grade [Framework / Language, e.g., asynchronous FastAPI microservice in Python] that [Primary Purpose, e.g., serves real-time machine learning inference requests].

[AUDIENCE]
Target Audience: Senior MLOps & Software Engineers who require strict type safety, input validation, and production error resilience.

[CONTEXT]
Environment: [Operating Context, e.g., Dockerized microservice processing 128-float embeddings under 200 requests/sec traffic load].

[OUTPUT FORMAT]
Structure the output into 3 distinct sections:
1. Pydantic Input/Output Validation Schemas
2. Application Lifecycle & Model State Manager (lifespan context manager)
3. API Router Endpoints with explicit type hints and response_model bindings.

[CONSTRAINTS & QUALITY CRITERIA]
- Include a Kubernetes-compliant `/healthz` liveness/readiness probe.
- Implement structured JSON logging (`time`, `level`, `message`).
- Include explicit HTTP exception handling (503 for uninitialized model, 500 for inference failures).
- Do NOT include unused imports or external dependencies outside [Allowed Dependencies, e.g., FastAPI, Pydantic, NumPy].
```

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Six Total Runs**: Baseline (V0) plus 5 incremental versions.
- [x] **One Layer Per Version**: Each version added exactly one named layer (Goal, Audience, Context, Format, Constraints).
- [x] **Output-Focused Notes**: All 4 notes per iteration describe changes in the *output*, not just the prompt.
- [x] **Honest Regression Moment**: V3 documented an unwanted library import regression (`async_timeout`).
- [x] **Final Reusable Prompt**: Final template is generalized so any engineer can apply it.
