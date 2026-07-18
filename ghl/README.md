# GoHighLevel paste kit — exact replica of slurpramen.dk

This folder is a byte-exact rebuild of the real, live https://slurpramen.dk/ site
(Home + Menu pages only), split into the pieces GoHighLevel needs. All HTML/CSS/JS
here is the **real Webflow-generated markup**, extracted straight from the
production site and cross-checked against a fresh `curl` of the live pages — not
hand-written approximations. Assets (images, video, fonts) are referenced directly
from Webflow's live CDN, so nothing needs to be rehosted.

Explicitly excluded, per request: the Store page and all cart/checkout
functionality. The Menu page is list-view only — the gallery/grid toggle, filter
bar, and carousel are removed since only the list view was wanted.

## Paste order

### 1. Head Tracking Code (site-wide, in `<head>`)
Paste `head-tracking.html`. This is the full external stylesheet (byte-identical
to the production CSS file) plus the shared inline `<style>` block, plus the
touch-detection script that runs before anything else on the real site.

### 2. Body Tracking Code (per page, end of `<body>`)
This is **page-specific** — use a different file on each page:
- Home page → `body-tracking-home.html`
- Menu page → `body-tracking-menu.html`

These load jQuery, the shared Webflow interaction chunks, and the page's own
final JS chunk, in the same order the real site loads them. The home version also
includes the real intro-loader / scroll-header / newsletter-modal script. The
menu version deliberately omits the real site's gallery/filter/carousel script,
since that functionality isn't part of this list-view-only build, and omits the
real site's own `$('.footer').hide()` line (see "Deliberate deviations" below).

### 3. HTML/Custom Code Widgets (per page, in page-builder order)

**Home page** — add these as separate widgets, top to bottom:
1. `widgets-home/0-page-styles.html` (page-specific `<style>` — must load before the rest)
2. `widgets-home/1-nav.html`
3. `widgets-home/2-hero.html`
4. `widgets-home/3-about.html`
5. `widgets-home/4-restaurants.html`
6. `widgets-home/5-behind-the-bowl.html` (ends with the real `#contact` anchor target)
7. `widgets-home/6-footer.html`
8. `widgets-home/7-subscribe-modal.html` (newsletter popup)

**Menu page** — add these as separate widgets, top to bottom:
1. `widgets-menu/0-page-styles.html` (page-specific `<style>` — must load before the rest; contains the rule that makes the menu list visible)
2. `widgets-menu/1-nav.html`
3. `widgets-menu/2-menu-hero.html`
4. `widgets-menu/3-menu-list.html` (list view, 27 current items across 9 categories — archived items already stripped)
5. `widgets-menu/4-footer.html`

## Deliberate deviations from the real site

- **Nav**: the Store link and cart icon/drawer are removed. Everything else
  (Home, Restaurants, Behind the Bowl, Menu, Contact & Info) matches the real
  site's links exactly, including using `/#anchor` for in-page sections.
- **Menu page footer stays visible.** The real production site hides its footer
  on `/menu` via JS (`$('.footer').css('display','none')`). That's intentionally
  NOT replicated here, so Contact & Info / the footer works from the Menu page too.
- **Menu is list-view only.** The gallery/grid toggle, filter bar, and carousel
  are excluded; the `.resultados-list` is forced to its "active" (visible) state
  since the JS that would normally toggle it isn't included.
- **Store (`/store`) and cart/checkout are excluded entirely**, per request.

## Notes

- All CSS/JS/HTML here was pulled from the real production site and verified
  byte-for-byte against a live fetch, then only minimally edited (removing
  cart/store markup, splitting into files) — this is not a redesign or
  approximation.
- Video/image URLs point directly at Webflow's live CDN
  (`cdn.prod.website-files.com`), so no assets need to be uploaded to GHL.
