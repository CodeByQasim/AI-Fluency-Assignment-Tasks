# FL-07: Build the Agent — ML Study Coach

**Assignment Code:** FL-07  
**Track:** General AI Fluency  
**Phase:** Build  
**Author:** Ghulam Qasim  
**Agent:** ML Study Coach (Claude Project, free tier)  
**Spec reference:** [FL-06 Design Doc](../\#16%20Design%20Your%20Personal%20Agent%20-%20FL-06/README.md)

---

## Deliverable 1: Working Agent

**Platform:** Claude.ai — Claude Project (free tier)  
**Project name:** `ML Study Coach — Ghulam Qasim`  
**Live tool connection:** File search over uploaded FlyRank assignment README files (14 files = knowledge base)

---

## Deliverable 2: System Prompt (Agent Instructions)

Paste this exactly into the Claude Project's "Project instructions" field:

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

## Deliverable 3: Build Log

### Step 1 — Created Claude Project
- Created new Project in Claude.ai: "ML Study Coach — Ghulam Qasim"
- Pasted system prompt into Project Instructions field
- **Result:** Agent responded correctly to first test prompt

### Step 2 — Uploaded Knowledge Base Files
Uploaded the following files to the Project:
- All 14 FlyRank assignment README.md files
- A brief `my-baseline.md` describing my current ML knowledge level

**Issue encountered:** Claude Project has a file size limit per upload. Solution: combined all READMEs into one `flyrank-assignments-kb.md` file and uploaded that instead.

**Deviation from spec:** Spec said upload all 14 files individually. Changed to single combined KB file due to upload limits. Outcome identical — file search still works across all content.

### Step 3 — Ran Eval Cases 1–5

| Eval | Result | Notes |
| :--- | :--- | :--- |
| Eval 1: Attention in transformers | ✅ Pass | Explanation correct, used analogy, quiz asked |
| Eval 2: Fine-tuning vs RAG | ✅ Pass | Referenced my ML pipeline project from KB |
| Eval 3: `loss.squeeze()` code | ✅ Pass | Explained correctly, quiz targeted squeeze |
| Eval 4: RLHF explained | ✅ Pass | Under 250 words, one link given |
| Eval 5: Wrong quiz answer | ✅ Pass | Agent caught wrong answer, corrected precisely |

### Step 4 — One Prompt Iteration
**Problem found:** On first run, agent gave 3 "read next" links despite rule saying one.  
**Fix:** Added to system prompt: *"You are only allowed to give ONE 'read next' resource. If you list more than one, you have failed at your job."*  
**Result:** Agent now consistently gives one link only.

### Step 5 — Recorded Screen Capture
- Recorded a 2-minute unedited screen capture of Eval 1 (attention in transformers)
- Full loop shown: my input → agent explanation → my quiz answers → agent feedback
- File: `run-capture.mp4` *(to be uploaded to FlyRank portal directly — file too large for GitHub)*

---

## Deliverable 4: Run Capture Note

**Screen capture:** Recorded using Windows + Shift + R (Xbox Game Bar) or OBS.  
**Duration:** ~2 minutes  
**What it shows:**
1. Claude Project open with ML Study Coach
2. I paste: *"What is attention in transformers? I keep reading about it but I don't really get what it's computing."*
3. Agent explains with query/key/value analogy
4. Agent asks a check question
5. Agent gives 2 quiz questions
6. I answer (one wrong deliberately)
7. Agent catches the wrong answer and corrects the gap

*Upload the `.mp4` directly to the FlyRank portal submission field.*

---

## What I Cut From the Spec and Why

| Cut Item | Reason |
| :--- | :--- |
| Web search tool (Phase 2) | Not in free Claude tier without API — cut to stay on free path. Study coaching works fine without live web. |
| Individual file uploads (14 files) | Claude Project file limit — combined into one KB file. Same search capability, no loss of functionality. |
| Monthly notes update automation | Out of 10h build scope — manual update (copy-paste new README) is fast enough for now. |
