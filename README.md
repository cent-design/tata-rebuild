# Slurp — static mirror

A clean, self-hosted static copy of [slurpramen.dk](https://slurpramen.dk), a
Webflow-built site (incl. Webflow Ecommerce cart/checkout). Pages, layout,
styling, and interactive behavior (nav, cart, forms, video backgrounds) are
byte-for-byte reproductions of the live site — only asset paths were
relocated to serve locally instead of from Webflow's CDN.

## Structure

```
index.html              Home
menu/index.html          /menu
store/index.html         /store
checkout/index.html      /checkout
assets/site/              Site's own assets: logo, icons, fonts, CSS, JS, videos
assets/site/css/          Stylesheet
assets/site/js/           Webflow runtime + page bundles (unmodified)
assets/site/videos/       Background videos (mp4/webm) + poster frames
assets/media/              Product/location photography (second Webflow asset space)
assets/vendor/              Third-party libs (jQuery)
```

Clean URLs (`/menu`, `/store`, `/checkout`) work directly via the
`<dir>/index.html` layout — no server rewrite rules needed on any static host
(GitHub Pages, Netlify, S3, etc.).

## What's local vs. live

- HTML, CSS, JS, fonts, images, and videos are all served from this repo.
- The site's cart/checkout still talks to Webflow's live commerce backend
  (`formdata.webflow.com`, `render.webflow.com`) and Stripe (`js.stripe.com`)
  — that's the actual e-commerce backend, not something to mirror.
- External embeds/links (Tally form, Instagram, Fresto gift cards) still
  point at those third-party services, same as the live site.

## Verification

Every localized asset was checksum/size-verified against the live CDN. The
CSS's three font `url()`s were the only thing rewritten inside a binary/text
asset (to point locally instead of at Webflow's CDN); its `integrity` hash
on the `<link>` tag was recomputed to match.

## Serving locally

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000/`.
