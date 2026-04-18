# Claude README – bilingual-site

## What this site is
A trilingual (Hebrew, English, Polish) memorial website for the Jewish community of Różan, Poland. It honors **Shmuel Tzvi Braude** (1926–2025), a Holocaust survivor from Różan, and documents the reclamation of the Różan Jewish cemetery. Hosted on GitHub Pages at **https://idancoanthem.github.io/bilingual-site/**.

## Repository
- GitHub: https://github.com/Idancoanthem/bilingual-site
- Local clone: `/Users/Idan.Cohen/bilingual-site/`
- Single file site: everything is in `index.html`

## Tech stack
- Pure HTML/CSS/JS — no framework, no build process
- Hosted directly on GitHub Pages from `main` branch
- Google Fonts: "Assistant" (Hebrew-friendly)

## Page structure
All 9 "pages" live in one `index.html`, shown/hidden via JS. Each has an ID of the form `[lang]-[type]`:

| ID | Content |
|----|---------|
| `he-main` / `en-main` / `pl-main` | Landing/navigation page |
| `he-text1` / `en-text1` / `pl-text1` | Biography of Shmuel Tzvi Braude |
| `he-text2` / `en-text2` / `pl-text2` | Story of the Różan cemetery reclamation |
| `he-text3` / `en-text3` / `pl-text3` | Photos page (empty divs — gallery is an overlay) |

## Language switching
- Hebrew: RTL (`dir="rtl"` on `<html>`)
- English/Polish: LTR (`dir="ltr"` on inner divs)
- `switchLang(lang)` keeps you on the same page type when switching
- Language buttons: top-right of each page

## Photo gallery
- **8 photos** total: `1.jpeg` through `8.jpeg` in repo root
- Source of truth for images: `/Users/Idan.Cohen/Downloads/images/` (named 1–8)
- Gallery is a **fullscreen overlay** (`#gallery-overlay`) placed *outside* `.container` in the HTML — this is critical because `.container` has `backdrop-filter: blur()` which creates a stacking context that traps `position: fixed` children
- Navigation: scroll wheel or swipe up/down → fade transition between photos (0.6s)
- Only one photo visible at a time (opacity fade, not scroll-snap)
- Controls: back button (top-left), lang switchers (top-right), counter (bottom-center), bounce arrow ↓ (above counter, hidden on last photo)
- `switchGalleryLang()` switches language while preserving current photo index

### Photos array (in `index.html` JS)
```js
{ src: '1.jpeg', captions: { he: 'לאחר השואה', en: 'After the Holocaust', pl: 'Po Zagładzie' } }
{ src: '2.jpeg', captions: { he: 'מדריך אגודת ישראל במחנה יתומים', en: 'Agudat Yisrael counselor in an orphan camp', pl: 'Wychowawca Agudat Israel w obozie dla sierot' } }
{ src: '3.jpeg', captions: { he: 'עם אשתו בצעירותם', en: 'With his wife in their youth', pl: 'Z żoną w młodości' } }
{ src: '4.jpeg', captions: { he: 'וליד ביתם בישראל', en: 'And near their home in Israel', pl: 'I przy ich domu w Izraelu' } }
{ src: '5.jpeg', captions: { he: 'מכניס ספר תורה לכבוד משפחתו וכל ניצולי השואה', en: 'Dedicating a Torah scroll in honor of his family and all Holocaust survivors', pl: 'Wnoszący zwój Tory ku czci swojej rodziny i wszystkich ocalałych z Zagłady' } }
{ src: '6.jpeg', captions: { he: 'מדליק נרות לזכר ששת המליונים בטכס יום השואה 2022', en: 'Lighting candles in memory of the six million at a Holocaust Remembrance Day ceremony, 2022', pl: 'Zapalający znicze ku pamięci sześciu milionów podczas uroczystości Dnia Pamięci o Holokauście 2022' } }
{ src: '7.jpeg', captions: { he: 'סוכות האחרון בחייו 2025', en: 'The last Sukkot holiday of his life', pl: 'Ostatnie święto Sukkot w jego życiu' } }
{ src: '8.jpeg', captions: { he: 'השבט אותו הקים, צאצאיו, קרא להם "הניצחון שלי"', en: 'The tribe he established, his descendants – he called them "my victory"', pl: 'Ród, który stworzył, jego potomkowie – nazywał ich „moim zwycięstwem"' } }
```

## Background images
- `saba.jpg` — used on biography pages (text1)
- `rojan.jpg` — used on cemetery pages (text2), applied via `body.bg-rojan` class

## Key CSS notes
- `.container` has `backdrop-filter: blur(10px)` — this creates a stacking context, so any `position: fixed` elements inside it are clipped. The gallery overlay must remain outside `.container`.
- `.hidden { display: none }` — page visibility mechanism
- Gallery image max-height: `72vh` (leaves room for caption + arrow)
- Caption has `margin-bottom: 3.5rem` to clear the bounce arrow

## Workflow
- Edit `index.html` locally at `/Users/Idan.Cohen/bilingual-site/index.html`
- Add images to `/Users/Idan.Cohen/bilingual-site/`
- `git add`, `git commit`, `git push` — site updates automatically
- Browser cache can lag; use incognito or Cmd+Shift+R to verify changes
