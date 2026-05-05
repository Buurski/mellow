# Mellow — Designsystem

Baseret på Under Klippens struktur og animationer, tilpasset Mellows identitet: beige-domineret, blød og uformel i tonen, med stærkt fokus på selskaber og events.

---

## Tone og stemning

> "Styr på tingene, men stemningen må gerne være blød, rolig og uformel."

Sproget på sitet er hverken stift eller uorganiseret. Det er varmt, imødekommende og afslappet — præcis som beigen i farvepaletten. Teksten taler direkte til gæsten uden formalia.

**Mellows to primære budskaber:**
1. **Selskaber og events** — bryllupper, samkomster, firmafester, fødselsdagsfester op til 300 gæster
2. **À la carte-menuen** — Mellows daglige madprofil og identitet

Begge skal have fremtrædende plads på forsiden. Selskabssektionen sidder senest som anden eller tredje sektion.

---

## Farvepalette

### Princippet
Under Klippen bruger mørk brun som primær baggrund med beige som lys kontrast.
Mellow vender det om: **beige er grundtonen**, og brun er kun til CTA-knapper, footer og tynde accentlinjer — aldrig som sektionsbaggrund.

```css
:root {
  /* Primær baggrund — beige dominerer hele oplevelsen */
  --c-cream:        #F5F0E8;
  --c-cream-warm:   #EDE8DF;

  /* Tekst */
  --c-ink:          #2B1A0A;
  --c-ink-soft:     #6B5240;
  --c-light-text:   #FAF7F2;

  /* Mørke sektioner — footer, drawer, mørke baggrunde */
  --c-dark:         #2B1A0A;
  --c-mid:          #3D2510;

  /* Guld — bruges KUN i selskaber/bryllupssektionen + dekorative elementer */
  --c-accent:       #C9A96E;

  /* Brun — KUN CTA-knapper, footer og tynde accentlinjer. ALDRIG sektionsbaggrund */
  --c-cta:          #5D3B0D;

  /* Borders og linjer */
  --c-rule:         rgba(43, 26, 10, 0.12);   /* på beige baggrund */
  --c-rule-light:   rgba(250, 247, 242, 0.18); /* på mørk baggrund */
}
```

### Farveregel — vigtig
- `--c-cta` (#5D3B0D) bruges **aldrig** som sektionsbaggrund
- `--c-accent` (#C9A96E) er guldfarven til selskaber, bryllup, separatorlinjer, ikoner
- Beige (#F5F0E8) er grundtonen og sætter stemningen for hele oplevelsen

---

## Typografi

Display-fonten bør være blødere og mere afrundet end Cormorant Garamond — fx **Playfair Display**, **Lora** eller **Libre Baskerville**. Body-fonten kan være **Outfit** eller lignende neutralt grotesk.

```css
:root {
  --f-display: "Playfair Display", "Lora", Georgia, serif;
  --f-body:    "Outfit", -apple-system, "Helvetica Neue", sans-serif;
}
```

### Typografiskala

| Klasse | Font | Størrelse | Vægt | Letter-spacing | Transform | Brug |
|---|---|---|---|---|---|---|
| `h1` / `.display` | display | clamp(36px, 5.4vw, 72px) | 300 | — | — | Hero-overskrifter |
| `h2` | display | clamp(40px, 5vw, 64px) | 300 | — | — | Sektionsoverskrifter |
| `h3` | display | 28px | 300 | — | — | Underoverskrifter |
| `.eyebrow` | body | 11px | 400 | 0.22em | UPPERCASE | Kategori-labels |
| `.body-lg` | body | 18px | 300 | — | — | Manchetafsnit |
| `.body` | body | 15px | 400 | — | — | Brødtekst |
| `.caption` | body | 12px | 300 | 0.04em | — | Billedtekster |

**Særlige typografimønstre:**
- `.eyebrow`: 11px, uppercase, 0.22em letter-spacing, farve: `--c-accent`
- `text-wrap: balance` på display-overskrifter
- `text-wrap: pretty` på `.body-lg`
- Kursiv til stemning: display-font, vægt 300–400

---

## Navigation

Fast navigation øverst, højde 76px. Glaseffekt med beige baggrund.

```css
:root {
  --nav-h: 76px;
}

.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: var(--nav-h);
  z-index: 100;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 0 40px;
  background: rgba(245, 240, 232, 0.92);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  border-bottom: 1px solid var(--c-rule);
  transition: background 0.4s var(--ease);
}

/* Mørk variant — til mørke sektioner */
.nav.is-dark {
  background: rgba(43, 26, 10, 0.92);
  border-bottom-color: var(--c-rule-light);
}

/* Indlæsningsanimation */
.nav {
  opacity: 0;
  transform: translateY(-12px);
  transition: opacity 0.7s var(--ease), transform 0.7s var(--ease);
}
.nav.is-loaded {
  opacity: 1;
  transform: none;
}
```

**Navigationslinks — hover-understregning:**
```css
.nav-link {
  position: relative;
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.nav-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0; right: 0;
  height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s var(--ease);
}
.nav-link:hover::after {
  transform: scaleX(1);
}
```

**Burger vises ved ≤1040px.**

---

## Hero — video til venstre, logo til højre

Omvendt fra Under Klippen. Venstre side: video med overlay og tagline. Højre side: beige baggrund med logo og tekst.

```html
<section class="hero" data-tone="dark">
  <div class="hero-left">
    <video autoplay muted loop playsinline>
      <source src="video/hero.mp4" type="video/mp4">
    </video>
    <div class="hero-overlay"></div>
    <p class="hero-tagline">Blød stemning. Godt selskab.</p>
    <div class="scroll-cue">
      <div class="scroll-arrow"></div>
    </div>
  </div>
  <div class="hero-right reveal">
    <img src="billeder/mellow-logo.svg" alt="Mellow" class="hero-logo">
    <p class="eyebrow">Restaurant & Selskaber</p>
    <p class="body-lg">Åben for alle — og klar til din fest.</p>
    <a href="#selskaber" class="btn-outline">Se selskabsmuligheder</a>
  </div>
</section>
```

```css
.hero {
  display: grid;
  grid-template-columns: 60fr 40fr;
  min-height: 100svh;
}

.hero-left {
  position: relative;
  overflow: hidden;
}

.hero-left video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(43, 26, 10, 0.18),
    transparent 30%,
    transparent 70%,
    rgba(43, 26, 10, 0.42)
  );
}

.hero-tagline {
  position: absolute;
  bottom: 28px;
  left: 40px;
  right: 40px;
  font-family: var(--f-display);
  font-size: 22px;
  font-style: italic;
  color: var(--c-light-text);
  text-shadow: 0 2px 24px rgba(0, 0, 0, 0.6);
  animation: heroIn 1.2s var(--ease) 0.9s both;
}

.hero-right {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  padding: 60px 48px;
  background: var(--c-cream);
  gap: 24px;
  animation: heroIn 1.2s var(--ease) 0.45s both;
}

@media (max-width: 880px) {
  .hero {
    grid-template-columns: 1fr;
  }
  .hero-left {
    aspect-ratio: 4 / 3;
    min-height: 0;
  }
  .hero-right {
    padding: 48px 24px;
  }
}
```

---

## Animationer og overgange

```css
:root {
  --ease:   cubic-bezier(0.33, 1, 0.68, 1);
  --t-fast: 0.3s var(--ease);
  --t-slow: 0.7s var(--ease);
}

@keyframes heroIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

@keyframes scrollArrow {
  0%   { opacity: 0; transform: translateY(-20px); }
  40%  { opacity: 1; transform: translateY(0); }
  100% { opacity: 0; transform: translateY(20px); }
}
```

### Scroll-reveal

```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.7s var(--ease), transform 0.7s var(--ease);
}
.reveal.is-in {
  opacity: 1;
  transform: none;
}

/* Stagger-forsinkelser via data-attribut */
.reveal[data-delay="1"] { transition-delay: 0.08s; }
.reveal[data-delay="2"] { transition-delay: 0.16s; }
.reveal[data-delay="3"] { transition-delay: 0.24s; }
.reveal[data-delay="4"] { transition-delay: 0.32s; }
```

### Hover-overgange

```css
/* Billeder */
.pair-frame img {
  transition: transform 1.2s var(--ease);
}
.pair-frame:hover img {
  transform: scale(1.03);
}

/* Knapper med pil */
.btn-ghost .arrow {
  width: 28px;
  transition: width 0.3s var(--ease);
}
.btn-ghost:hover .arrow {
  width: 44px;
}
```

---

## Scroll-cue (pil-animation)

```html
<div class="scroll-cue">
  <div class="scroll-arrow"></div>
</div>
```

```css
.scroll-arrow {
  width: 1px;
  height: 38px;
  background: linear-gradient(to bottom, transparent, var(--c-light-text));
  animation: scrollArrow 2.4s var(--ease) infinite;
}
```

---

## Sektionslayout og grid

### Sektionsafstand

```css
.section-pad    { padding: 140px 0; }
.section-pad-sm { padding: 96px 0; }
```

### Max-bredder

```css
.col-narrow   { max-width: 640px;  margin-inline: auto; }
.col-medium   { max-width: 720px;  margin-inline: auto; }
.col-wide     { max-width: 1100px; margin-inline: auto; }
.col-full     { max-width: 1200px; margin-inline: auto; }
```

### Info-strip (3 kolonner med borders)

```css
.info-strip {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  border-top: 1px solid var(--c-rule);
  border-bottom: 1px solid var(--c-rule);
}
.info-strip > * {
  padding: 48px 40px;
  border-right: 1px solid var(--c-rule);
}
.info-strip > *:last-child { border-right: none; }

@media (max-width: 720px) {
  .info-strip { grid-template-columns: 1fr; }
  .info-strip > * { border-right: none; border-bottom: 1px solid var(--c-rule); }
}
```

### Billedpar med offset

```css
.pair {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.pair-frame {
  aspect-ratio: 4 / 5;
  overflow: hidden;
}
.pair-frame img {
  width: 100%; height: 100%;
  object-fit: cover;
  display: block;
}

/* Offset-varianter */
.pair.offset-left  .pair-frame:first-child { margin-top: 80px; }
.pair.offset-right .pair-frame:last-child  { margin-top: 80px; }

@media (max-width: 880px) {
  .pair { grid-template-columns: 1fr; }
  .pair.offset-left  .pair-frame:first-child,
  .pair.offset-right .pair-frame:last-child { margin-top: 0; }
}
```

### Events/selskaber-grid

```css
.events-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  border-top: 1px solid var(--c-rule);
}
.event-card {
  padding: 48px 40px;
  border-right: 1px solid var(--c-rule);
  transition: background 0.3s var(--ease);
}
.event-card:last-child { border-right: none; }
.event-card:hover { background: rgba(201, 169, 110, 0.05); }

/* Dato-styling med guldaccent */
.event-card .date {
  font-family: var(--f-display);
  font-size: 56px;
  font-style: italic;
  color: var(--c-accent);
}
.event-card .month {
  font-size: 11px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--c-accent);
}

@media (max-width: 880px) {
  .events-grid { grid-template-columns: 1fr; }
  .event-card  { border-right: none; border-bottom: 1px solid var(--c-rule); }
}
```

### Menukort (2 kolonner)

```css
.set-menus {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  max-width: 1100px;
  margin-inline: auto;
  border: 1px solid var(--c-rule);
}
.menu-card {
  padding: 36px;
  border-right: 1px solid var(--c-rule);
  transition: background 0.4s ease;
}
.menu-card:last-child { border-right: none; }
.menu-card:hover { background: var(--c-cream-warm); }

@media (max-width: 880px) {
  .set-menus { grid-template-columns: 1fr; }
  .menu-card { border-right: none; border-bottom: 1px solid var(--c-rule); }
}
```

### Footer

```css
.footer {
  background: var(--c-dark);
  color: var(--c-light-text);
  padding: 80px 0 40px;
}
.footer-grid {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 64px;
  max-width: 1200px;
  margin-inline: auto;
  padding-inline: 40px;
}
.footer h4 {
  font-size: 11px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--c-accent);
  margin-bottom: 20px;
}
.footer a {
  color: rgba(250, 247, 242, 0.7);
  transition: color 0.3s;
}
.footer a:hover { color: var(--c-light-text); }

@media (max-width: 880px) {
  .footer-grid { grid-template-columns: 1fr 1fr; gap: 40px; }
}
@media (max-width: 600px) {
  .footer-grid { grid-template-columns: 1fr; }
}
```

---

## Knapper

```css
/* CTA-knap — brun (#5D3B0D) er eneste brug af brun som baggrund */
.btn-solid {
  display: inline-flex;
  align-items: center;
  height: 52px;
  padding: 0 28px;
  background: var(--c-cta);
  color: var(--c-light-text);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  transition: opacity var(--t-fast);
}
.btn-solid:hover { opacity: 0.85; }

/* Outline-knap */
.btn-outline {
  display: inline-flex;
  align-items: center;
  height: 38px;
  padding: 0 20px;
  border: 1px solid currentColor;
  font-size: 11px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  transition: background var(--t-fast), color var(--t-fast);
}
.btn-outline:hover {
  background: var(--c-ink);
  color: var(--c-light-text);
}

/* Ghost-knap med animeret pil */
.btn-ghost {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  font-size: 11px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
}
.btn-ghost .arrow {
  width: 28px;
  height: 1px;
  background: currentColor;
  transition: width 0.3s var(--ease);
}
.btn-ghost:hover .arrow { width: 44px; }
```

---

## Breakpoints

```css
@media (max-width: 1180px) {
  /* Nav: reducer link-afstand og skriftstørrelse */
}

@media (max-width: 1040px) {
  /* Burger vises, nav-links skjules */
}

@media (max-width: 880px) {
  /* 2-kolonne → 1-kolonne overalt */
  /* Footer-grid: 4-kol → 2-kol */
  /* Events-grid: 3-kol → 1-kol */
  /* Hero: split → stablet */
}

@media (max-width: 720px) {
  /* Info-strip: 3-kol → 1-kol */
}

@media (max-width: 600px) {
  /* Footer: 2-kol → 1-kol */
  /* Mindre padding */
}
```

---

## Selskaber og events — designprioriteter

Dette er Mellows vigtigste forretningsområde og skal kommunikeres tydeligt fra første scroll.

**Hvad sektionen skal indeholde:**
- Kapacitet op til **300 gæster** som fremhævet USP
- Typer: bryllupper, samkomster, firmafester, fødselsdagsfester
- Billeder af lokalet opsat til selskaber
- Kontaktformular eller direkte link til forespørgsel
- Guldfarven `--c-accent` (#C9A96E) bruges som accentfarve her — separatorlinjer, ikoner, dekorative elementer

**Placering på forsiden:** Senest som anden eller tredje sektion. Kan introduceres med en bred hero-sektion med mørk baggrund og guldaccenter for at markere skiftet visuelt.

**À la carte-menuen** er det andet fokuspunkt — vises som PDF-link. Menukortet (PDF) tilføjes i projektet, når det er klar.

---

## JavaScript-skelet

### Scroll-reveal (IntersectionObserver)

```javascript
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('is-in');
      io.unobserve(e.target);
    }
  });
}, { threshold: 0.12, rootMargin: '0px 0px -80px 0px' });

document.querySelectorAll('.reveal').forEach(el => io.observe(el));
```

### Nav-indlæsningsanimation

```javascript
setTimeout(() => {
  document.querySelector('.nav').classList.add('is-loaded');
}, 150);
```

### Mørk nav (tilpasser sig sektion-baggrund)

```javascript
const nav = document.querySelector('.nav');
const sections = document.querySelectorAll('[data-tone]');

function updateNav() {
  const navBottom = nav.getBoundingClientRect().bottom;
  let isDark = false;
  sections.forEach(s => {
    const r = s.getBoundingClientRect();
    if (r.top <= navBottom && r.bottom >= navBottom) {
      if (s.dataset.tone === 'dark') isDark = true;
    }
  });
  nav.classList.toggle('is-dark', isDark);
}

window.addEventListener('scroll', updateNav, { passive: true });
window.addEventListener('resize', updateNav, { passive: true });
updateNav();
```

**Brug `data-tone="dark"` på mørke sektioner (fx footer, hero-video-side).**

### Parallax (til stillbilleder — ikke video)

```javascript
const parallaxEls = document.querySelectorAll('[data-parallax]');
let ticking = false;

function doParallax() {
  parallaxEls.forEach(el => {
    const speed = parseFloat(el.dataset.parallax);
    const r = el.getBoundingClientRect();
    const offset = -r.top * speed;
    el.style.transform = `translate3d(0, ${offset}px, 0)`;
  });
  ticking = false;
}

window.addEventListener('scroll', () => {
  if (!ticking) {
    requestAnimationFrame(doParallax);
    ticking = true;
  }
}, { passive: true });
```

**Brug `data-parallax="0.18"` på billeder med parallax-effekt.**

### Mobil-drawer

```javascript
document.querySelector('.burger').addEventListener('click', () => {
  const drawer = document.createElement('div');
  drawer.className = 'nav-drawer';
  drawer.innerHTML = `
    <button class="drawer-close" aria-label="Luk">×</button>
    <nav>
      <a href="/">Forside</a>
      <a href="/menu">À la carte</a>
      <a href="/selskaber">Selskaber & Events</a>
      <a href="/om-os">Om os</a>
      <a href="/kontakt">Kontakt</a>
      <a href="/book" class="btn-solid">Book bord</a>
    </nav>
  `;
  document.body.appendChild(drawer);
  requestAnimationFrame(() => drawer.classList.add('is-open'));

  drawer.querySelector('.drawer-close').addEventListener('click', () => {
    drawer.classList.remove('is-open');
    setTimeout(() => drawer.remove(), 400);
  });
});
```

```css
.nav-drawer {
  position: fixed;
  inset: 0;
  z-index: 200;
  background: var(--c-dark);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 32px;
  opacity: 0;
  transition: opacity 0.4s var(--ease);
}
.nav-drawer.is-open { opacity: 1; }
.drawer-close {
  position: absolute;
  top: 24px; right: 24px;
  width: 44px; height: 44px;
  font-size: 28px;
  color: var(--c-light-text);
  background: none;
  border: none;
  cursor: pointer;
}
.nav-drawer a {
  font-size: 22px;
  font-family: var(--f-display);
  color: var(--c-light-text);
  font-weight: 300;
}
```

---

## Komponentliste

| Komponent | Beskrivelse |
|---|---|
| `nav` | Fast navigation, glaseffekt, mørk variant |
| `hero` | Video venstre, logo/tekst højre, 60/40 split |
| `info-strip` | 3 kolonner med borders, nøglefakta |
| `pair` | 2 billeder side om side med offset |
| `quote-block` | Centreret citat, display-font, kursiv |
| `events-grid` | 3 kolonner, dato i guld, hover-baggrund |
| `set-menus` | 2 menukort side om side med borders |
| `wide-photo` | Fuld-bredde billede med overlay og billedtekst |
| `selskaber-sektion` | Fremhævet sektion med guldaccenter, kapacitet USP |
| `footer` | Mørk baggrund, 4-kolonne grid |
| `mobil-drawer` | Fullscreen overlay, opacity-animation |
| `btn-solid` | Brun CTA-knap |
| `btn-outline` | Outline-knap, inverteret ved hover |
| `btn-ghost` | Tekstknap med animeret pil |

---

## Billedmønstre

```css
img {
  display: block;
  max-width: 100%;
  object-fit: cover;
}
```

**Standardformater:**
- Herovideoformat: 16/9 (desktop), 4/3 (mobil)
- Billedpar: 4/5
- Kvadratisk sektion: 1/1
- Bredt foto: 21/9

**Overlay-gradient (mørke billeder):**
```css
.img-overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(43, 26, 10, 0.18),
    transparent 30%,
    transparent 70%,
    rgba(43, 26, 10, 0.42)
  );
}
```

---

## Forsidestruktur (anbefalet rækkefølge)

1. **Hero** — video venstre, Mellow-logo højre
2. **Selskaber & Events** — fremhævet, bred sektion, guld-accenter, 300 gæsters kapacitet
3. **Info-strip** — 3 kernepunkter (fx: à la carte · selskaber · beliggenhed)
4. **À la carte-menuen** — teaser + PDF-link (menukortet tilføjes når klar)
5. **Billedsektion** — stemningsbilleder, billedpar med offset
6. **Citat eller fortælling** — om stedet og stemningen
7. **Events** — kommende arrangementer
8. **Footer** — mørk baggrund, kontakt, åbningstider, links
