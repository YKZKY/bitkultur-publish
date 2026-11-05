# BitKultur Learning — magyar tudástár

Cél: https://lrn.bitcultur.com/hu/

## Szerkezet
- `hu/index.html` — mobilbarát, kereshető tudástár
- `hu/cikkek/*/index.html` — önképzési mintacikkek
- `data/articles.json` — keresési index, téma, sorozat és metaadatok
- `hu/lexikon/` — fogalomtár
- `CNAME` — lrn.bitcultur.com
- `.github/workflows/pages.yml` — GitHub Pages Actions telepítés

## Biztonság
Nincsenek tokenek vagy titkos konfigurációk. Nem aktiváltunk VPS-alkalmazást, LLM API-t vagy automatikus Telegram-publikálást. A mintacikkek a tulajdonos szerkesztői felülvizsgálatáig nem tekinthetők jóváhagyott végleges anyagnak.

## Közzététel
GitHub-repository: `YKZKY/bitkultur-publish`. Állítsd be a Settings > Pages > Source: GitHub Actions opciót. A HTTPS csak a GitHub Pages-domain hozzárendelése és a tanúsítvány élesítése után lesz érvényes.
