# FL-06: Design Your Personal Agent

**Assignment Code:** FL-06  
**Track:** General AI Fluency  
**Phase:** Build  
**Author:** Ghulam Qasim — FlyRank Machine Learning & AI Fluency Intern  
**Submitted:** September 2026  

---

## Agent Name: ML Study Coach

---

## 1. Job To Be Done

**One-line job:** When I encounter an ML concept, paper, or technique I don't fully understand, the agent explains it in plain terms, connects it to my existing knowledge, quizzes me to test retention, and tells me where the gap is.

**Why this job matters to me:**  
As an ML intern I read code, papers, and documentation daily. I often hit walls — a term in a paper I half-understand, or a technique I can name but can't explain. The typical fix is to Google, fall into a rabbit hole, and lose 45 minutes. This agent replaces that rabbit hole with a focused 10-minute tutoring session in my own context.

**Usage frequency:** 4–6 times per week, during or after study/work sessions.

---

## 2. The User (Me) and Usage Pattern

| Field | Detail |
| :--- | :--- |
| **User** | Ghulam Qasim, ML & AI Fluency Intern at FlyRank |
| **Background** | Comfortable with Python, familiar with basic ML concepts (regression, classification, neural nets at high level), learning transformers and LLM tooling |
| **Pain point** | Reading papers or docs and hitting terms I half-know — wasting time on unfocused Googling |
| **Usage trigger** | "I just read something I don't fully get" — pastes the concept/snippet |
| **Session length** | 10–15 minutes, ends when I can explain it back |
| **Frequency** | 4–6× per week |

---

## 3. Tools and Data Needed

| Tool / Data Source | Why Needed | Access Plan |
| :--- | :--- | :--- |
| **Knowledge Base: FlyRank Assignment Files** | Gives the agent context about my current learning level, my projects, my proof statement | Upload all 14 README.md files to the Claude Project as files |
| **Knowledge Base: My own notes** | Agent knows what I already understand vs. what is new | Upload a `my-knowledge-baseline.md` file (written once, updated monthly) |
| **File search (Claude Projects built-in)** | Agent retrieves relevant context from my uploaded files when explaining | Built into Claude Projects — no extra setup |
| **Web search (optional, later phase)** | For retrieving live paper abstracts | Not in MVP scope — add in Phase 2 if needed |

**Access plan summary:** Everything runs inside a Claude Project on the free Claude.ai tier. Files are uploaded once as the knowledge base. No API keys, no external services, no cost.

---

## 4. Draft Instructions (System Prompt)

```
You are ML Study Coach, a personal AI tutor for Ghulam Qasim, an ML & AI Fluency Intern at FlyRank.

YOUR JOB:
When Qasim pastes a concept, term, paper excerpt, or code snippet he doesn't understand, you:
1. Explain it in plain, concrete terms — no jargon without definition
2. Give one real-world example that connects to ML work he's likely doing
3. Check his current understanding by asking one targeted question
4. Quiz him: give him 2–3 short questions to test retention
5. After his answers, tell him exactly what he got right, what the gap is, and what to read next (one source, not five)

YOUR KNOWLEDGE OF QASIM:
Use the uploaded project files to understand his current level, his projects, and his internship work. Always connect new concepts to things he has already done or built.

RULES:
- Never explain more than ONE concept per session — depth over breadth
- Never give more than one "read next" link — choice paralysis kills learning
- If he says "I get it now", run one final quiz question to confirm before ending
- Do not explain generic concepts he clearly already knows (Python basics, what a for-loop is)
- Keep explanations under 200 words before quizzing — don't lecture, teach

TONE: Direct, like a sharp senior engineer explaining to a smart junior. No padding. No "great question!"
```

---

## 5. Five Evaluation Cases

These are written BEFORE building, to define what "working" looks like.

| # | Input I Give | Expected Agent Behavior | Pass Condition |
| :--- | :--- | :--- | :--- |
| **Eval 1** | "What is attention in transformers? I keep reading about it but I don't really get what it's computing." | Explains query/key/value in plain words with a concrete analogy. Asks one check question. Gives a quiz. | Explanation is correct, uses analogy, quiz questions test understanding not recall |
| **Eval 2** | "What's the difference between fine-tuning and RAG? When do I pick one over the other?" | Explains both approaches, gives a decision rule I can actually use, connects to my FlyRank ML context | Agent uses my project context from uploaded files to personalize the answer |
| **Eval 3** | "I don't understand this line of code: `loss = criterion(outputs, labels.squeeze())`" | Explains what `criterion`, `outputs`, and `labels.squeeze()` each do and why squeeze is needed. Quizzes. | Correct explanation; quiz actually tests the squeeze concept specifically |
| **Eval 4** | "What is RLHF?" | Plain explanation + real example + quiz. Does NOT give 5 links or a 500-word essay. | Response under 250 words, ends with a quiz, one "read next" resource |
| **Eval 5** | I deliberately answer a quiz question wrong | Agent catches the wrong answer, explains the gap precisely, does NOT just say "almost!" | Agent identifies the specific misconception and corrects it with a targeted 2-3 sentence explanation |

---

## 6. Risks and Guardrails

| Risk | Guardrail |
| :--- | :--- |
| **Agent over-explains** (walls of text → I stop reading) | System prompt enforces < 200 words before quizzing |
| **Agent tells me I'm right when I'm wrong** | Eval case 5 tests this explicitly; quiz answer validation is a core requirement |
| **Scope creep: I ask it to write code** | Agent must redirect: "I'm your study coach, not your code writer. Want me to explain how this works instead?" |
| **Agent gives 5 "read next" links** (choice paralysis) | Hard rule in system prompt: one link only |
| **Uploading sensitive data** | Knowledge base = only my own README files and notes — no private company data, no credentials |
| **Agent skips the quiz step** | Eval cases 1–4 all require a quiz — if agent skips, I revise the instructions to make quiz mandatory |

---

## 7. Platform Choice and Justification

**Chosen platform:** Claude Project (Claude.ai free tier)

| Platform | Cost | Tool connections | Eval against my use case |
| :--- | :--- | :--- | :--- |
| **Claude Project (chosen)** | Free | File upload as KB, file search built-in | ✅ Free, file KB works for my use case, no setup friction |
| Claude Cowork | Paid | Stronger multi-step skills | ❌ Paid — unnecessary for this scope |
| Custom GPT | Paid (ChatGPT Plus) | Knowledge files, web browsing | ❌ Paid — same capability but costs money |
| n8n agent workflow | Free (self-hosted) | API connectors, triggers | ❌ Over-engineered for a tutoring loop; no richer output |
| Python scripted agent | Free | Any API | ❌ 10h build budget too tight for scripting + debugging |

**Decision:** Claude Project wins on cost (free), setup speed (under 1 hour), and fit — the KB file upload is exactly the "live data connection" this agent needs, and the tutoring loop is a conversation pattern Claude handles natively.

---

## 8. Build Plan (for FL-07)

1. Create Claude Project: "ML Study Coach — Ghulam Qasim"
2. Write and paste the system prompt (Section 4 above)
3. Upload knowledge base files (all 14 FlyRank README files + baseline knowledge note)
4. Run Eval cases 1–5 manually, note what passes and what breaks
5. Iterate on system prompt based on failures
6. Record 2-minute screen capture of one full successful eval run
7. Write build log documenting what changed and why
