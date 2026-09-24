# leadkeeper-site

Static, bilingual (Thai/English) one-page site for LeadKeeper. Plain HTML + CSS,
no build step, no JavaScript framework — deploys as-is via Hostinger's Git
integration into `public_html`.

## Contact info still hidden

Business registration number is still a placeholder and is not published
anywhere (footer, both languages). Add it to the footer `<p>` in `index.html`
and `en/index.html` once you have it — everything else from the original
brief (founder name, LINE, email, LinkedIn) is live.

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
