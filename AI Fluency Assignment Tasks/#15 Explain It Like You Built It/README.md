# Task : Explain It Like You Built It

**Assignment:** Week 5 — Explain It Like You Built It  
**Track:** General AI Fluency  
**Author:** Ghulam Qasim  

---

## What I Chose to Explain

**Topic:** How GitHub Actions automatically deploys my portfolio site when I push code.

**Why I chose this:** When I first saw `.github/workflows/static.yml` in my repository, I had no idea what it was doing. I knew pushing code somehow updated the live site, but I didn't understand the mechanism — it felt like magic. After having AI tutor me on it, I actually understand what's happening.

---

## My Explanation (In My Own Words)

*Written as if explaining to a friend who has never built a site.*

---

So you know how when I update a file on my laptop and want the live website to change, I have to somehow get that file onto the internet? Normally you'd think you'd have to manually upload it somewhere every time. That's where GitHub Actions comes in — it does that job automatically.

Here's how I think about it: GitHub Actions is like a robot worker that sits and watches my repository. I gave it a set of instructions written in a file called `static.yml` — think of it like a recipe card. The recipe says: "Whenever Qasim pushes new code to the `main` branch, wake up, take all his files, and put them on GitHub Pages."

So when I type `git push` on my laptop, three things happen in sequence:

**First**, my code travels from my laptop to GitHub's servers — that's just the normal git push.

**Second**, GitHub sees the push land on the `main` branch and wakes up the Actions runner — that's the robot. It reads my `static.yml` recipe and starts following it step by step.

**Third**, the runner picks up my files and deploys them to GitHub Pages — the public hosting service that makes my files available at my URL. The whole process takes about 60 seconds.

The `.nojekyll` file I also added is a small but important detail. GitHub Pages has a built-in assistant called Jekyll that tries to process your files before serving them. The problem is Jekyll ignores any folder whose name starts with `#` — and ALL my assignment folders start with `#1`, `#2`, `#3` and so on. So Jekyll was silently hiding them. The `.nojekyll` file (it's literally an empty file) just tells Jekyll: "Don't touch anything, serve the files exactly as they are."

The result: every time I `git push`, the site updates itself within a minute. I never have to touch a dashboard or manually upload anything. The recipe runs, the robot works, the site updates.

---

## What I Learned

Before this, I thought deployment was this mysterious complicated thing. Now I see it's just: a trigger (push to main) → an instruction file → an automated job → files served publicly. The concepts are the same whether it's GitHub Actions, Netlify, or any other CI/CD system — the pattern repeats everywhere in software engineering.
