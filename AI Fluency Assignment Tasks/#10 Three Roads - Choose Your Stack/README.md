# Task #10: Three Roads — Choose Your Stack with AI

**Track**: General AI Fluency  
**Phase**: Build  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 04](https://aifluency.flyrank.ai/week-04.html#three-roads)  

---

## 📌 Executive Summary

Choosing how to build is a core AI-fluency skill. Rather than obeying the first AI recommendation, this assignment evaluates three genuine tech stack options under four real constraints, analyzes trade-offs, and documents the final build rationale in my own words.

---

## 🔒 The Four Input Constraints Given to AI

1. **Cost Constraint**: 100% Free Tier Only (zero hosting or domain costs).
2. **Skill Level Constraint**: Machine Learning & Python intern with working HTML/CSS/JS knowledge; avoiding unnecessary backend DevOps overhead during build week.
3. **Content Needs**: Must display 4 sitemap pages, 3 structured case studies, architecture diagrams, code block syntax highlighting, and an embedded Calendly widget.
4. **Backend Requirement**: **Not yet needed.** Portfolio is static content presenting proof; dynamic server-side databases add maintenance drag without adding proof value.

---

## 🛣️ Three Stack Options Evaluated

### Option 1 (Simplest): Raw HTML/CSS + GitHub Pages
- **How to Build**: Plain HTML5, Vanilla CSS using Identity Kit variables (`#0B0F19`), and basic JS for tab switching.
- **Hosting**: GitHub Pages (Free).
- **Backend Needed**: No.
- **Real Trade-Off**: Extremely fast to ship, but code duplication across navigation bars and headers makes multi-page edits tedious.

### Option 2 (Balanced / Chosen): Vite + React / Static HTML + Vercel
- **How to Build**: Vite build tool with modular components for header, case study cards, and footer using Vanilla CSS.
- **Hosting**: Vercel / Netlify / GitHub Pages (Free Tier).
- **Backend Needed**: No.
- **Real Trade-Off**: Requires npm setup, but component reusability makes updating case studies effortless.

### Option 3 (Most Powerful): Full-Stack Next.js 14 + Tailwind + Supabase + Vercel
- **How to Build**: Next.js App Router, Tailwind CSS, Supabase PostgreSQL database for dynamic project comments.
- **Hosting**: Vercel Free Tier + Supabase Free Tier.
- **Backend Needed**: Yes (Supabase PostgreSQL).
- **Real Trade-Off**: Complete overkill. Adds environment variable configuration, database migrations, and deployment breaking risks for a portfolio that doesn't require dynamic user logins.

---

## ⚖️ Pressure-Testing & Trade-Off Analysis

| Pressure-Test Question | Option 1 (HTML/CSS) | Option 2 (Vite / React / Static) | Option 3 (Next.js + Supabase) |
| :--- | :--- | :--- | :--- |
| **What breaks if I pick the simplest?** | Nothing breaks, but repeating header/footer code on 4 pages invites maintenance copy-paste errors. | Perfect balance of component reuse and zero backend overhead. | Over-engineered. Server actions and DB connection timeouts will waste build week time. |
| **Can I finish in 2 weeks?** | Yes (~3 hours). | **Yes (~4 hours).** | Unlikely; debugging database schemas wastes time. |
| **Does it show my work well?** | Yes, but lacks interactive tab filtering. | **Yes; supports clean component cards, code highlighting, and embedded widgets.** | Yes, but offers zero extra visual proof value to a CTO. |
| **Can I maintain this alone?** | Yes. | **Yes, easily.** | High maintenance overhead. |

---

## 🎯 Written Rationale: The Chosen Stack

### Chosen Stack: **Option 2 — Vite + React / Static Components on Vercel & GitHub Pages**

> **In My Own Words**:  
> *"I chose Option 2 (Vite + React component architecture hosted on Vercel/GitHub Pages) because it strikes the exact balance between speed, maintainability, and visual fidelity. Option 1 (raw HTML) requires copy-pasting headers across four pages, while Option 3 (Next.js with Supabase DB) introduces unnecessary database backend overhead for a portfolio that needs zero server-side user data.*  
>  
> *Option 2 allows me to write modular `<CaseStudyCard />` components that inherit my `#0B0F19` Identity Kit perfectly. Can I maintain this? Yes—updating a project is as simple as editing a single JSON object. Does it show my work well? Absolutely—it delivers instantaneous page loads and clean syntax highlighting for code snippets without any server startup latency."*

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Three Genuine Options Evaluated**: Simplest (HTML/GitHub Pages), Balanced (Vite/React/Vercel), Most Powerful (Next.js/Supabase).
- [x] **Four Constraints Applied**: Free tier, ML intern skill level, sitemap display needs, no backend needed.
- [x] **Honest Backend Answer**: Correctly identified "not yet needed."
- [x] **Written Rationale**: Rationale written in own words addressing maintainability and display quality.
