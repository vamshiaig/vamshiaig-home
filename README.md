# vamshiaig.com

One-page corporate site for **Vamshi AIG LLP** — the entity behind [Vibe Resume](https://viberesume.in).
Pure static HTML, no build step, no dependencies. `index.html` is the whole site.

## Deploy (Vercel)

1. `git init && git add -A && git commit -m "feat: one-page vamshiaig.com site"` and push to a new
   GitHub repo (e.g. `vamshi-vadala/vamshiaig-site`).
2. Vercel → **Add New… → Project** → import the repo.
   - Framework preset: **Other**
   - Build command: *(leave empty)*
   - Output directory: *(leave empty — repo root is served)*
3. Deploy, then **Settings → Domains → Add** `vamshiaig.com` and `www.vamshiaig.com`.
4. In **Namecheap → Advanced DNS**, add the records Vercel shows:
   - `A` `@` → `76.76.21.21`
   - `CNAME` `www` → `cname.vercel-dns.com`
   Leave the existing Google Workspace **MX**, **TXT (SPF/DKIM/DMARC)** records untouched —
   adding web records does not affect mail, but deleting an MX record would.
5. Wait for Vercel to show *Valid Configuration* on both domains (usually minutes; Namecheap TTL
   can take up to an hour).

## Assets

- `logo-300.png` / `logo.svg` — the **VaiG** brand mark (caps V/G white, lowercase `ai`
  in coral `#ff8a7a` on a blue gradient). Used as the header lockup, `og:image`, and the
  favicon's accent. This is the file uploaded to the LinkedIn Page.
- `viberesume-hero.png` — Vibe Resume homepage screenshot (1002×544) leading the product card.
  Source: `vibe-resume/marketing/screenshots/Hero Page.png`.

## Editing

Everything is in `index.html` — copy, styles, and metadata. Light/dark both styled via
`prefers-color-scheme`; keep text on `--panel`/`--bg` (not on tinted accent surfaces) so contrast
stays AA.

## Claims to keep accurate

The footer states the LLP is registered in India. If you add an LLPIN, registered address, or
GST number later, put them in the footer — Indian LLPs are expected to carry entity details on
official web presence, and LinkedIn/payment-gateway verification checks look for them.
