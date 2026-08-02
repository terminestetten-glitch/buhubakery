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
- **NOCH NICHT GEBAUT – Verpackungswahl** (User, 02.08.2026): So läuft's real ab:
  - **Jeder Cookie einzeln verpackt** (kleines Tütchen) – das ist immer so, keine Wahl.
  - **Die ganze Bestellung** kommt dann in **eine** Aussenverpackung: entweder eine **grosse Box** (fancy, teurer)
    oder eine **weisse Papiertüte** (einfacher, günstiger).
  - Die Wahl gilt also **pro Bestellung**, nicht pro Cookie und nicht pro Grösse – die Boxgrösse bestimmt weiterhin
    nur, wie viele Cookies reinpassen.
  - **Offen**: wie gross der Preisunterschied zwischen Tüte und Box ist. Ohne diese Zahl nicht bauen.

## Abholung (vom User, 02.08.2026)
- **Ort**: Dübendorf. Genaue Adresse gibt's erst nach der Bestellung (bewusst so).
- **Vorlaufzeit**: mindestens 2 Tage.
- **Kaffee-Tage**: Sonntag ist fix (`CONFIG.coffeeDays: [0]`). Weitere Tage hängen vom Job des Users ab
  und werden bei Bedarf pro Datum im Admin-Panel gesetzt.
- **Offen**: an welchen Tagen kann man *ohne* Kaffee abholen?

## Offene Punkte (beim User nachfragen, wenn passend)
1. Mood-Zuordnung der Sorten bestätigen (in `COOKIES` von Claude geraten).
2. Kontakt: Bestell-Mail ist bestellung@buhubakery.ch (prüfen, ob Postfach existiert!).
   **Kein Instagram** (User hat keins, Stand 02.08.2026) → im Footer/Design nicht anbieten. WhatsApp noch offen.
   **Impressum (vom User, 02.08.2026)**: Laura Blessing, Dübendorf, bestellung@buhubakery.ch.
   Anmerkung: Der User will die genaue Adresse bewusst nicht öffentlich zeigen. Für den Schweizer Online-Handel
   verlangt UWG Art. 3 Abs. 1 lit. s aber Name **und** vollständige Adresse inkl. Strasse. Einmal darauf hingewiesen –
   Entscheid liegt beim User; nicht bei jeder Gelegenheit erneut aufbringen.
   **Domain**: User hat eine Domain bei **GoDaddy** gekauft (vermutlich buhubakery.ch). Plan: GitHub Pages + Custom Domain.
   Nötige Schritte: (a) Branch nach main mergen → Workflow deployt; (b) Repo-Settings → Pages → Custom Domain eintragen + "Enforce HTTPS";
   (c) Bei GoDaddy DNS: A-Records für @ auf 185.199.108.153 / 185.199.109.153 / 185.199.110.153 / 185.199.111.153, CNAME für www auf terminestetten-glitch.github.io.
   Achtung: Bei Workflow-Deploys zählt NUR die Pages-Einstellung, eine CNAME-Datei im Repo reicht nicht.
4. Fotos für Über-mich (Text ist schon drin, wörtlich vom User).
5. Impressum & Datenschutz vor echtem Launch (in der Schweiz: zumindest Kontaktangaben empfohlen).
6. **Go-Live-Status (19.07.2026)**: `main` ist gepusht, Deploy-Workflow lief an, aber `configure-pages` scheiterte
   ("Resource not accessible by integration") → Pages kann nicht per Workflow-Token aktiviert werden. Zusätzlich ist das
   Repo **privat** (Pages auf privaten Repos = nur mit bezahltem Plan). User muss einmalig selbst klicken:
   (a) Repo öffentlich machen (Settings → General → Danger Zone → Change visibility),
   (b) Settings → Pages → Source: "GitHub Actions", Custom Domain buhubakery.ch eintragen + Enforce HTTPS.
   Danach Workflow neu starten (workflow_dispatch via `actions_run_trigger` oder neuer Push). DNS-Schritte bei GoDaddy siehe Punkt 3.
