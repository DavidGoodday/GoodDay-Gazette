# The GoodDay Gazette

GoodDay Software's weekly internal newsletter. Published every Friday, covering the previous seven days across Sales, Partnerships, Merchant Success, Engineering, and the wider team.

Deployed at: `goodday-gazette.vercel.app` (or your custom Vercel URL)

---

## Repo structure

```
goodday-gazette/
├── index.html              # Always the latest issue
├── archive.html            # Index of all past issues (served at /archive)
├── issues/
│   ├── vol-1-no-1.html     # May 8, 2026 — inaugural
│   └── vol-1-no-2.html     # May 14, 2026 — latest
├── vercel.json             # Clean URLs, security headers, /latest → /
├── .gitignore
└── README.md
```

Each issue is a single self-contained HTML file. No build step, no framework, no node_modules. Chart.js loads from CDN. Everything else is inline.

---

## One-time setup (10 minutes)

You'll do these once, then forget about them.

### 1 — Create a GitHub repo

1. Go to https://github.com/new
2. Owner: `gooddaysoftware` (or your personal account if you prefer)
3. Repository name: `goodday-gazette`
4. Visibility: **Private**
5. Skip the "Initialize this repository" checkboxes
6. Click **Create repository**

### 2 — Push this folder

In Terminal, `cd` into the folder containing this README and run:

```bash
git init
git add .
git commit -m "Initial: Vol. I No. 1 and No. 2"
git branch -M main
git remote add origin git@github.com:gooddaysoftware/goodday-gazette.git
git push -u origin main
```

(If you don't have SSH set up, swap the remote URL for `https://github.com/gooddaysoftware/goodday-gazette.git` and you'll get prompted for credentials.)

### 3 — Connect to Vercel

1. Go to https://vercel.com/new
2. Click **Import Git Repository** and pick `goodday-gazette`
3. **Framework Preset:** Other
4. **Root Directory:** leave as is (`./`)
5. **Build / Output settings:** leave as defaults — Vercel will detect it as a static site
6. Click **Deploy**

In ~30 seconds you'll get a URL like `goodday-gazette-xxxxx.vercel.app`. The deploy reads `vercel.json` automatically — clean URLs and security headers are already set.

### 4 — Lock it down to the GoodDay team

1. In the Vercel project, go to **Settings → Deployment Protection**
2. Under **Vercel Authentication**, toggle it **On**
3. Choose **All Deployments** (or just Production if you want preview branches public)
4. Save

Now only people signed into your Vercel team can view the URL. Share the link in Slack — anyone clicking it will be prompted to authenticate with Vercel.

### 5 — (Optional) Custom domain

In **Settings → Domains**, add something like `gazette.gooddaysoftware.com`. Add the CNAME record Vercel shows you to your DNS, wait a few minutes, done.

---

## Publishing a new issue every Friday

Three steps. Eventually this becomes a Cowork skill that automates all three.

### Manual (today)

1. Run the GoodDay Gazette weekly skill (or ask Claude in Cowork: *"refresh the GoodDay Gazette for this week"*).
2. Take the resulting HTML file and:

```bash
cd goodday-gazette

# Save the new issue to the archive
cp /path/to/new-issue.html issues/vol-1-no-3.html

# Make it the new "latest"
cp issues/vol-1-no-3.html index.html

# Add a row to archive.html (between the masthead and the existing issues)
# — open archive.html and copy/paste the most recent <div class="issue">…</div>
#   block, swap in the new title, deck, date, and href.

git add .
git commit -m "Vol. I No. 3 — May 21, 2026"
git push
```

Vercel auto-deploys on push. Within ~30 seconds the live site updates.

### Automated (future)

The weekly Cowork skill can be wired to do steps 1–4 above automatically — generate the HTML, commit, push. That requires a GitHub deploy token; happy to scaffold when you're ready.

---

## Local preview

Want to look at the site locally before pushing?

```bash
cd goodday-gazette
python3 -m http.server 8080
# Then open http://localhost:8080
```

Or just open `index.html` directly in a browser — the file:// protocol works fine since everything is self-contained.

---

## Editing an issue after publish

Each issue is a single HTML file. Edits are direct: open `issues/vol-1-no-2.html`, find the text, fix it, commit, push. No build step.

Typo-level fixes don't need a new version number — just commit with `Vol. I No. 2 — fix typo on Page 3` or similar.

---

## What's in each issue

Every weekly issue covers the same six surfaces:

1. **Front Page** — three to six top stories that cut across departments
2. **Sales Desk** — `#sales-support` + `#go-to-market` Slack + Gong calls by Kelley + Kyle
3. **Partnerships** — `#partnerships` Slack + Gong calls by Evan
4. **Merchant Success** — `#merchant-success` Slack + Pylon themes + Gong calls by the MS team
5. **Engineering** — `#engineering`, `#critical-support`, `#product-support`, `#sers-tavern`
6. **Around GoodDay** — Notion All Hands + VOTM agendas + personal section

Vol. I No. 1 (the inaugural issue) doesn't have a Partnerships page — that started with No. 2.

---

## Questions?

The weekly skill lives in the Cowork session. To regenerate, restart, or change the structure, message David Ortiz or whoever currently owns the skill.
