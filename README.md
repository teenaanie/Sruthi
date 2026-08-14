# Sruthi — deploying to Vercel

A single static HTML file. No build step, no framework, no server. This is the
easiest possible thing to host, and Vercel will serve it for free.

---

## Before you deploy: two things to know

**1. The Hobby (free) plan is non-commercial only.** Vercel's fair-use terms
restrict the free tier to personal, non-commercial projects. Sharing a demo with
teachers to get feedback is fine. The moment Sruthi takes commission, runs ads,
or is presented as a business, you need Pro at $20/developer/month. Don't build
a business on a plan that prohibits it — Vercel can and does pause accounts for
this.

**2. This deploy makes the page public, not the bookings shared.** The 30-minute
slot holds still live in each visitor's browser. Two people on two phones will
not see each other's holds. Deploying does not fix that — only a real backend
does. Everything else (filters, availability, WhatsApp links, freshness badges)
works exactly as it does locally.

---

## Deploy — pick one

### Option A: drag and drop (no account setup beyond signup, ~2 minutes)

1. Zip this folder's contents (`index.html`, `vercel.json`, `robots.txt`).
2. Go to https://vercel.com/new
3. Drag the zip onto the page.
4. Done. You get a `something.vercel.app` URL.

Fastest way to see it live. Downside: to update it you re-upload by hand.

### Option B: GitHub (recommended if you'll keep changing it)

```bash
cd sruthi-deploy
git init
git add .
git commit -m "Sruthi prototype"
gh repo create sruthi --private --source=. --push
```

Then at https://vercel.com/new, import the repo. Every future `git push`
redeploys automatically, and you get a preview URL per branch.

### Option C: CLI

```bash
npm i -g vercel
cd sruthi-deploy
vercel          # preview deploy
vercel --prod   # promote to production
```

---

## Keep it private while it's a demo

The listings are fake and the numbers are placeholders. Don't let it leak.

- **Vercel Authentication** (Settings → Deployment Protection) is available on
  Hobby and limits access to your Vercel account. Good for solo review.
- **Password Protection** for sharing with teachers who don't have Vercel
  accounts is a Pro add-on.
- `robots.txt` and the `X-Robots-Tag` header in `vercel.json` already tell search
  engines to stay away. **Both must be removed when you launch for real**, or your
  live site will never appear in Google.

---

## Custom domain

Buy a domain anywhere (or through Vercel), then Settings → Domains → Add.
Vercel issues the HTTPS certificate automatically. `sruthi.in` or `sruthi.kerala`
would both read well.

---

## Pre-launch checklist — do NOT skip these before real teachers go up

- [ ] **Replace all placeholder numbers.** `919999900001`–`011` in `index.html`
      are fake. Never ship real numbers without each teacher's written consent
      to publish them.
- [ ] **Child safeguarding policy.** Most students will be minors. Parent's
      number for bookings, teacher references collected and checked, policy
      stated on the page.
- [ ] **DPDP Act 2023 compliance.** Privacy notice, documented teacher consent
      for listing, verifiable parental consent for under-18 users.
- [ ] **Remove the demo banner** at the top of `index.html`.
- [ ] **Remove `robots.txt` and the `X-Robots-Tag` header.**
- [ ] **Upgrade to Pro** if Sruthi is by then a commercial concern.
- [ ] **Move slot holds to a real backend** so bookings sync across visitors.

---

## Where to edit things

| What | Where in `index.html` |
| --- | --- |
| Teacher list, timings, numbers | `const TEACHERS = [...]` — search for `DATA —` |
| How stale is "stale" | `FRESH_DAYS` / `STALE_DAYS` |
| Hold duration | `HOLD_MINUTES` |
| Colours | `:root { ... }` at the top of `<style>` |
| Backend swap point | the four `Store` methods — see the comment above them |
