# Malvern Financial — static site

Single-page marketing site for [Malvern Financial](https://www.malvernfinancial.com), rebuilt from the former Wix site for **GitHub Pages**.

## Local preview

From this directory:

```bash
# Python
python3 -m http.server 8080

# or Node
npx --yes serve -l 8080
```

Open <http://localhost:8080> and check Home → Services → Mission → About → Contact, plus mobile nav.

## Site structure

```
index.html          # one-pager (#home #services #mission #about #contact)
404.html            # friendly not-found → home
CNAME               # www.malvernfinancial.com
robots.txt
sitemap.xml         # / only (no /map)
css/styles.css
js/main.js
assets/             # logos, hero, strips, headshot, icons (JPEG + WebP)
```

## Decisions in this build

- **No contact form** — Contact shows `mailto:ryan@malvernfinancial.com` and `tel:+14843330968` only.
- **About photo** — Ryan’s current headshot (`assets/ryan-yurkanin.jpg` / `.webp`), not the old Wix image.
- **Footer social** — LinkedIn only: <https://www.linkedin.com/in/ryan-yurkanin-8aba0b6>
- **Dropped** — `/map` Wix template page; Twitter / Wix placeholder social destinations.
- **Mission pillars** — “Working with you to stay within budget…” under **Budget Friendly**; project-results line under **Project Driven**; full-service line under **Full Service**.

## GitHub Pages cutover

1. Create a GitHub repo and push this folder (do **not** commit secrets; this tree is static-only).
2. **Settings → Pages**: deploy from the branch that holds these files (root, or `/docs` if you nest them).
3. Confirm the `CNAME` file (`www.malvernfinancial.com`) is present so Pages issues HTTPS for the custom domain.

### DNS (Google Cloud Domains → GitHub Pages)

Domain DNS is currently on **Google Cloud Domains** and points at **Wix**. For Pages:

| Record | Host | Value |
|--------|------|--------|
| `A` | `@` (apex) | GitHub Pages IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| `AAAA` (optional) | `@` | GitHub Pages IPv6 equivalents (see [GitHub Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)) |
| `CNAME` | `www` | `<user-or-org>.github.io` |

Remove the old **Wix** A / CNAME records when you cut over. In the GitHub repo Pages settings, set custom domain to `www.malvernfinancial.com` and enable **Enforce HTTPS** after the certificate provisions.

Apex → www: keep a redirect (Google Domains forwarding, or Pages apex + www both configured) so `malvernfinancial.com` continues to land on `www`.

### Keep Mailgun (email)

Mail for `ryan@malvernfinancial.com` uses **Mailgun** (`mxa` / `mxb.mailgun.org` and SPF `include:mailgun.org`). When changing A/CNAME for hosting:

- **Do not** delete or overwrite MX, TXT (SPF/DKIM), or other mail-related records.
- Only change web hosting records (A / AAAA / www CNAME).
- After cutover, send a test message to `ryan@malvernfinancial.com` before canceling Wix.

### After go-live

- Export any useful contacts from Wix CRM before canceling the Wix plan.
- Spot-check mailto / tel / LinkedIn, favicon, and mobile layout.
- Optional later: privacy page, analytics, or a form endpoint if Ryan wants lead capture again.

## Brand tokens

- Fonts: Noticia Text (wordmark), Raleway (headings), Open Sans (body)
- Navy `#00305B`, CTA `#0F4C85`, logo green `#18A44B`, hero card soft green
