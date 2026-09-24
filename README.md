# leadkeeper-site

Static, bilingual (Thai/English) one-page site for LeadKeeper. Plain HTML + CSS,
no build step, no JavaScript framework — deploys as-is via Hostinger's Git
integration into `public_html`.

## ⚠️ Not launch-ready: no contact info is published

`index.html` and `en/index.html` currently have **no Contact section and no
CTA buttons in the hero**. The source brief listed LINE OA ID, email, and
LinkedIn as `[bracketed]` placeholders with no real values, and the brief's
own hard rule #3 says bracketed values must not be published — so they were
removed rather than invented.

The problem: this site's stated purpose is letting partner programs and
prospects verify the business is real *and reach it*. Right now nobody who
lands on the site can contact LeadKeeper — no LINE button, no email link, no
LinkedIn. That defeats the primary goal, not a cosmetic gap. Fill in **at
least one real contact method** (email is the easiest to stand up on the
domain, e.g. `hello@leadkeeper.site`) before this goes live.

Also removed for the same reason: the founder's name in the "About" section,
and the business registration number in the footer.

## How to add the missing values

1. Get a working email address, a LINE Official Account ID/link, and the
   founder's LinkedIn URL.
2. In `index.html` (Thai) and `en/index.html` (English):
   - Add a `.cta-row` inside `.hero .wrap` with the LINE and email buttons
     (see `.btn`, `.btn-primary`, `.btn-secondary` in `assets/style.css`).
   - Add a `<section id="contact">` before the footer, with a `.contact-list`
     of `<li><a href="...">...</a></li>` items for LINE, email, LinkedIn.
   - In "About", reinstate "...founded in 2026 by **[name]**, based in
     Bangkok."
3. When the business registration number exists, add it to the footer `<p>`
   in both files.

## Editing copy

All visible text lives directly in `index.html` / `en/index.html` — there is
no CMS or templating. Edit the HTML, keep both language versions in sync, and
don't reintroduce anything in `[brackets]`.

Shared styling is in `assets/style.css`. The favicon (`favicon.svg`) is a
plain "LK" text mark — no third-party logos are used anywhere on the site,
per the brief.

## Local preview

No build step needed. Serve the folder with any static server, e.g.:

```
python3 -m http.server 8000
```

Then open `http://localhost:8000/` and `http://localhost:8000/en/`.

## Redeploy

Push to `main`. Hostinger's Git integration copies the repo as-is into
`public_html` on every push — no build, no `package.json`, no `node_modules`
anywhere in the repo (Hostinger would otherwise treat it as a Node app).

## Connecting Hostinger (do this yourself in hPanel)

1. **hPanel → Websites → your site → Git.**
2. Connect the repository `rapintk/leadkeeper-site`, branch `main`, deploy
   path = document root (`public_html`).
3. Trigger the first deployment (or push a commit to `main` — this repo is
   already on `main` after this change).
4. **hPanel → Domains** — point `leadkeeper.site` at this hosting account if
   not already done, and confirm `www.leadkeeper.site` also resolves there
   (`.htaccess` redirects `www` → apex, but DNS must route both first).
5. **hPanel → SSL** — issue/enable the free SSL certificate for
   `leadkeeper.site` (and `www`). `.htaccess` forces HTTPS once the
   certificate is active — enabling it before the cert exists will break
   the site.
6. After DNS + SSL propagate, verify both `https://leadkeeper.site/` and
   `https://leadkeeper.site/en/` load, and that a bad URL shows the custom
   404 page.
