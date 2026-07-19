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
- **Build your own box**: Im Packaging-Regal rechts Boxgrösse wählen (S=4, M=6, L=9, XL=12 Cookies), dann Cookies aus der Vitrine in die Box packen (Box füllt sich sichtbar auf dem Tisch).
- **Cookie Mood**: Need comfort / Celebrating / Hangry / Study session / Date night → hebt passende Cookies hervor.
- **Kaffee nur an Abhol-Tagen**: Kaffeemaschine + COFFEEMENU (Americano, Cappuccino, Schale, Espresso, Kaffee Crème) erscheinen nur an konfigurierten Tagen (`CONFIG.coffeeDays` in index.html, 0=So…6=Sa; aktuell Fr+Sa als Platzhalter). Es gibt einen "Kafi-Tag simulieren"-Vorschau-Button.
- Bestellung = mailto-Link mit fertig ausgefüllter Bestellübersicht (kein Backend!).

## Branding
- Logo: **Biene im Geisterkostüm** (Buhu = Geist) mit Kochmütze und Honiglöffel. Der User hat ein
  fertiges Logo-Bild (kam nur inline im Chat, nicht als Datei) → im HTML als SVG nachgezeichnet
  (`#buhu-bee`). **TODO: Original-Logodatei vom User einholen und einbauen.**
- Slogan (Visitenkarte, Schweizerdeutsch, wörtlich übernehmen):
  «De Schreck isch nur wenns kei meh het, drum bstell en jetzt bevor de Kolleg de letscht wett»
- Farbwelt aus dem Logo: Creme #FBF3E4, Greige #CDC1AC, Honig-Orange #F5A11C, Dunkelbraun #2E2015.
- Sprache: Deutsch mit Schweizer Schreibweise (**kein ß**), UI-Texte teils Schweizerdeutsch, Moods auf Englisch (so in der Skizze).
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

## Beispieldaten (alle noch Platzhalter!)
- Boxpreise: S 14 / M 20 / L 28 / XL 36 CHF. Cookiesorten: Choco Chip, Double Choc, Red Velvet, Peanut Butter, Espresso, Birthday Confetti (mit Mood-Zuordnung in `COOKIES` in index.html).
- Kaffeepreise: 3.50–4.80 CHF.

## Offene Punkte (beim User nachfragen, wenn passend)
1. Original-Logodatei (PNG/SVG) einbauen.
2. Echte Cookiesorten, Preise, Boxgrössen/-preise.
3. Echte Abhol-Tage/-Ort + Kaffeetage konfigurieren.
4. Kontaktkanal: aktuell mailto an ai@honegger.dev – WhatsApp/Instagram gewünscht?
5. Über-mich-Text + Fotos.
6. Impressum & Datenschutz vor echtem Launch (in der Schweiz: zumindest Kontaktangaben empfohlen).
7. Eigene Domain? (GitHub Pages kann Custom Domains.)
8. GitHub Pages muss ggf. einmalig in den Repo-Settings aktiviert werden (Source: GitHub Actions) – der Workflow versucht es automatisch (`enablement: true`).
