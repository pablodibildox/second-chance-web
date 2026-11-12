# Second Chance — website

Legal pages and the DSA contact form for the **Second Chance** iOS app
(a map of free "zu verschenken" giveaway boxes in Aachen).

Live at **https://pablodibildox.github.io/second-chance-web/** (GitHub Pages,
`main` branch, root).

- `index.html` / `en/index.html` — landing page + contact/report form (DE / EN)
- `datenschutz.html` / `en/privacy.html` — privacy policy (German is authoritative)
- `nutzungsbedingungen.html` / `en/terms.html` — terms of use
- `impressum.html` / `en/imprint.html` — imprint (§ 5 DDG)
- `style.css`, `fonts/` — pixel-art styling (Fusion Pixel 10px, OFL)
- `.nojekyll` — serve files as-is (no Jekyll processing)

## Source of truth

These files are **generated from the app repo's `website/` directory**, which
lives next to the legal drafting + review notes (`docs/legal/`). Edit there and
re-deploy here — don't diverge. To redeploy after changing `website/` in the app
repo:

```bash
# from the app repo root
rsync -a --delete --exclude='.git' --exclude='.nojekyll' --exclude='DNS.md' --exclude='README.md' \
  website/ /path/to/second-chance-web/
cd /path/to/second-chance-web && git add -A && git commit -m "sync website" && git push
```

The contact form POSTs to the live Supabase Edge Function `report-content`
(absolute URL in `index.html`), so it works from any origin.

## Custom domain

See [`DNS.md`](DNS.md) for moving to `secondchance.app` when that domain is bought.
