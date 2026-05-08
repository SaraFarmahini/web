# Mahyar Moghimi — personal website

A static, **deployment-ready** personal site: semantic HTML, share-friendly metadata (Open Graph / Twitter / JSON-LD), security-oriented headers on major hosts, and no build step.

## Before you share the link

**1. Set your public URL for link previews (Open Graph)** — In `index.html`, every absolute URL for SEO/social should match your **stable** production address.

- **Netlify:** Use the main site URL from **Site settings → Domain** (e.g. `https://funny-unicorn-82c363.netlify.app`).  
  Do **not** use deploy-preview URLs like `https://abc123--yoursite.netlify.app`; they change every time.

If you add a **custom domain** later, search-and-replace the Netlify URL in `index.html` with your new `https://…`.

Examples if you move host:

- Custom domain: `https://mahyarmoghimi.com`
- Vercel: `https://your-project.vercel.app`
- GitHub **project** Pages: `https://username.github.io/repo-name`

On GitHub project Pages, image URLs in meta tags must include the repo path (e.g. `…/repo-name/pics/profile_pic.jpg`).

**2. CV** — Replace `assets/Mahyar_Moghimi_CV.pdf` or update the `href` in `index.html`.

**3. AutoRelate screenshots** — The site uses optimised JPEGs `pics/autorelate-screen-1.jpg` and `pics/autorelate-screen-2.jpg`. Full-size PNG exports stay on your machine only (they are gitignored). Re-export JPEGs from your `Screenshot…png` files after design changes.

## Git push troubleshooting (`RPC failed; HTTP 400`)

If `git push` over **HTTPS** fails with **400** / disconnect:

```bash
git config --global http.version HTTP/1.1
git config --global http.postBuffer 524288000
git push -u origin main
```

Or switch to **SSH** (add an SSH key in GitHub → Settings → SSH keys):

```bash
git remote set-url origin git@github.com:SaraFarmahini/web.git
git push -u origin main
```

This repository **does not** track `*.HEIC` or `pics/Screenshot*.png`, to keep pushes small (~5 MiB).

## Run locally

```bash
cd /path/to/Mahyar_Website
npm run dev
```

Or: `python3 -m http.server 8080` and open `http://localhost:8080`.

## Project layout

| Path | Purpose |
|------|--------|
| `index.html` | Page content + SEO / social meta + Person JSON-LD |
| `css/styles.css` | Layout and visual design |
| `js/main.js` | Mobile nav, in-page scrolling |
| `favicon.svg` | Browser tab icon |
| `site.webmanifest` | Name, theme colours (install / PWA hints) |
| `robots.txt` | Allow all crawlers |
| `netlify.toml` | Netlify publish + cache + security headers |
| `vercel.json` | Vercel security + cache headers |
| `package.json` | `npm run dev` local preview |
| `pics/` | Photos |
| `assets/` | CV PDF |

## Deploy (production)

### Vercel

1. Push this folder to a Git repository or run `npx vercel` from the project root.
2. Framework: **Other**; output / root: repository root; build command: empty.
3. `vercel.json` applies headers automatically.

### Netlify

1. Drag-and-drop the folder or connect Git; publish directory: **`/`** (root).
2. `netlify.toml` sets `publish = "."` and headers.

### GitHub Pages

1. Push the repo. **Settings → Pages →** deploy from branch, folder **`/` (root)**.
2. If the site is **`https://user.github.io/repo/`**, complete the URL replacements in `index.html` (include the `/repo` segment in absolute image and canonical URLs).

---

Social and messaging previews read **Open Graph** tags from the **live** URL. After each deploy, use your host’s tools or [opengraph.xyz](https://www.opengraph.xyz/) to verify previews once the URL is final.
