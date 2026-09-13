# Task: Survive the Crit

**Assignment Code:** Survive the Crit  
**Track:** General AI Fluency  
**When:** Week 6  
**Phase:** Build+  
**Author:** Ghulam Qasim — FlyRank Machine Learning & AI Fluency Intern  
**Live Site Reviewed:** [https://ghulamqasim.netlify.app](https://ghulamqasim.netlify.app)

---

## 1. Executive Summary

The purpose of this assignment is to submit the live portfolio for **peer design review** without defending, collect raw feedback on positioning and clarity, sort feedback into **Must-Fix** vs. **Nice-to-Have**, and implement the Must-Fix items directly on the live website.

---

## 2. Reviewer Brief & Proof Statement Provided

Before asking for feedback, the reviewer was provided with Ghulam Qasim's **Proof Statement** from Chapter 1:

> **Proof Statement:**  
> *"I build production-grade ML pipelines and AI-native automation that replace manual bottlenecks with measurable speed, accuracy, and ROI."*

---

## 3. Two Core Reviewer Questions & Raw Answers

| # | Question Asked | Reviewer's Raw Unedited Response | Assessment |
|---|---|---|---|
| **Q1** | **In 10 seconds, what do I do?** | *"You build machine learning systems and AI automation for companies. Your site clearly says you work on ML pipelines and NLP classification."* | ✅ **Pass** — Reviewer immediately stated the exact core focus within 10 seconds. |
| **Q2** | **Would you believe I'm good at it?** | *"Yes, because you have specific numbers right near the top — like 10× speedup and 91% accuracy target — rather than just saying 'experienced engineer'. But I wanted a direct way to contact you on the page instead of just GitHub links."* | ✅ **Pass with feedback** — Numbers built credibility, but missing contact form was identified as a gap. |

---

## 4. Feedback Sorting: Must-Fix vs. Nice-To-Have

```
RAW FEEDBACK RECEIVED:
1. "Add a direct message form on the site so visitors don't have to leave to contact you."
2. "Highlight the FlyRank internship badge more clearly."
3. "Make the primary CTA button pop out more on mobile screens."
4. "Add a dark/light mode toggle."
5. "Add video previews of the projects."
```

### Feedback Sorting Table:

| Feedback Item | Category | Reason / Priority | Action Taken |
|---|---|---|---|
| **1. Add direct contact form on page** | 🚨 **MUST-FIX** | Directly impacts the single most important user action (getting in touch). Leaving site to email creates drop-off. | **FIXED:** Added live, fully integrated Web3Forms contact form with AJAX status feedback. |
| **2. Improve mobile CTA button visibility & touch target** | 🚨 **MUST-FIX** | Hurt mobile navigation usability and tap accuracy. | **FIXED:** Increased touch targets to 44px min-height, full-width on mobile. |
| **3. Highlight FlyRank internship badge** | 🚨 **MUST-FIX** | Enhances credibility and proof statement context for evaluators. | **FIXED:** Added dedicated glowing FlyRank AI Fluency Internship card section. |
| **4. Add dark/light mode toggle** | 💡 **NICE-TO-HAVE** | Dark mode is already the primary brand aesthetic; toggle is low priority. | Deferred to future iteration. |
| **5. Add video previews of projects** | 💡 **NICE-TO-HAVE** | Great for FL-07 demo, but GitHub links & screenshots already fulfill current scope. | Deferred to capstone polish. |

---

## 5. Evidence of Must-Fixes Addressed on Live Site

1. **Live Contact Form Added (`#contact`):**
   - Added `<form id="contact-form">` with Name, Email, and Message fields.
   - Integrated Web3Forms / Netlify Forms API backend (`https://api.web3forms.com/submit`).
   - Added instant AJAX success/error state container (`#form-status`).

2. **Mobile CTA & Touch Target Polish:**
   - Updated `.btn-primary` and `.btn-ghost` CSS with `min-height: 44px`.
   - On viewports < 640px, CTA buttons automatically expand to full width (`width: 100%`) for effortless thumb tapping.

3. **FlyRank Internship Section:**
   - Added structured internship acknowledgment section with gradient border and `🎖 FlyRank AI Fluency — In Progress` badge.

---

## 6. Pass / Revise Criteria Checklist

- [x] **Submitted with Proof Statement:** Reviewed against Chapter 1 proof statement.
- [x] **10-Second Test Passed:** Reviewer correctly stated core role ("ML pipelines & AI automation").
- [x] **Feedback Sorted Honestly:** Divided into Must-Fix vs. Nice-to-Have without defensive pushback.
- [x] **Must-Fixes Implemented:** All 3 must-fixes live on site and verified.
