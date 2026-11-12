# Custom domain `secondchance.app` — what to do once you own it

Right now the site is served at **https://pablodibildox.github.io/second-chance-web/**
(GitHub Pages, `main` branch, root). Nothing below is needed until you buy
`secondchance.app`. **Don't buy anything yet.**

## 1. At your domain registrar (DNS records)

Point the apex domain at GitHub Pages. Add these records for `secondchance.app`:

**A records** (apex → GitHub Pages IPv4):
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

**AAAA records** (apex → GitHub Pages IPv6, recommended):
```
AAAA  @  2606:50c0:8000::153
AAAA  @  2606:50c0:8001::153
AAAA  @  2606:50c0:8002::153
AAAA  @  2606:50c0:8003::153
```

**CNAME for `www`** (optional, if you want www to work too):
```
CNAME  www  pablodibildox.github.io.
```

(If you'd rather use `www.secondchance.app` as the primary and redirect the apex,
set the `www` CNAME above and use `www.secondchance.app` as the custom domain in
step 2 instead of the apex.)

## 2. In this repo / GitHub

1. **Settings → Pages → Custom domain:** enter `secondchance.app` and Save.
   GitHub writes a `CNAME` file to the repo root containing `secondchance.app`.
   (Equivalently, add a file named `CNAME` at the repo root with the single line
   `secondchance.app` and push it.)
2. Wait for the DNS check to go green, then tick **Enforce HTTPS** (GitHub issues
   the TLS cert automatically; can take up to ~24 h).

## 3. In the iOS app (app repo)

Change the base host from `pablodibildox.github.io/second-chance-web` to
`secondchance.app` in **all four** value xcconfigs (the `.example` ones too):

- `SecondChance/Config.Cloud.xcconfig`
- `SecondChance/Config.Local.xcconfig`
- `SecondChance/Config.Cloud.example.xcconfig`
- `SecondChance/Config.Local.example.xcconfig`

```
PRIVACY_URL   = https:/$()/secondchance.app/datenschutz.html
IMPRESSUM_URL = https:/$()/secondchance.app/impressum.html
TERMS_URL     = https:/$()/secondchance.app/nutzungsbedingungen.html
```

(`/$()/` is the xcconfig escape for `//`, since `//` starts a comment.) The
`en/` mapping in `LegalLinks` is host-independent, so the English links follow
automatically. No Swift change needed. Clean-build and confirm the Settings →
Rechtliches links resolve.

## 4. Elsewhere

- **App Store Connect → App Privacy → Privacy Policy URL:** update to
  `https://secondchance.app/datenschutz.html`.
- **Impressum / Datenschutz / contact copy:** the website's own cross-links are
  relative, so they keep working; only absolute references (e.g. the contact-form
  endpoint stays the Supabase URL — leave it) need no change.
- Keep `pablodibildox.github.io/second-chance-web` working for a while, or add a
  redirect, so any already-shipped build's links don't break.
