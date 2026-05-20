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

## Add your logo

Drop your logo at **`assets/logo.png`**. Until that file exists, the site shows
a built-in inline-SVG loon mark so nothing looks broken. A transparent PNG or
SVG (~200px tall or larger) looks best on the dark background. See
`assets/README.txt` for details.

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
