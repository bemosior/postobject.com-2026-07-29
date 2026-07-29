# postobject.com — static backup

A static mirror of the Postobject Squarespace site, captured on 2026-07-29
before the Squarespace account was canceled. All HTML, CSS, JS, images, and
fonts referenced by the five live pages were downloaded and rewritten to
local relative paths, so the site no longer depends on Squarespace's
infrastructure.

## Pages captured

- `index.html` — homepage
- `blog.html` — blog index (no posts existed at capture time)
- `contact.html`
- `cart.html`
- `workshop-template.html` — unlisted page, not linked from nav

## Known limitations

This is a **visual/content snapshot**, not a functioning copy of the
Squarespace site:

- The subscribe form, contact form, and cart are non-functional — they
  posted to Squarespace's backend, which no longer exists for this content.
- The cookie-consent banner can't be dismissed (its script calls a
  Squarespace API), but it doesn't block scrolling or reading the page.
- Analytics/editor scripts pulled from `assets.squarespace.com` and
  `definitions.sqspcdn.com` are included since the page referenced them,
  but aren't required for the site to display correctly.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. In the repo settings, enable Pages, source: `main` branch, `/ (root)`.
3. The `.nojekyll` file is already present so GitHub doesn't try to run
   Jekyll over the Squarespace output.
4. To serve this under `postobject.com` again, add a `CNAME` file
   containing the domain and point the domain's DNS at GitHub Pages
   (this wasn't done automatically — it changes live DNS).

## Regenerating this mirror

```
wget --page-requisites --span-hosts --convert-links --adjust-extension \
  --restrict-file-names=windows --no-parent -e robots=off \
  https://www.postobject.com/ https://www.postobject.com/blog \
  https://www.postobject.com/contact https://www.postobject.com/cart \
  https://www.postobject.com/workshop-template
```

`--span-hosts` is required — Squarespace serves images and fonts from
separate CDN domains that wget won't follow by default.
