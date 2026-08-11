# Projekt.md — Aktueller Stand der Projekte

> Diese Datei ergänzt `Dieter.md` (Spielregeln der Zusammenarbeit) und
> `info_1.md` (Volltexte für die Übersichtsseite). **Bei Bedarf werden beide
> herangezogen:** `Dieter.md` für *wie* gebaut wird, `info_1.md` für die
> ausführlichen Beschreibungstexte einzelner Tools, diese Datei für *was*
> aktuell läuft und *woran* gerade gearbeitet wird.
>
> Reihenfolge beim Einlesen zu Chat-Beginn: zuerst `Dieter.md`, dann
> `Projekt.md` (diese Datei), `info_1.md` nur bei Bedarf nachschlagen.

---

## 1. Projekt-Familien — Stand 11.08.2026

| Projekt | Version | Struktur | Link |
|---|---|---|---|
| Lotto 6aus49 — Analyse-Konsole | 2.1.0 | Einzeldatei | dietertepe.github.io/Lotto/Lotto_2-1-0.html |
| Lotto 6aus49 — Daten-Manager | 2.0.0 | Einzeldatei | dietertepe.github.io/Lotto/Lotto_Manager_Pro_2-0-0.html |
| EuroJackpot — Analyse-Konsole | 1.0.1 | Einzeldatei | dietertepe.github.io/Eurolotto/Eurolotto_1-0-1.html |
| EuroJackpot — Daten-Manager | 0.1.8 | Einzeldatei | dietertepe.github.io/Eurolotto/EuroJackpot_Manager_0-1-8.html |
| Skip-Bo — Basisversion | 6.6.0 | Einzeldatei | dietertepe.github.io/Ordner1/SkipBo_6_6_0.html |
| Skip-Bo — Klassisches Kartenspiel | 7.0.0 | Einzeldatei | dietertepe.github.io/Skipo/SkipBo_7_0_0.html |
| Skip-Bo — KI-Tuner | 2.7 (Turbo + 2.7b) | Einzeldatei | dietertepe.github.io/SkipBo_Tuner/SkipBo_Tuner_v2_7.html |
| DT-ProfiDreieck — Testversion | Test 1.1.0 (Engine 3.0.0) | Einzeldatei | dt-profidreieck.de |
| DT-ProfiDreieck — Pro-Version | Pro 1.1.0 (Engine 3.0.0) | Einzeldatei | dietertepe.github.io/Ordner1/DT-ProfiDreieck_Pro_1-1-0.html |
| DT-ProfiSchraube — Testversion | Test | Einzeldatei | dietertepe.github.io/dt-profischraube-web/DT-ProfiSchraube_Test.html |
| DT-ProfiSchraube — Vollversion | 4.9.5 | Einzeldatei | dietertepe.github.io/dt-profischraube-web/DT-ProfiSchraube-4-9-5.html |
| DT-ProfiSchweissnaht — Testversion | — | Einzeldatei | dietertepe.github.io/dt-profischweissnaht-web/DT-ProfiSchweissnaht_Testversion.html |
| DT-ProfiSchweissnaht — Vollversion | — | Einzeldatei | dietertepe.github.io/dt-profischweissnaht-web/DT-ProfiSchweissnaht_Vollversion.html |
| DT-ProfiPassung — Testversion | — | Einzeldatei | dietertepe.github.io/dt-profipassung-web/DT-ProfiPassung_Testversion.html |
| DT-ProfiPassung — Vollversion | — | Einzeldatei | dietertepe.github.io/dt-profipassung-web/DT-ProfiPassung_Vollversion.html |
| Wärmeverlust- & Gebäude-Analyse (Heizungs-Check) | 1.0 | Einzeldatei | dietertepe.github.io/Heizungsanlage/waermeverlust.html |
| Speicher-Studio (Browser-Speicher verwalten) | — | Einzeldatei | dietertepe.github.io/Ordner1/speicher-studio_aktuell.html |

Volltexte (Was es kann / Was es auszeichnet) zu jedem dieser Tools stehen in
`info_1.md` — dort bei Bedarf nachschlagen, nicht hier duplizieren.

**DT-ProfiDreieck** ist seit v1.8.0 der Übersichtsseite in zwei Kacheln geteilt
(Test kostenlos mit freiem Export; Pro schaltet Spezialfälle Umkreis/Inkreis/
Fläche/Höhen frei, mit Lizenz-Wasserzeichen, Vertrieb über Digistore24).
**DT-ProfiSchraube** ist eine eigene Familie (Test + Vollversion):
Schraubenauslegung nach VDI 2230 Blatt 1 mit fünf Nachweisen und Ampel-
Bewertung; die Testversion rechnet alles, kann aber nicht exportieren/laden/
speichern.

**Sonderfall Heizungs-Check:** Anders als die übrigen Tools ist dies kein
eigenständig veröffentlichtes Projekt, sondern für Dieters konkrete eigene
Heizungsanlage gebaut (mehrere Heizkreise, manuell bedienter Mischer). Läuft
trotzdem nach denselben Standards (Einzeldatei, responsiv, lokal gespeichert).

---

## 2. Aktives Projekt: Tool-Werkstatt — Start-/Übersichtsseite

Eine neue, übergeordnete Einzeldatei (`uebersicht.html`), die alle obigen
Tools als Kacheln zugänglich macht. Kein eigenständig veröffentlichtes
Lotto/Skip-Bo/Dreieck/Heizungs-Tool, sondern die zentrale Startseite für alle.

- **Datei:** `uebersicht.html` — eine selbst-enthaltene HTML (Grundregel 1:
  Einzeldatei, läuft auf Handy/Tablet/PC ohne Installation).
- **Design:** Dunkles Konsolen-/Schaltpult-Design. Neun Akzentfarben nach
  Projektfamilie (Lotto = Gold, EuroJackpot = Türkis, Skip-Bo = Karmesinrot,
  DT-ProfiDreieck = Stahlblau-Grau, DT-ProfiSchraube = Amethyst-Violett,
  DT-ProfiSchweissnaht = Kupfer/Bernstein, DT-ProfiPassung = Beere/Magenta,
  Wärmeverlust-Analyse = Ember-Orange,
  Speicher-Studio = Smaragdgrün).
- **Stand v1.11.0 (fertig):**
  - Alle 17 Tools als Kacheln in 9 Familien, gruppiert (inkl. Heizungs-Check).
    DT-ProfiDreieck als zwei Kacheln (Test + Pro); Familie DT-ProfiSchraube
    (Test + Vollversion, VDI 2230 Blatt 1); Familie DT-ProfiSchweissnaht
    (Test + Vollversion, EN 1993-1-8 u. a., direkt nach der Schraube);
    Familie DT-ProfiPassung (Test + Vollversion, ISO 286 / DIN 7190 /
    ISO 2768); Familie Speicher-Studio (Browser-Speicher, ans Ende gestellt).
  - **Versions-Chip optional (seit v1.9.0):** Tools ohne Versionsnummer (aktuell
    Speicher-Studio, DT-ProfiPassung und DT-ProfiSchweissnaht) zeigen weder auf der Kachel
    noch im Overlay einen Chip.
    Sobald eine echte Nummer vorliegt, einfach ins `version`-Feld eintragen.
  - Familien-Filter-Schalter oben (Kippschalter-Optik, LED-Puls)
  - Eigenes Icon pro Kachel (handgezeichnetes Inline-SVG)
  - Kachel-Klick → Overlay mit vollem Text + „Öffnen"-Link
  - Optionaler dritter Overlay-Abschnitt „So wird es genutzt" für Tools mit
    eigener Schritt-für-Schritt-Anleitung (bisher nur der Heizungs-Check)
  - Favoriten-Funktion: Stern pro Kachel markiert einen Favoriten (immer nur
    einer aktiv), erscheint oben im großen Favoriten-Display mit Start-Button
  - Direktstart pro Kachel: „Direkt starten"-Link, der das Tool sofort öffnet,
    ohne erst die Beschreibung lesen zu müssen
  - Favorit + Sprache + Familien-Filter werden lokal im Browser gespeichert
    (localStorage, kein Server, kein Tracking — wie die Theme-Speicherung bei
    Skip-Bo). Die ein-/ausgeblendeten Gruppen sind beim nächsten Start wieder
    genau wie beim Verlassen (gespeichert wird die Liste der ausgeblendeten
    Familien; Default = alle sichtbar).
  - Optik „echtes Schaltpult": Panel-Tiefe (Schraubenkopf-Punkte, Groove),
    Hover-Glow + nachzeichnende Icons, Boot-Animation beim Laden + dauerhaft
    pulsierende Status-LEDs, dezente Farbverläufe im Hintergrund
  - Handy: theme-color färbt die Statusleiste; Kacheln blenden am Handy
    zusätzlich sanft einzeln auf (reduced-motion abgesichert)
  - **Optik-Feinschliff (v1.8.0):** Kacheln heben sich beim Überfahren leicht
    an (Desktop-Hover, translateY); ein einmaliger Glanz-Streif läuft über das
    Favoriten-Display, sobald ein Favorit gesetzt wird. Beides
    reduced-motion-abgesichert.
  - **Mehrsprachigkeit (seit v1.6.0):** vier Sprach-Schalter oben rechts
    (DE/EN/PT/UA) im Kippschalter-Stil, je mit kleiner selbst gezeichneter
    SVG-Flagge (dezent; SVG statt Emoji, weil Flaggen-Emojis auf Windows nur
    als Buchstaben erscheinen). ALLE Texte übersetzt — Oberfläche UND die
    kompletten Tool-Beschreibungen. Sprache wird lokal gespeichert,
    <html lang> wird mitgesetzt, Datums-/Zeitformat folgt der Sprache.
  - **Bugfix v1.7.0 (Auto-Übersetzung):** Manche Browser übersetzten die Seite
    bei nicht-deutscher Sprache automatisch (z. B. „UK" → „Vereinigtes
    Königreich") und kollidierten mit der eigenen Umschaltung. Unterbunden über
    <html translate="no"> + Meta „notranslate". Das Ukrainisch-Kürzel zeigt
    jetzt „UA" statt „UK" (interner Sprachcode bleibt „uk").
- **Code-Stand (seit v1.4.0, erweitert in v1.6.0/v1.7.0):** Daten strikt von
  Logik getrennt; Kacheln werden EINMAL gebaut, Filter/Sprachwechsel
  aktualisieren nur Sichtbarkeit bzw. Texte (über gemerkte Referenzen, kein
  Neuaufbau); alle Inhalts-Texte über textContent, nur statische SVG-Icons und
  -Flaggen via innerHTML. Pro Tool ein i18n-Block {de,en,pt,uk};
  sprachunabhängige Felder (id, family, icon, version, link) bleiben außerhalb.
  Drei localStorage-Schlüssel: Sprache, Favorit, Filter (Liste ausgeblendeter
  Familien). Neue Sprache = Kürzel in LANGS + Eintrag in UI/LANG_ABBR/
  LANG_FLAGS/LOCALES, jeder FAMILIES-label und jedem TOOLS-i18n.
- **Geplant, noch offen (zu besprechen):**
  - Ukrainische Übersetzung bei Gelegenheit von einem Muttersprachler
    gegenlesen lassen (maschinell sorgfältig, aber nicht muttersprachlich
    geprüft). Weitere optische Verfeinerungen nach Bedarf.

---

## 3. Notizen / offene Fragen

### Namensschema lokal ↔ GitHub (feste Regel)

Zwei Namen für dieselbe Datei, bewusst getrennt:

| | Name | Zweck |
|---|---|---|
| **Lokal / Auslieferung** | versioniert, z. B. `uebersicht_1-11-0.html` | Verwaltung und Sicherung; die Versionsnummer ist am Dateinamen ablesbar |
| **Auf GitHub** | stabil, z. B. `uebersicht.html`, `speicher-studio_aktuell.html` | Der Link bleibt konstant, damit bestehende Verknüpfungen nicht brechen |

- Das **Umbenennen macht Dieter selbst** beim Hochladen — Claude liefert immer
  unter dem versionierten Namen aus und benennt nichts um.
- Aktuell gilt: ausgeliefertes `uebersicht_1-11-0.html` = `uebersicht.html`
  auf GitHub; die jeweils neueste Speicher-Studio-Datei liegt dort als
  `speicher-studio_aktuell.html`.
- In `info_1.md` und in der Übersichtsseite stehen daher immer die **stabilen
  GitHub-Namen** als Link, nicht die lokalen Versionsnamen.

### Tools ohne öffentliche Versionsnummer

Zeigen weder auf der Kachel noch im Overlay einen Versions-Chip (seit v1.9.0
ist der Chip optional). Sobald eine Nummer feststeht, einfach ins `version`-Feld
des Tools eintragen — der Chip erscheint dann automatisch wieder.

- **Speicher-Studio** — Dateiname endet auf `_aktuell`; lokal als v1.9.0 geführt.
- **DT-ProfiPassung (Test + Voll)** — wird laut Werbe-Grundlage erst kurz vor
  Verkauf festgelegt.
- **DT-ProfiSchweissnaht (Test + Voll)** — interner Programmstand N12 / Plan 2.70;
  öffentliche Nummer noch offen.

### Weitere Notizen

- Reihenfolge der Familien auf der Übersichtsseite aktuell: Lotto →
  EuroJackpot → Skip-Bo → DT-ProfiDreieck → DT-ProfiSchraube →
  DT-ProfiSchweissnaht → DT-ProfiPassung → Wärmeverlust-Analyse →
  Speicher-Studio. Bislang keine Rückmeldung, dass das geändert werden soll.
- **Werbe-Grundlage DT-ProfiSchweissnaht (Werbung.md, Stand 07.08.2026):** Die
  Kacheltexte halten sich an die dortige Verbotsliste. Nicht beworben werden
  Ermüdungsnachweis und Verzug/Schrumpfung (folgen als kostenpflichtiges Update);
  nicht verwendet werden normkonform, normgerecht, geprüft, zertifiziert,
  zugelassen, „ersetzt den Statiker", „vollständiger Nachweis" (er ist vollständig
  für die Naht, nicht für das Bauteil) und „kostenloses Update". Bei künftigen
  Textänderungen erneut dagegen prüfen.
- Keine bekannten offenen Bugs in den Einzeltools selbst (Stand dieser Notiz);
  diese Datei verfolgt nur die Übersichtsseite als aktuell aktives Projekt.
