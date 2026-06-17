# Launching samsonbienstock.com

You already have the hard parts done: the domain is purchased and the site is
built (`index.html`, `about.html`, `projects.html`, `style.css`, plus `assets/`).
This is a **static site**, so the rest is hosting + pointing your domain at it.

> **Recommendation:** Use **Cloudflare Pages** or **Netlify**. Both are free,
> give you HTTPS automatically, deploy on every change, and handle the custom
> domain cleanly. Steps below cover Netlify (simplest) with Cloudflare notes.

---

## Step 1 — Put the site in a Git repo (recommended but optional)

A repo lets the host auto-redeploy whenever you edit a file. If you'd rather not,
skip to Step 2's drag-and-drop option.

1. Create a free GitHub account if you don't have one.
2. Make a new **private** repo named `samsonbienstock-site`.
3. From this folder:
   ```bash
   cd "/Users/samsonbienstock/Desktop/Ryan/Career/website"
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/samsonbienstock-site.git
   git push -u origin main
   ```

---

## Step 2 — Deploy the site

### Option A — Netlify (easiest)
1. Sign up at https://netlify.com (use "Continue with GitHub").
2. **If you did Step 1:** "Add new site" → "Import an existing project" → pick the
   repo. Leave build command blank, publish directory = `/` (root). Deploy.
3. **If you skipped Git:** Go to the "Sites" tab and **drag this entire `website`
   folder** onto the upload area. Done — it's live on a `*.netlify.app` URL.

### Option B — Cloudflare Pages
1. Sign up at https://dash.cloudflare.com → "Workers & Pages" → "Create" → "Pages".
2. Connect the GitHub repo (or upload the folder directly).
3. Framework preset = "None", build output directory = `/`. Deploy.

At this point your site is live on a temporary URL. Verify it looks right before
moving on.

---

## Step 3 — Connect your domain (samsonbienstock.com)

You need to know **where you bought the domain** (the registrar — e.g. GoDaddy,
Namecheap, Google/Squarespace, Cloudflare). You'll change DNS settings there.

### If you used Netlify
1. In the site dashboard: **Domain management** → "Add a domain" →
   enter `samsonbienstock.com`.
2. Netlify shows you DNS records. Two paths:
   - **Easiest:** Change your domain's **nameservers** to Netlify's (Netlify
     gives you the exact values). Do this at your registrar under "Nameservers".
   - **Or keep your registrar's DNS** and add the records Netlify lists:
     - `A` record → `@` → Netlify's load-balancer IP (they provide it)
     - `CNAME` record → `www` → `your-site.netlify.app`
3. Add both `samsonbienstock.com` and `www.samsonbienstock.com`; set one to
   redirect to the other (pick which you prefer as the primary).

### If you used Cloudflare Pages
1. Easiest if your domain's nameservers are already on Cloudflare. In the Pages
   project: **Custom domains** → "Set up a domain" → `samsonbienstock.com`.
   Cloudflare wires the DNS for you automatically.
2. Also add `www.samsonbienstock.com`.

### HTTPS / SSL
Both hosts issue a free SSL certificate automatically once DNS is verified.
Just wait for the dashboard to show "certificate active" — no action needed.

---

## Step 4 — Wait for DNS, then verify

- DNS changes can take **5 minutes to a few hours** (occasionally up to 24h).
- Check progress at https://dnschecker.org (search `samsonbienstock.com`).
- When ready, visit:
  - https://samsonbienstock.com
  - https://www.samsonbienstock.com
  - Confirm the padlock (HTTPS) shows and isn't a warning.

---

## Step 5 — Polish before sharing it on your resume

- [ ] **Favicon** — add a small `favicon.ico` (your initials/logo) so the browser
      tab looks finished. Put it in the folder and add to each page's `<head>`:
      `<link rel="icon" href="/favicon.png">`
- [ ] **Social preview** — add Open Graph tags so links look good when shared
      (LinkedIn, text). Add to each `<head>`:
      ```html
      <meta property="og:title" content="Samson Bienstock">
      <meta property="og:description" content="Energy projects & capital.">
      <meta property="og:image" content="https://samsonbienstock.com/assets/samson.jpg">
      <meta property="og:url" content="https://samsonbienstock.com">
      ```
- [ ] **Proofread** all three pages on desktop **and** phone.
- [ ] **Resume link** — add the live URL to your resume and LinkedIn profile.
- [ ] (Optional) Analytics — Cloudflare Web Analytics or Plausible (privacy-
      friendly, free/cheap) to see who's visiting.

---

## Quick reference

| Thing | Value |
|---|---|
| Domain | samsonbienstock.com (already purchased) |
| Site type | Static HTML/CSS — no build step needed |
| Files to deploy | everything in this `website` folder |
| Recommended host | Netlify or Cloudflare Pages (free, auto-HTTPS) |
| What to change at registrar | Nameservers **or** A + CNAME records |

**The one thing to figure out first:** which registrar you bought the domain
from — that's where Step 3's DNS changes happen.
