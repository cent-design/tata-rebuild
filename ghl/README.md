# GoHighLevel paste kit — tata (Miami dessert kitchen)

This folder is a byte-for-byte rebuild of the live site at
https://cent-design.github.io/tata-rebuild/, split into the pieces GoHighLevel
needs. All images/videos/JS/CSS reference that live GitHub Pages site
directly, so nothing needs to be uploaded to GHL — just paste the text below.

Store and cart/checkout are excluded. The Menu page is list-view only
(no gallery/grid toggle). "Store" is replaced with an "Events" placeholder
link, and the cart is replaced with an "Order Online" button that opens a
panel with UberEats / DoorDash / direct-order links (currently placeholder
URLs — see "Known follow-ups" below).

## Paste order

### 1. Head Tracking Code (site-wide, in `<head>`)
Paste `head-tracking.html`. Contains the full site CSS (inlined), the shared
inline `<style>` block (FAQ accordion, placeholder colors), and the
touch-detection script that runs before anything else.

### 2. Body Tracking Code (per page, end of `<body>`)
Page-specific — use a different file on each page:
- Home page → `body-tracking-home.html`
- Menu page → `body-tracking-menu.html`

Loads jQuery, the shared Webflow interaction chunks, the page's own final JS
chunk, and the Order Online panel's open/close script. The home version also
includes the intro-loader / scroll-header / newsletter-modal script. The menu
version omits the gallery/filter/carousel script (not needed — list view
only) and omits the line that hides the footer on `/menu`, since Contact &
Info should stay reachable from the Menu page.

### 3. HTML/Custom Code Widgets (per page, in page-builder order)

**Home page** — add these as separate widgets, top to bottom:
1. `widgets-home/0-page-styles.html` (page-specific `<style>` — must load before the rest)
2. `widgets-home/1-nav.html`
3. `widgets-home/2-hero.html`
4. `widgets-home/3-about.html` (Our Story)
5. `widgets-home/4-restaurants.html` (Delivery Zones — pink section background)
6. `widgets-home/5-behind-the-bowl.html` (Behind the Batter, ends with the `#contact` anchor target)
7. `widgets-home/6-footer.html`
8. `widgets-home/7-subscribe-modal.html` (newsletter popup)

**Menu page** — add these as separate widgets, top to bottom:
1. `widgets-menu/0-page-styles.html` (page-specific `<style>` — must load before the rest; contains the rule that makes the menu list visible)
2. `widgets-menu/1-nav.html`
3. `widgets-menu/2-menu-hero.html`
4. `widgets-menu/3-menu-list.html` (list view, 27 current items across 9 categories — archived items already stripped, `active` class forced since the toggle JS isn't included)
5. `widgets-menu/4-footer.html`

## Deviations from the original Webflow site

- **Nav**: Store replaced with "Events" (`/events`, placeholder — no page built yet). Cart icon replaced with "Order Online", which opens a custom slide-in panel (built from scratch — the original Webflow cart JS doesn't function without a live Webflow commerce backend, which this site doesn't have).
- **Menu page footer stays visible** (the original site hides it via JS on `/menu`; kept visible here so Contact & Info still works from the Menu page).
- **Menu is list-view only.** Gallery/grid toggle, filter bar, and carousel excluded.
- **Store and checkout are excluded entirely.**

## Known follow-ups

- The "Order Online" panel's 3 links (UberEats, DoorDash, "Direct from tata")
  currently point to placeholder URLs (`ubereats.com`, `doordash.com`,
  `/order`) — swap in the real ordering links once available.
- "Events" (`/events`) has no destination page yet.
- Founder photo, hero video, restaurant videos, and Behind the Batter photos
  are all still the original Slurp ramen shop photography — no tata-specific
  media has been supplied yet.

## Notes

- Everything here was pulled from the live, verified site and only
  minimally restructured for GHL's paste fields — not a redesign.
- Asset URLs point to `https://cent-design.github.io/tata-rebuild/assets/...`
  (this repo's GitHub Pages deployment), so nothing needs to be re-uploaded
  to GHL. If that GitHub Pages site is ever taken down, these assets would
  need to be rehosted.
