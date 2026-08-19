# RAZFRESCO — Shopify theme

A custom theme for razfresco.com, built on the BKRSCLB design system. Dark BAKERY surfaces for the artist side, the light Store surface for anything that sells.

---

## What's in the box

```
theme/
  layout/theme.liquid          Document shell, font preload, header/footer groups
  assets/razfresco.css         All styling. Design tokens at the top.
  assets/razfresco.js          Slideshow, signup dropdown, variant picker. No dependencies.
  assets/manteka.woff2         Display font
  sections/                    17 sections, all with schema settings
  templates/                   Homepage, product, collection, cart, press, credits, contact
  config/                      Theme settings (favicon, share image)
  locales/                     Translations
```

## Install

1. **Zip the `theme` folder's *contents*** — not the folder itself. The zip must have `layout/`, `assets/`, `sections/`, `templates/`, `config/`, `locales/` at its root, or Shopify rejects it.
2. Shopify admin → **Online Store → Themes → Add theme → Upload zip file**.
3. Leave it unpublished. Click **Customize** to preview against real products.
4. When it looks right: **Actions → Publish**.

Your current theme stays untouched and can be republished at any time.

## Set up before it looks right

### Collection
The homepage band and the Shop page read a collection with the handle **`c-01`**. Confirm it exists at `razfresco.com/collections/c-01`. If the handle differs, pick the right one in Customize → Collection band → Collection.

### Pages
Create these pages in **Online Store → Pages**. The template dropdown on each page is what matters — the body content can be empty.

| Page title | Handle | Template to select |
|---|---|---|
| Press | `press` | `page.press` |
| Credits | `credits` | `page.credits` |
| Contact | `contact` | `page.contact` |

### Menus
**Online Store → Navigation → Main menu:**

- Shop → `/collections/c-01`
- Press → `/pages/press`
- Contact → `/pages/contact`

Create a **Footer menu** with your shipping and privacy policies, then select it in Customize → Footer → Footer menu.

### Hero photos
Customize → Hero slideshow. Eight empty photo blocks are waiting — add your images to each. Add or remove blocks freely; the counter follows automatically.

### Favicon and share image
Customize → Theme settings → Brand. Use the chef hat for the favicon (the graffiti logotype is illegible at 32px). Use the logotype for the share image.

### Outlet logos
Customize → Outlet logos. Nine blocks are set as text placeholders. Upload each outlet's logo to replace the text. Turn **Invert** on for white-on-black marks like Vice.

---

## Launch day

The lock lives in **two** places and both must be switched:

1. Customize → homepage → **Collection band** → uncheck **Locked**
2. Customize → a product page → **Product** → uncheck **Locked**

Until then, every Add to Cart is replaced by a waitlist form, and tiles carry a "Locked" badge.

## How the signups work

Both forms create a real Shopify customer and apply a tag:

- Hero signup → `club-member-signed-up`
- Waitlist → `c-01-waitlist`, plus `waitlist-<product-handle>` on product pages

Find them under **Customers**, filtered by tag. Export to CSV to email the list.

**The cross-platform part is not built.** A Shopify form cannot create an account on streaming.bkrsclb.com. To make one signup do both you need either:

- a webhook on Shopify's `customers/create` that calls your streaming app's signup endpoint, or
- the form posting to your app first, with the app creating the Shopify customer via the Admin API.

Until that exists, the tag is the shared key: your app can look up whether a customer carries `club-member-signed-up`.

## Editing content

Everything the design shows is a section block, so it's all drag-and-drop in Customize:

- **Press quotes** — add, delete and reorder blocks. Each has quote, outlet, date, and an optional article link. The homepage shows four; the press page shows all.
- **Credits** — each artist is a block with a name, the song, and a URL. The song appears as an overlay on hover and the tile links to the URL. Leave the song blank and no overlay shows.
- **Collaborator crawl** — one block per name. The label above links to the credits page.

## Notes

- **Fonts.** MANTEKA is embedded from `assets/manteka.woff2` and preloaded. Body copy is set in Geist with a system-font fallback; if you want Geist served properly, add it under Theme settings → Typography or self-host it the same way.
- **Product images.** The theme uses whatever images are on the products in your admin — the first image is the default, the second shows on hover. Upload front and back shots in that order.
- **Product pages** stack every product image down the left, info column sticky beside them.
- **Mobile.** Six-across becomes three on tablet and two on phones. The hero stacks.
- **Blog** templates aren't included. Add one if you start posting.
- **Pitchfork's logo** is a JPG with a white background. On the off-white logo band it reads as a faint white patch — a transparent PNG would sit cleaner.
