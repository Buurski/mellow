# Restaurant Mellow, Lemvig — demo-site (prospekt)
Enkeltside-HTML i `index.html` (al CSS i `<style>`, al JS i `<script>`, intet framework/build). Live https://mellow-gold.vercel.app · GitHub `Buurski/mellow` · Vercel-projekt `mellow`.
Kunde: Natasja (ejer, mail@restaurantmellow.dk), Ismael (medejer, SMS). Demo sendt, intet svar; status i kundenoten.
Hårde regler: `C:\Users\Buur\Documents\KnowledgeOS\context\hard-rules.md` (læs først). Router: `C:\Users\Buur\Documents\Websites\AGENTS.md`.

## Opgave | læs | læs IKKE
KB = `C:\Users\Buur\Documents\KnowledgeOS`. Gæt aldrig et faktum; står det ikke her eller i filen, skriv "ved ikke".

| Opgave | læs | læs IKKE |
|---|---|---|
| Tekst/indhold på siden | `index.html`, `KB\wiki\kunder\mellow.md`, `KB\context\brand-og-tone.md` | `C:\Users\Buur\_Arkiv`, andre kunders sites |
| Design/CSS | `DESIGN-SYSTEM.md` (kilde til tokens, klasser, breakpoints), `index.html` | nye farver/skrifter udenfor tokens |
| SEO | `index.html` (title, meta, schema), `KB\wiki\kunder\mellow.md` | generiske SEO-skabeloner uden at tjekke siden |
| Deploy | `C:\Users\Buur\Documents\Websites\AGENTS.md`, `KB\wiki\os\agents-detaljer.md` (afsnit "Deploy-disciplin") | `.vercel\` (projekt-id, rør ikke) |
| Kinly-priser, startpris, tilbud | `KB\context\priser.md` (kanon; hjemmeside fra 3.997 kr) | gamle tilbud i wiki; individuelle aftaler afviger |
| Kundefakta, kontakt, status, log | `KB\wiki\kunder\mellow.md` | `C:\Users\Buur\Documents\Kunder\`, `.send_queue\` |
| Adresser (kunder, bl.a. Ikast Autoservice), tværgående fakta (Planuko-wordmark, HQ-gates, modelvalg) | `KB\context\fakta.md` | Lucas' privatadresse må aldrig stå nogen steder |
| Selskab, CVR, adresseregel | `KB\context\selskab.md` | |
| Mails/udgående tekst til kunden | `KB\context\brand-og-tone.md`, `KB\context\forbidden-phrases.md` | |
| Alle repos og sites | `C:\Users\Buur\Documents\REPOS.md`, `C:\Users\Buur\Documents\Websites\SITES.md` | |

## Kommandoer
Ingen `package.json`, ingen build, ingen `verify`-script.
- Dev: `python -m http.server 8080` i repo-roden → http://localhost:8080
- Deploy: kun Lucas merger til `main` (GitHub→Vercel auto-deploy). `vercel deploy --prod` kun efter Lucas' ja.

## Arkitektur (kort)
- `images/` (logobrown/logowhite, gallery1-4 m.fl.), `video/herovideo.mp4`, `Mellow-A-la-Carte-og-vinkort.pdf` (linkes fra siden).
- Tokens i `:root`: `--c-cream`, `--c-dark`, `--c-accent` (#C9A96E, eneste guld), `--c-cta`, `--f-display` (Playfair Display), `--f-body` (Outfit), `--ease`. Afvig aldrig.
- JS: nav `is-loaded`/`is-scrolled` (>60px, logo brun→hvid), scroll-reveal (IntersectionObserver `.reveal*` → `.is-in`), galleri (`#galleryTrack`, 300vh, 7 slides, 3 synlige, 5 positioner), brunch-parallax, mobil-burger ≤1040px.
- Sektioner: nav → hero (60/40, video venstre) → selskaber (mørk) → info-strip → menu → galleri → citat → brunch → events → footer.

## Regler
1. Aldrig `main` uden Lucas: ny gren + Vercel-preview, Lucas merger. Samler ændringer; maks 2-3 prod-deploys/dag; `[skip vercel]` ved docs.
2. "Done" = live-check: åbn preview/prod og print HTTP-status eller screenshot; ikke kun "ser rigtigt ud i koden".
3. Udgående (mails, SMS, opslag til Natasja/Ismael) er KLADDER; Lucas sender selv. Intet sendes, ingen konti, køb eller DNS.
4. Dansk. Ingen AI-slop (ingen gradient-blobs, emoji-ikoner, fyldtekst). Selskaber skal forblive fremtrædende; palet kun beige/varm brun.
5. Én kode-agent pr. worktree; commit med eksplicit `git add <sti>`, aldrig `git commit -a`; ingen stash/reset/clean.
