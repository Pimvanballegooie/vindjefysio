# VindJeFysio Netwerk — vindjefysio.net (de hub)

Dit is de **hub** van het VindJeFysio-netwerk, geen spoke. vindjefysio.net is het centrale zoekportaal waar patiënten via alle 9 hoofdcategorieën en subcategorieën een gespecialiseerde therapeut of praktijk vinden, en van waaruit centraal wordt doorverwezen naar (en aangemeld bij) de gespecialiseerde spoke-subsites: rugnek, enkelvoet, beenklachten, kansrijkopgroeien, mentaalgezond, chronischezorg, armklachten, en (nog in aanbouw) gezond-oud-worden en neurologie.

## Architectuur
- Statische HTML/CSS/vanilla JS op GitHub Pages, custom domein via CNAME.
- Gedeelde Supabase-backend, project islujznszevdynguhjdc, met anon key in de frontend — dezelfde backend als alle spokes.
- Gedeelde tabellen: therapeuten, praktijken, therapeut_subcategorieen, therapeut_praktijken, subcategorieen, categorieen.
- In tegenstelling tot de spokes heeft deze repo geen eigen protocollen-pipeline (geen sync_protocollen.py, geen protocollen.html) — protocollen leven op de spoke-subsites zelf. Bestanden hier: index.html (zoekportaal), aanmelden.html (centrale praktijk/locatie-aanmelding), therapeut-aanmelden.html.
- index.html doorzoekt live via Supabase over alle 9 hoofdcategorieën heen en toont, waar relevant, een link naar de bijbehorende spoke-subsite (`cat-subsite-link` / `subsite-kaart`).

## Belangrijke conventies
- Praktijk/locatie-aanmelden loopt centraal via vindjefysio.net/aanmelden.html?via=<domein> — dit is de enige plek waar praktijken zich aanmelden, spokes linken hiernaartoe.
- Therapeut-aanmelden gebeurt juist NIET hier maar lokaal op elke spoke-subsite (therapeut-aanmelden.html linkt daar altijd relatief/lokaal, nooit naar vindjefysio.net).
- Mails lopen via info@vindjefysio.net.
- Therapeut-registratie (op de spokes) zet aangemeld_via op het eigen subsite-domein en actief=false (wacht op goedkeuring).
- Palet: navy #1B3A5C, teal #2A9D8F (het "neutrale" basispalet dat meerdere spokes ook als basis gebruiken, hier zonder domein-specifieke accentkleur omdat de hub alle categorieën gelijkwaardig toont).
- Structuur = de volledige, gedeelde `categorieen`-tabel met 9 hoofdcategorieën (elk met eigen icoon, zie `CAT_ICONS` in index.html):
  1. 👶 Kansrijk opgroeien — kinderfysiotherapie (spoke: kansrijkopgroeien.net)
  2. 🧓 Gezond oud worden — ouderenzorg, valpreventie (nog geen actieve spoke)
  3. 🧠 Neurologie — CVA, Parkinson, MS, duizeligheid (nog geen actieve spoke)
  4. 💭 Mentale gezondheid — psychosomatiek, burn-out, hyperventilatie (spoke: mentaalgezond.net)
  5. ❤️ Chronische zorg — COPD, hartrevalidatie, oncologie, chronische pijn (spoke: chronischezorg.net)
  6. 🦴 Rug, nek en bekken — lage rug, nek, bekken, scoliose (spoke: rugnek.net)
  7. 🦵 Benen — heup, knie, enkel en voet (spokes: beenklachten.net, enkelvoet.net)
  8. 💪 Armen — schouder, elleboog, pols en hand (spoke: armklachten.net)
  9. ⚕️ Behandelvormen — manuele therapie, dry needling, shockwave, echografie, bekken-/kaakfysiotherapie e.d. (netwerkbreed, geen eigen spoke)
- De subsites-sectie op de homepage toont de status van elke spoke expliciet (✓ Actief vs. Binnenkort); houd dit in sync met welke domeinen daadwerkelijk live zijn.

## Wat hier NIET hoort
- Geen sync-pipeline voor protocollen (die logica leeft per spoke, niet hier).
- Geen domein-specifieke subcategorie-secties zoals bij de spokes (`DOMEINEN`/`CATEGORIEEN`-objecten) — de hub toont juist de volledige breedte via de gedeelde categorieen/subcategorieen-tabellen, live opgehaald.
