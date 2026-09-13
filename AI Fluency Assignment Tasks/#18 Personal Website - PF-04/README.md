# PF-04: Personal Website Live on the FlyRank Domain

**Assignment Code:** PF-04  
**Track:** General AI Fluency  
**Phase:** Build  
**Author:** Ghulam Qasim — FlyRank Machine Learning & AI Fluency Intern  

---

## Deliverable 1: Live HTTPS URL

**Live site:** [https://ghulamqasim.netlify.app](https://ghulamqasim.netlify.app)  
*(Deployed via Netlify Drop — public, HTTPS, no credit card required)*

---

## Deliverable 2: DNS Walkthrough

*Written in plain words, as if explaining to a non-technical team member.*

---

### What is DNS and What Does It Actually Do?

DNS stands for **Domain Name System**. The simplest way to think about it: DNS is the internet's phone book.

When you type `ghulamqasim.netlify.app` into a browser, your computer has no idea where that is. It only knows IP addresses — numbers like `75.2.60.5`. DNS is the system that translates the human-readable name into the machine-readable number, so your browser knows which server to talk to.

---

### What Happens Between Typing a URL and the Page Loading?

Here is the full journey, step by step:

**1. You type the address.**
You type `ghulamqasim.netlify.app` and press Enter. Your browser first checks its own memory (cache) — "have I been here before?" If yes, it reuses the IP address it already knows. If no, the lookup begins.

**2. Your computer asks the Recursive Resolver.**
Your internet provider (or a service like Google's `8.8.8.8`) runs a **recursive resolver** — a server whose only job is to go find the answer for you. Your computer asks it: "What is the IP address for `ghulamqasim.netlify.app`?"

**3. The resolver asks the Root Nameserver.**
The resolver starts at the top of the DNS hierarchy — the **root nameservers**. These are 13 sets of servers around the world that know where to find the next layer. The root server says: "I don't know the answer, but `.app` records are managed by these nameservers — go ask them."

**4. The resolver asks the TLD Nameserver.**
`.app` is a **Top-Level Domain (TLD)**. Its nameservers know which nameservers are responsible for `netlify.app`. They point the resolver to Netlify's own nameservers.

**5. The resolver asks Netlify's Nameserver.**
Netlify's nameserver has the actual record. It returns the **A record** (or **CNAME record**) for `ghulamqasim.netlify.app` — the specific IP address of Netlify's server where my site files live.

**6. Your browser connects.**
Now your computer has the IP address. It opens a connection to Netlify's server, requests my `index.html` file, and the page loads in your browser. The whole DNS lookup above takes milliseconds.

---

### What is a CNAME Record?

A **CNAME** (Canonical Name) record is a DNS record type that says: *"This name is an alias for another name."*

For example, if I set up a custom domain `ghulamqasim.com` and wanted it to point to my Netlify site, I would create a CNAME record that says:

```
www.ghulamqasim.com  →  ghulamqasim.netlify.app
```

This tells DNS: "Whenever someone looks up `www.ghulamqasim.com`, treat it as if they typed `ghulamqasim.netlify.app`." Netlify then handles the rest.

CNames are useful because they let you point a domain to a service (like Netlify, Vercel, or GitHub Pages) without knowing or tracking the actual IP address — the service manages its own IPs and your CNAME just follows the name.

---

### Why HTTPS? Where Does the Padlock Come From?

HTTPS means the connection between your browser and Netlify's server is **encrypted**. Without it, anyone on the same network could see what data is being sent.

Netlify automatically issues a free **SSL/TLS certificate** for every site (via Let's Encrypt). When my site deployed, Netlify generated this certificate within seconds. The padlock appears in your browser automatically — I didn't have to configure anything.

---

### Summary in One Paragraph

When you type `ghulamqasim.netlify.app`, your computer asks a resolver to look it up. The resolver works through a hierarchy — root servers, TLD servers, then Netlify's nameservers — until it gets the IP address of the server hosting my files. Your browser connects to that IP, requests my `index.html`, and the page loads. The HTTPS padlock is there because Netlify automatically issued a free SSL certificate when I deployed. A CNAME record is what I'd use if I connected a custom domain — it's an alias that says "treat this name as that other name."

---

## Site Contents

The personal website (`index.html`) contains:
- **Hero section** — name, positioning statement, available-for-opportunities badge
- **Stats row** — 4 measurable outcomes from my work
- **What I Build** — 3 capability cards (ML Pipelines, NLP, AI Workflow Design)
- **Projects** — 3 case studies with real outcomes
- **Connect** — links to GitHub and LinkedIn
- **FlyRank badge section** — internship acknowledgment

---

## Netlify Deployment Steps (for reviewer reference)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the `#18 Personal Website - PF-04/` folder onto the page
3. Netlify assigns a random URL (e.g. `spontaneous-kitten-3f21.netlify.app`)
4. Go to **Site configuration → Change site name**
5. Rename to `ghulamqasim`
6. Live URL becomes: `https://ghulamqasim.netlify.app`
7. HTTPS is automatic — padlock appears within seconds

---

## Files I Can Explain

| File | What it does |
| :--- | :--- |
| `index.html` | The entire single-page website — HTML structure, embedded CSS styles, and content |
| CSS `:root` variables | Define the color palette used everywhere — change one value, updates the whole site |
| `nav` sticky block | Fixed navigation bar with blur backdrop that stays at top while scrolling |
| `.hero` section | First thing visitor sees — name, sub-heading, CTA buttons |
| `.project-card` | Each card is an HTML div with flex layout — content left, arrow link right |
| `@media (max-width: 640px)` | Mobile responsive rules — hides nav links, stacks cards vertically on small screens |
