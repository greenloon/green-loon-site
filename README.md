# Green Loon Capital — Marketing Site

A single-page marketing site for **Green Loon Capital**, a boutique advisory
firm focused on energy, infrastructure, and industrial decarbonization.

Built with plain HTML and **Tailwind CSS via the Play CDN** — no build step, no
dependencies. It's one file (`index.html`) plus a logo.

## View it

Just open the file in a browser:

```bash
open index.html
```

Or serve it locally (recommended — some browsers treat `file://` differently):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Logo & icons

The original supplied logo (`assets/logo.jpeg`, a dark-green loon on white) is
kept as the source. The transparent assets used by the site are derived from it
with ImageMagick:

- **`assets/logo-light.png`** — the loon recolored cream with its natural dark
  markings showing through; floats directly on the dark hero/nav/footer (no
  white box). This is the visible site logo.
- **`assets/logo-mark.png`** — dark-green loon, transparent background, for use
  on light surfaces (and the light-tab favicon).
- **Favicons:** `favicon.ico` + `favicon-32.png` (dark loon, light tabs) and
  `favicon-32-light.png` (cream loon, dark-mode tabs, via `prefers-color-scheme`).
- **Mobile / app icons:** `apple-touch-icon.png` (180), `icon-192.png`,
  `icon-512.png` — a branded dark-green tile with the cream loon — plus
  `site.webmanifest`.

To regenerate after replacing `logo.jpeg`, the commands are recorded in git
history; the key one is `magick logo.jpeg -fuzz 18% -transparent white …`.

## Contact form

The contact form POSTs to Formspree:

```
https://formspree.io/f/mvzykwye
```

> Note: the endpoint originally provided was doubled
> (`https://formspree.io/f/https://formspree.io/f/mvzykwye`); the corrected
> form ID is used above. On the **first** submission Formspree emails the form
> owner to confirm the endpoint — do that once and submissions will flow.

## Customizing

Everything lives in `index.html`:

- **Colors** — defined in the `tailwind.config` block in the `<head>`
  (`forest`, `loon`, `cream`). Change them in one place and they apply
  site-wide.
- **Copy** — each section (hero, about, services, contact) is plainly labeled
  with an HTML comment.
- **Fonts** — Fraunces (display) + Inter (body), loaded from Google Fonts.

## A note on the Tailwind Play CDN

The Play CDN ships the entire Tailwind engine to the browser and compiles
classes on the fly. That's perfect for a no-build prototype like this, but it
adds load time and prints a "not for production use" warning in the console.
When you're ready to ship for real, the production path is to install Tailwind
and build a small static CSS file containing only the classes you actually use:

```bash
npx tailwindcss -i input.css -o assets/styles.css --minify
```

…then replace the `<script src="https://cdn.tailwindcss.com">` tag with
`<link rel="stylesheet" href="assets/styles.css">`. Smaller, faster, no warning.

## Deploy

It's a static site — drag the folder onto any static host (Netlify, Cloudflare
Pages, GitHub Pages, etc.). No server or build configuration required.
