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
- **Build your own box**: Im Packaging-Regal rechts Boxgrösse wählen (XXS=1, XS=2, S=4, M=6, L=9, XL=12; ab 13 = "Sonderbstellig" mit Zahlenfeld 13–30), dann Cookies aus der Vitrine in die Box packen (Box füllt sich sichtbar auf dem Tisch; Cookie in der Box antippen = wieder entfernen).
- **Jede Sorte in 2 Varianten**: "eifach so" oder "mit Soft Melt Chärn" (flüssiger Kern, im Bild als oranger Punkt). Umschalter-Chips über der Szene bestimmen, welche Variante beim Antippen in der Vitrine gilt; in der Liste hat jede Sorte zwei Zähler.
- **Cookie Mood**: Need comfort / Celebrating / Hangry / Study session / Date night → hebt passende Cookies hervor.
- **Kaffee nur an Abhol-Tagen**: Kaffeemaschine + COFFEEMENU (Americano, Cappuccino, Schale, Espresso, Kaffee Crème) erscheinen nur an konfigurierten Tagen (`CONFIG.coffeeDays` in index.html, 0=So…6=Sa; aktuell Fr+Sa als Platzhalter). Es gibt einen "Kafi-Tag simulieren"-Vorschau-Button.
- **Becher-Wahl bei Kaffee**: Wenn Kaffee im Warenkorb ist, muss gewählt werden: eigener Becher mitbringen ♻️ oder Einweg. Ohne Wahl bleibt der Bestell-Knopf gesperrt.
- Bestellung = mailto-Link mit fertig ausgefüllter Bestellübersicht (kein Backend!).

## Branding
- Logo: **Biene im Geisterkostüm** (Buhu = Geist) mit Kochmütze und Honiglöffel. Der User hat ein
  fertiges Logo-Bild (kam nur inline im Chat, nicht als Datei) → im HTML als SVG nachgezeichnet
  (`#buhu-bee`). **TODO: Original-Logodatei vom User einholen und einbauen.**
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
- Szene ist SVG mit klickbaren Elementen; **alle Funktionen gehen zusätzlich über die HTML-Liste darunter** (Barrierefreiheit + kleine Bildschirme). Szene scrollt horizontal (min-width 800px).
- **Hosting: GitHub Pages** via Workflow `.github/workflows/deploy.yml` (deployt bei Push auf `main`).
  Vorschau während der Arbeit: Claude-Artifact.
- Branch-Konvention: Feature-Branches `claude/...`, Merge nach `main` deployt.

## Sortiment & Preise
- **Echte Sorten (vom User)**: Oreo, Lotus (Biscoff), Ovomaltine Classic, Ovomaltine Noir – je "eifach so" oder "Soft Melt Chärn". Mood-Zuordnung in `COOKIES` in index.html ist von Claude geraten → bei Gelegenheit bestätigen lassen.
- **Preise noch Platzhalter**: XXS 4 / XS 7.50 / S 14 / M 20 / L 28 / XL 36 CHF; Sonderbstellig 3 CHF/Cookie; Kaffee 3.50–4.80 CHF. Soft Melt kostet aktuell gleich viel wie normal → fragen, ob Aufpreis.

## Offene Punkte (beim User nachfragen, wenn passend)
1. **Logo**: User hat es selbst gezeichnet, besitzt KEINE Vektordatei; das Bild kam bisher nur inline im Chat an (nicht speicherbar). User wurde gebeten, die Bilddatei als Anhang hochzuladen → dann als `assets/logo.png` einbauen und den nachgezeichneten SVG-Platzhalter `#buhu-bee` ersetzen/ergänzen.
2. Echte Preise (Boxen, Sonderbstellig, Kaffee, evtl. Soft-Melt-Aufpreis); Mood-Zuordnung der Sorten bestätigen.
3. Echte Abhol-Tage/-Ort + Kaffeetage konfigurieren.
4. Kontaktkanal: aktuell mailto an ai@honegger.dev – WhatsApp/Instagram gewünscht?
5. Über-mich-Text + Fotos.
6. Impressum & Datenschutz vor echtem Launch (in der Schweiz: zumindest Kontaktangaben empfohlen).
7. Eigene Domain? (GitHub Pages kann Custom Domains.)
8. GitHub Pages muss ggf. einmalig in den Repo-Settings aktiviert werden (Source: GitHub Actions) – der Workflow versucht es automatisch (`enablement: true`).
