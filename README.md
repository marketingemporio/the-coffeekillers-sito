# The Coffeekillers — sito

Sito vetrina della band **Hot Joe & The Coffeekillers** (country live, Brescia).
Online su **https://thecoffeekillers.com**.

> 📖 **Prima di lavorarci, apri [`_STATO.md`](_STATO.md)**: è la fonte di verità
> unica su a che punto siamo, cosa manca e come riprendere. Le regole per chi ci
> lavora (anche Claude) stanno in [`CLAUDE.md`](CLAUDE.md).

## Come è fatto

**HTML statico scritto a mano. Nessuna build, nessun framework, nessun `npm install`.**
Si apre un file, si modifica, si salva.

| File | Cos'è |
|---|---|
| `hjck.css` | **il foglio di linguaggio di tutto il sito** (dal 18/10/2026): colori, caratteri, bottoni, card, testata, piede |
| `index.html` | home |
| `chi-siamo.html` · `country.html` · `date.html` · `gallery.html` · `faq.html` | pagine interne |
| `preventivo.html` | il modulo di richiesta preventivo (due passi) |
| `privacy.html` | informativa privacy |
| `musica-country-dal-vivo.html` | **landing delle inserzioni** — `noindex`, ci si arriva solo dagli annunci; ha tutto lo stile inline ed è il riferimento da cui `hjck.css` è stato ricavato |
| `en/` | **il sito in inglese**: le stesse 8 pagine tradotte a mano |
| `consenso.js` | il riquadro dei cookie (va **prima** di Tag Manager, senza `defer`) |
| `traccia-modulo.js` + `netlify/functions/` | l'imbuto anonimo del modulo di preventivo |
| `fonts/` · `images/` | caratteri (tutti auto-ospitati) e fotografie (copie web; `images/gal/` le miniature della gallery) |

Ogni pagina linka `hjck.css` **prima** del proprio `<style>`, che contiene solo
l'impaginazione di quella pagina. Gli strumenti di verifica e i «corpi» da cui le pagine
sono rigenerate stanno in `_strumenti/`, che è fuori da git (solo sul Mac di Michele).

### I caratteri
**Bonzana** (titoli, licenza Webfont comprata il 02/09/2026), **LT Cushion** (bottoni ed
etichette) e **Manrope** (testi) stanno in `fonts/`, in woff2. **Nessun carattere arriva da
Google**: è una scelta di privacy e non si torna indietro.

## Le due lingue (dal 03/09/2026)

Il sito esiste in **italiano** (radice) e in **inglese** (cartella `en/`). Non c'è nessun
reindirizzamento automatico: **l'indirizzo resta lo stesso per tutti** e la lingua la sceglie
chi legge, col bottone **EN** / **IT** in testata (nel menu del telefono: *English* / *Italiano*)
o con la strisciolina che compare a chi ha il browser nell'altra lingua (si chiude e non
ricompare per la sessione: `sessionStorage`, non un cookie).

| Italiano | Inglese |
|---|---|
| `index.html` | `en/index.html` |
| `chi-siamo.html` | `en/about.html` |
| `country.html` | `en/country-music.html` |
| `date.html` | `en/dates.html` |
| `gallery.html` | `en/gallery.html` |
| `faq.html` | `en/faq.html` |
| `preventivo.html` | `en/quote.html` |
| `privacy.html` | `en/privacy.html` |

**Da sapere quando si lavora.** Le pagine inglesi sono **copie tradotte**, con lo stesso
scheletro di tag di quella italiana: se cambi un testo in italiano **va cambiato anche in `en/`**.
Le **date dei concerti** sono scritte a mano in quattro punti (`date.html`, `en/dates.html` e i
calendari in home di entrambe le lingue). I percorsi in `en/` salgono di un livello
(`../images/`, `../fonts/`, `../hjck.css`). I commenti nel codice restano in italiano.
La landing non è tradotta: gli annunci sono in italiano.

## I moduli
I tre moduli di preventivo (`preventivo.html`, `en/quote.html` e la landing) mandano a
**Netlify Forms** (dal 12/09/2026): form `preventivo-sito`, `preventivo-en`, `preventivo-landing`.
Nomi dei campi, due passi, vincolo servizio → budget e testi delle chip **non si toccano** senza
leggere `CLAUDE.md`. Solo la **newsletter** va ancora a Formspree, di proposito (il piano Netlify
gratuito dà 100 invii al mese e vanno tenuti per i preventivi).

## Hosting e pubblicazione
- **Netlify**, collegato al repo GitHub `marketingemporio/the-coffeekillers-sito`, branch `main`.
  Publish directory: `.` (la radice) · Build command: nessuno · **ogni `push` su `main` pubblica**.
- ⚠️ Netlify pubblica **la radice**: tutto quello che è tracciato da git finisce online.
  Per questo `_parcheggio/`, `_strumenti/`, `_font-prova/`, `_brand-def/`, `_bozzetti/`, i PDF del
  brand, le foto originali e i file `_prova-*.html` sono esclusi in `.gitignore`, e `_redirects`
  blocca `_STATO.md`, `README.md` e `CLAUDE.md`.

## Analytics e cookie
**Google Tag Manager** e **Google Analytics** dal 12/09/2026, **solo dopo il consenso** dato nel
riquadro (`consenso.js`, stato di partenza «negato»). In più **Cloudflare Web Analytics**, senza
cookie. L'informativa è in `privacy.html` ed `en/privacy.html`: si cambia sempre in due lingue.

## Cosa c'è in `_parcheggio/` (solo in locale, fuori dal repo)
Niente si cancella: quello che non serve più si sposta qui. Tra l'altro: il sito React che c'era
fino al 01/09/2026, le maquette scartate, il vecchio `stile-hjck.css` (fino al 18/10/2026), le
immagini non più usate e le versioni pesanti delle foto alleggerite il 18/10.
