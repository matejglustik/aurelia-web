# AURELIA – web s CMS cez GitHub

Statická stránka (bez buildu) + administrácia **Sveltia CMS**, ktorá ukladá zmeny priamo do tvojho GitHub repozitára.
Všetky texty, modely, ceny, blog, motta a sociálne siete sa upravujú v administrácii bez zásahu do kódu.

## Čo je v balíku
- `index.html` – celá stránka (3D hodinky, obchod, blog). Obsah číta z priečinka `content/`.
- `content/site.json` – hlavné texty, motta, výhody, päta, sociálne siete.
- `content/models.json` – modely (názov, popis, cena, súčiastky, blog, 3D vzhľad).
- `content/posts.json` – ďalšie články v blogu.
- `admin/index.html`, `admin/config.yml` – administrácia.
- `assets/uploads/` – sem sa ukladajú nahrané fotky.
- `.nojekyll` – aby GitHub Pages nič nepreskladával.

## Nasadenie (GitHub Pages)
1. Na GitHube vytvor repozitár (napr. `aurelia-hodinky`) a nahraj do neho **celý obsah** tohto priečinka (vrátane `.nojekyll`).
2. V repozitári: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)`**.
   Stránka bude na `https://TVOJE-MENO.github.io/aurelia-hodinky/`.
3. Otvor `admin/config.yml` a v riadku `repo:` zmeň `VASE-MENO/NAZOV-REPOZITARA` na tvoje, napr. `jan-novak/aurelia-hodinky`. Ulož (commit).
4. Otvor `https://TVOJE-MENO.github.io/aurelia-hodinky/admin/`.
5. Prihlás sa cez **Sign in with token**: na GitHube vytvor *fine-grained personal access token*
   (Repository access: iba tento repozitár; Permissions → **Contents: Read and write**) a vlož ho.

## Úpravy
- **Stránka**: motta (pri každom obnovení sa vyberie iné), texty obchodu, výhody, päta, **sociálne siete**.
- **Modely hodiniek**: názov, kategória, popis, zoznam súčiastok, cena, parametre, článok v blogu, popisky fotiek.
  - **Nový model**: pridaj položku a v časti *3D vzhľad hodiniek* vyber farby a vlastnosti (luneta, náramok, kov, ručičky…).
  - **Poradie**: ťahaním. Prvý model je hlavný v úvode.
  - **Fotky**: ak nahráš vlastné fotky, použijú sa. Ak nie, stránka ich sama vyrenderuje z 3D modelu.
- **Blog – ďalšie články**: samostatné články s fotkou a textom.
- Po kliknutí na *Publish* sa vytvorí commit a stránka sa obnoví do pár minút.

## Lokálny náhľad
V priečinku spusti `python3 -m http.server 8000` a otvor `http://localhost:8000`.
Keď otvoríš `index.html` priamo zo súboru, použije sa vstavaná záloha obsahu (`<script id="fb">`) a zmeny z CMS sa neprejavia.
Na lokálne testovanie CMS (`local_backend: true`) použi `npx @sveltia/cms-proxy-server` (alebo Decap proxy) a otvor `/admin/`.

## Dôležité
- **Košík je ukážkový.** Platba, sklad ani objednávky nie sú pripojené; potrebuješ napr. Stripe/Shopify.
- Ceny, záruka, doprava, texty a články sú ukážkové – prepíš ich vlastnými.
- Nové *tvary* hodiniek (iný typ lunety, iný náramok) vyžadujú zásah do kódu. Farby a kombinácie existujúcich typov sa dajú meniť v CMS.
- Administrácia sa načítava zo služby unpkg. Po prvom spustení odporúčame v `admin/index.html` pripnúť konkrétnu verziu (`@sveltia/cms@X.Y.Z`).
- Alternatíva: rovnaký `config.yml` funguje aj s Decap CMS (vyžaduje OAuth server pre GitHub).
