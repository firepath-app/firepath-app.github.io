# FIRE Path — Landing Page

A single-page static site for FIRE Path (`index.html` + `assets/`). No build step, no dependencies — just plain HTML/CSS. Deploy it with GitHub Pages.

## Preview locally

Open `website/index.html` directly in a browser, or serve it so relative asset paths behave the same as they will in production:

```bash
cd website
python3 -m http.server 8000
# visit http://localhost:8000
```

## Option A — Host from this repo (quickest)

1. Push this repo to GitHub (it already is, if you're reading this from a clone).
2. On GitHub: **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Branch: `main`, folder: **`/website`** (or `/docs` — see note below) → **Save**.
5. GitHub gives you a URL like `https://<your-username>.github.io/fire-calculator/`. It takes a minute or two to go live after the first save.

> **Note:** GitHub Pages only lets you serve from the repo root (`/`) or a `/docs` folder — not an arbitrary folder like `/website`. If `/website` isn't offered as an option in the dropdown, either:
> - Rename this folder to `docs/` (`git mv website docs`), or
> - Use Option B below (a dedicated `gh-pages` branch), which has no folder restriction.

## Option B — Dedicated `gh-pages` branch (keeps the app repo clean)

This publishes only the contents of `website/` to a separate branch, so the site's root URL (`/`) maps directly to `index.html` without renaming anything in `main`.

```bash
# from the repo root, one-time setup
git subtree push --prefix website origin gh-pages
```

Then in **Settings → Pages**, set the source branch to `gh-pages`, folder `/ (root)`.

To publish updates later, re-run the same command:

```bash
git subtree push --prefix website origin gh-pages
```

## Option C — Separate GitHub account/repo with a custom domain

Since you mentioned possibly wanting a custom domain under a different GitHub account:

1. Create a new repo there named `<your-username>.github.io` (this special name serves at the account's root domain automatically) — or any repo name if you're fine with a `/reponame/` path.
2. Copy the contents of this `website/` folder (`index.html` + `assets/`) into that repo.
3. Push, then enable Pages in that repo's **Settings → Pages** (source: `main`, root).
4. To use a custom domain (e.g. `firepathapp.com`):
   - Add a `CNAME` file to the repo root containing just the domain, e.g.:
     ```
     firepathapp.com
     ```
   - At your domain registrar, add:
     - Either an `A` record pointing `@` to GitHub Pages' IPs (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`), or a `CNAME`/`ALIAS` record for `www` pointing to `<your-username>.github.io`.
   - Back in **Settings → Pages**, enter the custom domain and enable **Enforce HTTPS** once DNS propagates (can take up to 24h).

## Updating the page

Everything is in one file — edit `index.html` directly (styles are inline in a `<style>` block, no build step to run). Images live in `assets/`; they're already resized for web (max 700px wide) to keep the page light. Re-deploy by pushing to whichever branch Pages is configured to serve.

## What's in here

- `index.html` — the full page (hero, feature sections, privacy section, final CTA)
- `assets/icon.png` — app icon, used as favicon and in the nav
- `assets/shot-*.png` — framed iPhone screenshots pulled from `AppStoreScreenshots/Iphone17Mockups/`

The App Store link is hardcoded in a few places in `index.html` — search for `apps.apple.com` if it ever changes.
