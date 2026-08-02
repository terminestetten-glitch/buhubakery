# BuhuBakery – Projekt-Notizen für Claude

## Wichtig: Arbeitsweise mit dem User
- User hat **keine Programmierkenntnisse**, ist visuell orientiert, spricht Deutsch (Schweiz).
- **Token-sparsam arbeiten**: kurze Antworten, keine langen Erklärungen, wenige grosse Schritte statt vieler kleiner. Der User hat begrenztes Nutzungskontingent.
- Auf Deutsch antworten, einfach erklären, Fachbegriffe vermeiden oder kurz erklären.
- Entscheidungen selbst treffen, nur bei echten Weichenstellungen einfach formulierte Fragen stellen (AskUserQuestion).
- Immer schnell eine visuelle Vorschau bereitstellen (Artifact-Tool).
- **Diese Datei aktuell halten**, wenn sich Entscheidungen ändern.

## Was das Projekt ist
Website für das Cookie-Business "BuhuBakery" (Schweiz). Konzept laut Skizze des Users
(`docs/idee-skizze.pdf`): **Die Website ist ein illustriertes Café.**
- Theke mit Cookie-Vitrine, "Buhu Bakery"-Schild, Lampen, Bogenfenster, Tisch + Hocker, Herzballons.
- **Build your own box**: Im Packaging-Regal rechts Boxgrösse wählen (XXS=1, XS=2, S=4, M=6, L=9, XL=12; ab 13 = "Sonderbstellig" mit Zahlenfeld 13–30), dann Cookies aus der Vitrine in die Box packen (Box füllt sich sichtbar auf dem Tisch; Cookie in der Box antippen = wieder entfernen; bewusst KEINE Flug-Animation – User wollte das nicht).
- **Volli Box gaht zue**: sobald alli Plätz bsetzt sind, wird d'Box uf em Tisch zuegmacht (Deckel + Honig-Bändeli + "Voll! 🎉"). Atippe macht si wieder uf (`boxPeek` in index.html), s'letschte Cookie iiglegt macht si automatisch wieder zue.
- **Mehrere Boxen pro Bestellung**: Knopf "+ No e Box drzue" legt die aktuelle Box in die Bestellung (Stapel erscheint neben der offenen Box auf dem Tisch), ×-Knopf in der Zusammenfassung entfernt sie wieder.
- **Kaffee auch über die COFFEEMENU-Tafel in der Szene antippbar** (jede Zeile = 1× bestellen).
- **Handy geht jetzt au im Hochformat** (Wunsch hat sich geändert): kei Dreh-Overlay meh, d'Szene het kei `min-width` meh und skaliert uf jedi Breiti, ohni dass me was verschiebe muss.
- **Jede Sorte in 2 Varianten**: "eifach so" oder "mit Soft Melt Chärn" (flüssiger Kern, im Bild als oranger Punkt). Umschalter-Chips über der Szene bestimmen, welche Variante beim Antippen in der Vitrine gilt; in der Liste hat jede Sorte zwei Zähler.
- **Cookie Mood**: Need comfort / Celebrating / Hangry / Study session / Date night → hebt passende Cookies hervor.
- **Kaffee nur an Abhol-Tagen**: Kaffeemaschine + COFFEEMENU (Americano, Cappuccino, Schale, Espresso, Kaffee Crème) erscheinen nur an konfigurierten Tagen (`CONFIG.coffeeDays` in index.html, 0=So…6=Sa; aktuell Fr+Sa als Platzhalter). Es gibt einen "Kafi-Tag simulieren"-Vorschau-Button.
- **Becher-Wahl bei Kaffee**: Wenn Kaffee im Warenkorb ist, muss gewählt werden: eigener Becher mitbringen ♻️ oder Einweg. Ohne Wahl bleibt der Bestell-Knopf gesperrt.
- Bestellung = mailto-Link mit fertig ausgefüllter Bestellübersicht (kein Backend!).
- **Buhu (Café-Mitarbeiter) fliegt jetzt zwüsche de Schritt-Punkte** (Flügel flügle schneller während em Flug, Sprächblase blendet us), staht standardmässig im Gang hinter de Theke (zwüsche Theke-Deckfläche und Ablagefläche mit de Kaffimaschine – wie en Mitarbeiter hinter em Tresen).
- **Becher-Frag jetzt über Buhu**: sobald Kafi im Warenkorb isch und kei Becher gwählt, fragt Buhu direkt i de Sprächblase ("eigene Becher ♻️" oder "bruch eine") – nöd nur über d'Chips im Panel.
- **Schritt-Uflüchte**: s'passendi Bedienelement pulsiert sanft, je nach dem was Buhu grad vorschlaht (Regal → Vitrine → Kafi-Menü/Maschine → Kalender-Panel bi Schritt 4).
- **Ruum-Perspektive**: Rückwand goht bis y=300, dedrunter en tüüfe Bodä (300–660) mit Diele wo uf de Fluchtpunkt (620, 262) zuelaufed, plus Quer-Fuge wo nach hinde enger werded. Alles isch nach Tüefi gstaffelet: Ablagi hinde (Bodä y≈350) → Buhu im Gang → Theke vorne (Deckflächi y≈404) → Tisch/Höckerli. Fänschter und Regal ghöred a d'Rückwand und dörfed nöd under y=300 abeglange.
- **Boxe wieder bearbeite**: jedi zuegleiti Box i de Zämefassig het en ✏️-Knopf (`editSavedBox`) wo si zrugg uf de Tisch holt.
- **Variante-Wahl au i de Szene**: d'Chips "eifach so" / "mit Soft Melt Chärn" sind zuesätzlich direkt a de Vitrine (`#g-variant-scene`). Bi Sorte mit `plainOnly` (Cinnamon Dream) erschiint es "nur eifach"-Schildli, wenn Soft Melt gwählt isch.
- **Theke isch als echte 3D-Blockform gezeichnet**: sichtbari Deckfläche (Tischplatte-Trick, gliich wie bi de Box-Deckel) + Front mit iibauter Glasvitrine (Cookies liege dinne i re Reihe, nöd meh als separati Vitrine obe druf). D'Ablagefläche hinter de Theke het de gliiche Trick für iri Platte.

## Branding
- Logo: **Biene im Geisterkostüm** (Buhu = Geist) mit Kochmütze und Honiglöffel. **Original eingebaut**:
  `assets/logo.png` (720px, extrahiert aus dem Vektor-PDF des Users, Original liegt in `docs/logo.pdf` –
  bei Bedarf kann daraus jede Auflösung neu gerendert werden, PyMuPDF). Wird rund angezeigt (border-radius 50%).
- Slogan (Visitenkarte, Schweizerdeutsch, wörtlich übernehmen):
  «De Schreck isch nur wenns kei meh het, drum bstell en jetzt bevor de Kolleg de letscht wett»
- Farbwelt aus dem Logo: Creme #FBF3E4, Greige #CDC1AC, Honig-Orange #F5A11C, Dunkelbraun #2E2015.
- Sprache: **Züridütsch** für alle UI-Texte (Wunsch des Users), Moods auf Englisch (so in der Skizze). Kein ß.
- Über-mich-Text: vom User geliefert (Züridütsch, mit 🍪 und 🐝🤎), steht wörtlich in index.html – nicht umformulieren.
- Währung: **CHF**.

## Technik-Entscheidungen (mit Begründung)
- **Ein einziges statisches `index.html`** (CSS+JS eingebettet): kein Build, keine Abhängigkeiten,
  nichts kann kaputt-updaten, für Laien am wartbarsten. Erst aufteilen, wenn die Seite deutlich wächst.
- **Kein Backend/keine Datenbank**: Bestellung per mailto → keine Datenspeicherung, kein Datenschutz-Albtraum, nichts zu hacken. Security-Oberfläche minimal.
- **Tap statt Drag & Drop** zum Cookie-Hinzufügen: Drag & Drop ist auf Touchscreens unzuverlässig; Cookie "fliegt" stattdessen animiert in die Box (bei `prefers-reduced-motion` ohne Animation).
- **Mobile-first**, beide Farbmodi (hell/dunkel) über CSS-Tokens; die Café-Illustration hat bewusst fixe Farben.
- Szene ist SVG mit klickbaren Elementen; **alle Funktionen gehen zusätzlich über die HTML-Liste darunter** (Barrierefreiheit + kleine Bildschirme). Szene skaliert responsiv (kei horizontales Scrollen meh, kei min-width).
- **Hosting: GitHub Pages** via Workflow `.github/workflows/deploy.yml` (deployt bei Push auf `main`).
  Vorschau während der Arbeit: Claude-Artifact.
- Branch-Konvention: Feature-Branches `claude/...`, Merge nach `main` deployt.

## Sortiment & Preise
- **Echte Sorten (vom User)**: Oreo, Lotus (Biscoff), Ovomaltine Classic, Ovomaltine Noir – je "eifach so" oder "Soft Melt Chärn". Cinnamon Dream (Zimt-Cookie mit Pekannuss) isch **nume als "eifach so"** verfügbar, kei Soft-Melt-Variante (`plainOnly: true` in `COOKIES`). Mood-Zuordnung in `COOKIES` in index.html ist von Claude geraten → bei Gelegenheit bestätigen lassen.
- **Preise sind ECHT (vom User bestätigt, 02.08.2026)** – nicht mehr als Platzhalter behandeln:
  XXS 4.00 / XS 7.50 / S 15.50 / M 23.00 / L 35.50 / XL 44.00 CHF; Sonderbstellig 4.00 CHF/Cookie **minus 0.50 pauschal**
  (`boxPrice()` in index.html); Soft Melt **+0.50 CHF pro Cookie** (gilt für alle Boxgrössen);
  Kaffee: Espresso 3.50 / Kaffee Crème 4.00 / Americano 4.20 / Schale 4.50 / Cappuccino 4.80.
  Hinweis: `SONDER.meltSurcharge` ist definiert, wird aber nicht benutzt – `boxPrice()` hat 0.50 zweimal hardcodiert.
- **Pro Cookie (vom User, 02.08.2026)**: 4.00 CHF ohne Soft Melt, 4.50 CHF mit. Deckt sich mit dem +0.50-Aufpreis.
  Die Fixgrössen liegen leicht darunter (z.B. S = 4 Cookies für 15.50 statt 16.00) → enthält einen kleinen Mengenrabatt.
- **Verpackung (gebaut, Preise vom User bestätigt 02.08.2026)** – `PACKAGING` in index.html:
  - **Jeder Cookie einzeln verpackt** – immer, keine Wahl. In der Szene als durchsichtiges Säckli um jeden Cookie.
  - **Die ganze Bestellung** kommt in **eine** Aussenverpackung, Wahl gilt **pro Bestellung** (nicht pro Box):
    | Papiertüte | +0.00 | braunes Kraftpapier, schlicht |
    | Schöni Verpackig | **gestaffelt** | gleiche Tüte, mit Bändeli & Bienen-Sticker |
    | Gschänk-Box 🎁 | +2.50 | Box mit Deckel und Schleife |
  - **Staffelung der schönen Verpackung** (User, 02.08.2026): bis und mit L (≤9 Cookies) 0.50,
    darüber 1.00, ab 30 Cookies 2.50. Darum ist `surcharge` eine **Funktion** `(n) => …`, die die
    Gesamtzahl Cookies der Bestellung bekommt – nicht mehr eine Zahl. Wer hier etwas ändert, muss
    `packagingPrice()` benutzen, nie `p.surcharge` direkt.
  - Die Preise auf den Auswahl-Buttons aktualisieren sich in `render()` mit, weil sie von der
    Bestellgrösse abhängen.
  - Die Boxgrösse bestimmt weiterhin nur, wie viele Cookies reinpassen.
  - Achtung: die Tüten sind **braun** (Kraftpapier) **mit Tragriemli**, nicht weiss – vom User korrigiert.
  - **Erst ab 4 Cookies** gibt es überhaupt eine Aussenverpackung (`PACKAGING_MIN_COOKIES`). Bei XXS (1) und XS (2)
    bekommt man die einzeln verpackten Cookies einfach so – keine Wahl, kein Aufpreis, und in der Szene liegen
    sie ohne Tüte auf dem Tisch.

## Zahlung & Kontakt (vom User, 02.08.2026)
- **TWINT, vor der Abholung**. Die Handynummer für TWINT kommt in der Bestätigungsmail (nicht öffentlich auf der Site).
- Kein Bargeld erwähnt → nur TWINT anbieten.
- **WhatsApp braucht keinen eigenen Link**: Kundinnen haben die Nummer ohnehin aus der Bestätigungsmail (TWINT),
  können also direkt schreiben. Auf der Site nur die E-Mail zeigen.
- **`bestellung@buhubakery.ch` existiert** (vom User bestätigt) – Bestellungen kommen an.

## Sprache: Züridütsch (wichtig!)
Der User hat am 02.08.2026 reklamiert, die Texte seien "ein Mix von Schweizer Dialekten oder manchmal gar
kein Schweizerdeutsch". Alles ist auf **Züridütsch** vereinheitlicht. Beim Schreiben neuer Texte beachten:
- **nur** (nicht "nume" – das ist Bernisch) · **eme** (nicht "emne") · **usser** (nicht "ussert")
- **im Vorus** (nicht "Voruus") · **wiiter wäg als** (nicht "wiiter aus als" – "aus" ist Bernisch für "als")
- **si** statt "sie" · **mer/der** statt "mir/dir" im unbetonten Fall · **Chärn** nicht "Kern"
- **Wie vill** statt "Wieviel" · **bstätige/Bstätigung** statt "bestätigen/Bestätigung"
- **Cookie ist maskulin**: "de Cookie", "Dunkle Schoggi-Cookie", "Wettsch eine wieder use?"
- Der Über-mich-Text stammt wörtlich vom User und bleibt unverändert.

## Allergene (Stand 02.08.2026)
- **Alle Sorten**: Gluten, Eier, Milch (vom User bestätigt) → zentral in `ALLERGY_GENERAL`, nicht pro Sorte wiederholen.
- Privatküche, in der auch Nüsse verarbeitet werden → immer mit erwähnen.
- Pro Sorte zusätzlich (`allergens` in `COOKIES`):
  Neo Cookies = Soja · Lotus = Soja · Ovomaltine Classic/Noir = Haselnuss, Gerstemalz, Soja · Cinnamon Dream = Pekannuss.
- **`mayContain`** ist ein eigenes Feld für Spuren-Warnungen – bewusst getrennt von `allergens`, weil
  "cha enthalte" und "enthaltet" bei Allergien nicht dasselbe heissen. Wird kursiv dargestellt.
  Aktuell: **Lotus** enthält weisse Schokolade von Lidl, in der jegliche Nüsse sein können (vom User, 02.08.2026).
- **Haselnuss bei Ovomaltine** steckt in der Schokolade selbst (vom User gemeldet).
- ✅ **Vom User an den echten Verpackungen geprüft und bestätigt (02.08.2026)** – inkl. Soja und Gerstemalz.
  Nicht erneut in Frage stellen. Nur anfassen, wenn der User eine Rezeptur oder einen Lieferanten ändert.
- **Namensänderung**: Die "Oreo"-Sorte heisst neu **"Neo Cookies"** – es sind Neo-Guetzli von Lidl, nicht Oreo.
  Claude hatte zuerst den neutralen Namen "Cookies & Cream" vorgeschlagen (Markenbedenken); der User hat
  "Neo Cookies" ausdrücklich gewünscht. Das ist auch konsistent, da Lotus und Ovomaltine ebenfalls
  nach der Marke benannt sind. **Nicht erneut aufbringen.**
  Die interne `id` bleibt `"oreo"` (Zeichnung `garnish: "oreo"`, `WOB.oreo`, Gradient `dough-oreo`).

## Haltbarkeit (vom User, 02.08.2026)
- **Ca. 5–6 Tage.** Danach noch geniessbar, aber nicht mehr saftig, sondern eher krümelig.
  Diese ehrliche Formulierung übernehmen, nicht zu "5–6 Tage haltbar" verkürzen.
- **Im Kühlschrank halten sie am längsten und schmecken am besten** – immer mit erwähnen.

## Seitenaufbau (Stand 02.08.2026, gebaut)
Reihenfolge: Header → Hero (mit 3 Fakten + 2 CTAs) → Bald-neu-Band → **Sortiment** → Café →
Über mich → Abholig → **Hüfigi Fröge** → Footer.
- **Sortiment** (`#sortiment`): Karten werden aus `COOKIES` generiert und nutzen dieselbe `cookieSVG()`
  wie die Vitrine – eine Änderung an `COOKIES` schlägt automatisch überall durch.
- **Abholig** (`#bestellen`): vier Info-Karten (Wo / Vorlauf / Kafi-Täg / Zahle).
- **Fröge** (`#froege`): Haltbarkeit, Allergene, Verpackung, Grossbestellungen.
- Der Allergen-Text steht **einmal** in `ALLERGY_GENERAL` und wird an drei Stellen eingesetzt
  (Sortiment, Cookie-Liste, FAQ) – dort ändern, nicht im Markup.
- **Über mich**: Foto-Platzhalter zeigt aktuell das Logo. Zum Ersetzen das `<img>` in `.about-photo`
  auf ein echtes Bild zeigen lassen (Kommentar steht im Markup).
  **Erledigt (02.08.2026)**: Das Porträtfoto liegt als `assets/laura.jpg` (900×1200, ~190 KB) und ist eingebunden.
  Der User hatte es als `.heic` abgelegt – das können Browser nicht anzeigen, also mit
  `sips -s format jpeg -Z 1200 … --out laura.jpg` konvertiert. Bei künftigen Fotos gleich vorgehen.
- **Hero hat bewusst KEINE Buttons**: "Bau dir dini Box" / "Was gits?" wurden vom User entfernt, weil sie
  das Logo nach unten gedrückt haben. Das Logo ist der Blickfang. Nicht ungefragt wieder einbauen.

## Abholung (vom User, 02.08.2026)
- **Ort**: Dübendorf. Genaue Adresse gibt's erst nach der Bestellung (bewusst so).
- **Abhol-Tage**: grundsätzlich **jeden Tag** – der Kalender in Schritt 4 lässt bewusst jeden Tag zu.
- **Vorlaufzeit**: mindestens 2 Tage.
- **Kaffee-Tage**: Sonntag ist fix (`CONFIG.coffeeDays: [0]`). Weitere Tage hängen vom Job des Users ab
  und werden bei Bedarf pro Datum im Admin-Panel gesetzt.
- **Offen**: an welchen Tagen kann man *ohne* Kaffee abholen?

## Offene Punkte (beim User nachfragen, wenn passend)
1. Mood-Zuordnung der Sorten bestätigen (in `COOKIES` von Claude geraten).
2. Kontakt: Bestell-Mail ist bestellung@buhubakery.ch – **Postfach existiert** (vom User bestätigt).
   **Kein Instagram** (User hat keins, Stand 02.08.2026) → im Footer/Design nicht anbieten. WhatsApp noch offen.
   **Impressum (vom User, 02.08.2026)**: Laura Blessing, Dübendorf, bestellung@buhubakery.ch.
   Anmerkung: Der User will die genaue Adresse bewusst nicht öffentlich zeigen. Für den Schweizer Online-Handel
   verlangt UWG Art. 3 Abs. 1 lit. s aber Name **und** vollständige Adresse inkl. Strasse. Einmal darauf hingewiesen –
   Entscheid liegt beim User; nicht bei jeder Gelegenheit erneut aufbringen.
3. **Domain: erledigt.** buhubakery.ch läuft über GitHub Pages, DNS bei GoDaddy zeigt korrekt.
4. Fotos für Über-mich: **erledigt** – `assets/laura.jpg` ist eingebunden.
5. Datenschutz-Seite fehlt noch (Impressum steht im Footer). Bestellung läuft per mailto, es werden keine Daten gespeichert.
6. **Go-Live: ERLEDIGT (02.08.2026).** Die Site läuft live auf https://buhubakery.ch.
   Repo ist öffentlich, Pages-Source = "GitHub Actions", Custom Domain gesetzt,
   **Enforce HTTPS aktiv** (`https_enforced: true`, http → https 301). DNS bei GoDaddy zeigt korrekt.
   Deploy passiert automatisch bei jedem Push auf `main` – nichts mehr manuell nötig.
