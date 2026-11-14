# AURELIA – web s CMS cez GitHub (Netlify Drop alebo GitHub Pages)

Statická stránka bez buildu. Texty, modely, ceny, blog, motta a sociálne siete sa upravujú v administrácii (`/admin/`).

## A) Rýchlo na Netlify: drag & drop
1. Rozbaľ `hodinky-cms.zip`.
2. Otvor https://app.netlify.com/drop a **pretiahni celý rozbalený priečinok** (index.html musí byť priamo v ňom).
3. Netlify ti hneď dá adresu a stránka **funguje celá** (3D hodinky, obchod, blog).
   Názov a vlastnú doménu zmeníš v *Site configuration → Domain management*.

### Aby fungovalo CMS (jednorazovo)
CMS ukladá zmeny do GitHub repozitára, takže potrebuje repozitár:
1. Na GitHube vytvor repozitár a nahraj do neho obsah tohto priečinka.
2. V súbore `admin/config.yml` zmeň `repo:` na `tvoje-meno/nazov-repozitara`.
3. **Prepoj Netlify s týmto repozitárom** (*Site configuration → Build & deploy → Continuous deployment → Link repository*; ak možnosť nevidíš, vytvor nový Netlify site cez *Add new site → Import an existing project*, publish directory nechaj prázdny alebo `.`). Potom sa každá zmena z CMS sama nasadí za ~1 minútu.
4. Otvor `https://tvoja-adresa.netlify.app/admin/` a prihlás sa cez **Sign in with token**
   (GitHub → Settings → Developer settings → Fine-grained token → len tento repozitár, **Contents: Read and write**).

Bez kroku 3 sa zmeny z CMS uložia na GitHub, ale web na Netlify sa nezmení, kým ho znova nedropneš.
Úplne bez GitHubu: uprav JSON súbory v `content/` ručne a priečinok znova dropni.

## B) GitHub Pages
Repozitár → *Settings → Pages → Deploy from a branch → `main` / `(root)`*. Admin je na `/admin/` rovnako.

## Obsah balíka
- `index.html` – stránka; číta `content/*.json` (vstavaná záloha obsahu je v `<script id="fb">`).
- `content/site.json` – texty, motta, výhody, päta, sociálne siete.
- `content/models.json` – modely (popis, cena, súčiastky, blog, 3D vzhľad: farby, luneta, náramok, kov…).
- `content/posts.json` – ďalšie články v blogu.
- `admin/` – Sveltia CMS (`index.html`, `config.yml`).
- `_headers`, `netlify.toml` – nastavenia pre Netlify. `.nojekyll` – pre GitHub Pages.

## Čo upravovať v CMS
- **Stránka**: motta (pri každom obnovení iné), texty, výhody, odkazy na Instagram, Facebook, TikTok, YouTube…
- **Modely hodiniek**: pridávanie, poradie (ťahaním), ceny, popisy, vlastné fotky (ak ich nenahráš, stránka ich vyrenderuje z 3D).
- **Blog – ďalšie články**: samostatné články s fotkou.

## Dôležité
- Košík je ukážkový: platba ani objednávky nie sú pripojené (treba napr. Stripe alebo Shopify).
- Ceny, záruka, doprava, texty a články sú ukážkové.
- Nový *tvar* hodiniek (iný typ lunety/náramku) vyžaduje zásah do kódu; kombinácie existujúcich typov a farby sa menia v CMS.
- Admin sa načítava z unpkg; po prvom spustení pripni verziu v `admin/index.html` (`@sveltia/cms@X.Y.Z`).
- Lokálny náhľad: `python3 -m http.server 8000` v priečinku. Otvorenie `index.html` priamo zo súboru použije vstavanú zálohu obsahu.
