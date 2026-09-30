# knoverge.dev

The landing page for [Knoverge](https://github.com/gynsus/knoverge), a knowledge
ledger for humans and AI agents.

One HTML file, one stylesheet, no JavaScript and no build step. That is not
minimalism for its own sake: a page with nothing to build cannot break between
being written and being served, and it is the same decision the product makes
about its own dependencies.

## What is here

```text
public/         everything that is served
  index.html    the page
  styles.css    its styles, dark and light from the same tokens
  og.png        the social card, 1200x630
  icon-180.png  the touch icon
  favicon.svg   the icon
  robots.txt    allows everything, names the sitemap
  sitemap.xml   one URL, because there is one page
  _headers      security headers and cache lifetimes
wrangler.jsonc  what Cloudflare serves, and from where
```

## Editing it

Open `index.html`. To see it, serve the directory rather than opening the file,
so the absolute paths resolve:

```bash
python3 -m http.server 8765 --directory public
```

Then <http://localhost:8765>.

`og.png` and `icon-180.png` are rendered rather than drawn. If the wording on the
card changes, rebuild it from an HTML source at exactly 1200x630 — anything that
renders a page to a PNG will do.

## Deploying

Cloudflare builds nothing and serves `public/` as it is. A push to `main` is a
deployment.

There is no `_redirects` file. Static assets accept only relative URLs in one,
so sending `www` to the apex cannot be expressed there; it is a redirect rule in
the Cloudflare dashboard instead. A rule is also the right place for it: it
answers before anything is served, rather than after.
