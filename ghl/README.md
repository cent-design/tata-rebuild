# Slurp — GoHighLevel head/body/widget pieces

A faithful duplicate of [slurpramen.dk](https://slurpramen.dk) (home + menu
only — store and cart/checkout intentionally excluded), split into the
pieces GoHighLevel actually asks for instead of full standalone pages.

## Where each piece goes

- **`head-tracking.html`** — paste into the site's **Head Tracking Code**
  field (site-wide setting). Contains all CSS in a single `<style>` block —
  colors, the custom Altpicaro font (loaded from the live Webflow CDN),
  layout, and responsive rules. Only needs to be pasted once for the whole
  site, not per page.
- **`body-tracking.html`** — paste into the site's **Body/Footer Tracking
  Code** field (site-wide setting). Contains one `<script>` block: mobile
  nav toggle, FAQ accordion, and newsletter-form-reveal behavior. Also only
  needs to be pasted once.
- **`widgets/*.html`** — each file is one **HTML/Custom Code widget**,
  dropped into the page builder canvas as its own element. No `<style>` or
  `<script>` tags inside these — they rely entirely on the two tracking
  code snippets above.

## Page layout

**Home page** — widgets in this order:
1. `widgets/nav.html`
2. `widgets/hero.html`
3. `widgets/about.html`
4. `widgets/restaurants.html`
5. `widgets/behind-the-bowl.html`
6. `widgets/footer.html`

**Menu page** — widgets in this order:
1. `widgets/nav.html`
2. `widgets/menu-hero.html`
3. `widgets/menu-list.html`
4. `widgets/footer.html`

`nav.html` and `footer.html` are identical on both pages — same two widget
files, just placed on each page.

## Notes

- All images/video reference the live `cdn.prod.website-files.com` URLs
  from slurpramen.dk directly — nothing rehosted. All 25 asset URLs were
  verified to return 200 before committing.
- Nav has 5 items: Home, Restaurants, Behind the Bowl, Menu, Contact & Info.
  No Store, no cart/checkout — both were dropped per instructions, not just
  hidden.
- The "Restaurants," "Behind the Bowl," and "Contact & Info" nav links
  point to `/#restaurant`, `/#behind`, `/#contact` (leading slash) rather
  than bare `#anchor`, so they resolve correctly from the Menu page too —
  Home page for `/#restaurant` and `/#behind` (only exist there), and
  either page for `/#contact` (footer is on both).
- Menu lists only "Current" items (27), not the archived/retired ones.
