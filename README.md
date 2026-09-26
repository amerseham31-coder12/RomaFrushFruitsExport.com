# Roma Fresh Fruit Export — Website

Production-ready source for the Roma Fresh Fruit Export marketing site:
a cinematic hero, a bilingual-ready product catalog (Fruits/Vegetables,
7 languages), an interactive Egypt → World export map, and an inquiry
form — all in one self-contained page.

**Live structure:** this is a static HTML site — plain HTML, CSS and
JavaScript, no framework, no build tool, no server. All images, video,
fonts (aside from Google Fonts) and the logo are embedded directly
inside `index.html`, so there is nothing else to upload, link, or lose
along the way. That's also why the file itself is large (~7 MB) — it's
one file doing the work of a whole `assets/` folder.

## Project contents

```
Roma-Fresh-Fruit-Website/
├── index.html        The entire website (markup, styles, scripts, media)
├── 404.html           Friendly not-found page that redirects to index.html
├── netlify.toml        Netlify build & redirect configuration
├── package.json        Minimal manifest (no real dependencies — see below)
├── .env.example         Documents that no environment variables are needed
├── .gitignore
└── README.md            This file
```

## Deploying to Netlify

You don't need Node, npm, or a build step for this site to work — but the
project includes a `package.json` and a no-op build script so
`npm install && npm run build` complete without errors if your workflow
expects them.

### Option A — Drag and drop (fastest)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the `Roma-Fresh-Fruit-Website` folder onto the page.
3. Done — Netlify gives you a live URL immediately.

### Option B — GitHub → Netlify (recommended for ongoing edits)
1. Push this folder to a new GitHub repository.
2. In Netlify: **Add new site → Import an existing project → GitHub** →
   select the repo.
3. Netlify auto-detects `netlify.toml`. Confirm these settings if asked:
   - **Build command:** `echo "Static site — no build step required"`
     (or leave blank)
   - **Publish directory:** `.`
   - **Node version:** not required by this project; any default Netlify
     offers (18 or 20) is fine.
4. Click **Deploy site**.

No environment variables are required (see `.env.example`).

## What's already handled for you

- `netlify.toml` publishes the site and adds a catch-all redirect to
  `index.html`, so a shared link or a hard refresh never 404s.
- `404.html` is a branded fallback for the rare case a redirect is bypassed.
- Security-friendly default headers (`X-Frame-Options`,
  `X-Content-Type-Options`, `Referrer-Policy`).
- The only external network call the page makes is to Google Fonts
  (`fonts.googleapis.com` / `fonts.gstatic.com`) for the Manrope, Inter
  and Tajawal typefaces. Everything else — every product photo, the
  logo, the hero video, icons — is embedded in the file itself, so
  nothing can end up "missing" after deployment.

## Editing the site

Since everything lives in one file, here's where to find things inside
`index.html` if you want to make changes yourself later:

| What you want to change | Search for |
|---|---|
| Company name in browser tab / SEO description | `<title>` and `<meta name="description"` near the top |
| Colors, fonts, spacing | the `:root { ... }` CSS variables near the top of `<style>` |
| Logo | `nav-logo` (there are 3 uses: header, mobile menu, footer) |
| Hero video / slideshow images | `hero-video`, `hero-slide`, and the base64 payload in the `<script type="text/plain" id="hero-video-b64">` tag near the end of the file |
| Product photos, names, descriptions (all 7 languages) | `PRODUCT_PHOTOS`, `PRODUCT_GRADS`, and the `I18N` object (one block per language: `en`, `ar`, `fr`, `de`, `ru`, `zh`, `tr`) |
| Contact details (phone / address / email / WhatsApp) | search for the current phone number or `class="c-addr"` |
| Egypt map / world map routes | the `<svg class="egypt-svg">` / `<svg class="world-svg">` blocks and the `#reach`, `#egypt-card` sections |
| Inquiry form fields | `<form` near `id="b2b"` |

Because the file is large, use your editor's search rather than
scrolling, and always keep a backup copy before making direct edits.

## Local preview before deploying

No install needed — any static file server works:

```bash
npx --yes serve .
# or
python3 -m http.server 8080
```

Then open the printed local URL in your browser.

## Browser support notes

- The cinematic hero plays an embedded MP4. All current desktop and
  mobile browsers (Chrome, Safari, Firefox, Edge) support this natively.
  If a visitor's browser can't play it (very old browsers, or autoplay
  blocked by a data-saver setting), the site automatically falls back to
  a smooth cross-fading photo slideshow — nothing breaks either way.
- `prefers-reduced-motion` is respected throughout (hero, maps, card
  hovers, modal transitions) for visitors who've asked their OS for
  reduced motion.
- Fully responsive from small phones up through large desktop screens,
  including right-to-left layout when the visitor switches the language
  selector to Arabic.

## Before you go live — quick checklist

Everything below has already been verified against this build, but
worth a last look after your own deploy:

- [ ] Open the live Netlify URL and confirm the hero video/slideshow,
      logo, and fonts load.
- [ ] Click through every item in the Products mega-menu and the
      Fruits/Vegetables tabs — 13 fruits, 10 vegetables.
- [ ] Open a product card and confirm the modal image and details match.
- [ ] Scroll to **Global Reach** and **Contact** and confirm the map
      animates and the phone/address are correct.
- [ ] Switch the language selector (top right) through a couple of
      languages and re-check the pages above.
- [ ] Resize the browser (or check on an actual phone) to confirm layout
      holds at mobile, tablet, and desktop widths.
