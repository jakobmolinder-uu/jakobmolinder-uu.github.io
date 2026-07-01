# jakobmolinder.com

Personal academic website for Jakob Molinder. Plain, static HTML + one CSS file.
**No build step, no framework, no database, no tracking.** That is exactly why it is
free to host, fast, and impossible to hijack the way the old WordPress site was.

```
index.html            Home (bio, news, featured project, selected pubs, UHILL)
publications.html     Full publication list
research.html         Current projects + working papers
data.html             Public datasets (linked from your Dropbox + SND)
contact.html          Contact details
404.html              Friendly not-found page
css/style.css         All styling (light + dark mode, responsive sidebar layout)
assets/img/           Photo + favicon
assets/cv.pdf         Your CV (replace anytime, keep the filename)
_redirects            Old WordPress URLs → new pages (keeps inbound links working)
_headers              Basic security headers
robots.txt, sitemap.xml
```

## Preview it locally

Just double-click `index.html`, or for a proper local server:

```bash
cd ~/jakobmolinder-website
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy for free on Cloudflare Pages

**Recommended: connect a GitHub repo (easiest to update later).**

1. Create a GitHub repo and push this folder:
   ```bash
   cd ~/jakobmolinder-website
   git init && git add -A && git commit -m "Initial site"
   # create an empty repo on github.com, then:
   git remote add origin https://github.com/<you>/jakobmolinder-website.git
   git push -u origin main
   ```
2. Go to **Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git**, pick the repo.
3. Build settings — this is a plain static site, so:
   - Framework preset: **None**
   - Build command: **(leave empty)**
   - Build output directory: **`/`** (the repo root)
4. Deploy. Your site is instantly live at `https://<project>.pages.dev`.

*No GitHub?* In Pages choose **Upload assets** and drag this whole folder in. (You then re-upload to update.)

## Point jakobmolinder.com at it

Your domain is currently managed through WordPress.com. Cleanest path:

1. In Cloudflare, **add jakobmolinder.com as a site** (free plan). Cloudflare gives you two
   nameservers.
2. At your domain registrar, change the nameservers to Cloudflare's. (If WordPress.com is your
   registrar, you may first need to unlock/transfer the domain, or use route (ii) below.)
3. In **Pages → your project → Custom domains**, add `jakobmolinder.com` and `www.jakobmolinder.com`.
   Cloudflare provisions HTTPS automatically.
4. Once the new site loads on the real domain, **cancel the WordPress.com plan.**

*(Alternative — keep DNS at the current provider: add the CNAME record Cloudflare Pages shows you
under Custom domains. Slightly more manual, no nameserver change.)*

The `_redirects` file means old links like `jakobmolinder.com/publications/` keep working and
land on the new pages.

## Updating the site

You have technical chops, so either works:

- **Edit the HTML directly.** Content is plain and clearly labelled. To add a paper, copy an
  existing `<li class="pub">…</li>` block in `publications.html` and edit it.
- **Or just ask Claude Code**, e.g. *"add this new paper to publications and a news item on the
  home page"*, *"update my bio"*, *"swap in my new photo"*. That is the low-friction path.

Two maintenance notes:

- The **sidebar** (photo, title, nav, links) is duplicated at the top of every `.html` file so the
  site needs zero JavaScript. If you change a link, change it on all five pages (or ask Claude Code).
- Replace **`assets/cv.pdf`** with your latest CV using the same filename and the link just works.
  Replace **`assets/img/jakob-molinder.jpg`** with a new portrait (keep it ~600–800 px, optimized).

## A few things to double-check (I flagged these while rebuilding)

- **Erik Bengtsson** is cited correctly as *"Bengtsson, E."* here — your old site and CV had
  *"Bengtsson, B."* on the 2024 Stockholm-incomes and 2025 Great-Levelling papers. Worth fixing in
  your CV too.
- I listed your title as **Associate Professor of Economic History** (per Google Scholar). Your CV
  says "Associate and Assistant Professor" — adjust the sidebar text on each page if you prefer a
  different wording.
- **Lund email** is not shown (I only had your Uppsala address confirmed). Add it to `contact.html`
  if you'd like it listed.
- The **"Malmsten Fellow"** news item spelling — your CV writes "Malmsteen". Confirm and edit
  `index.html` if needed.
- A couple of older working-paper PDF links (Lund) may need refreshing if the repository moved.
