# Projekt.md — Lotto-Tools (Zentrale Projektübersicht)

> **WICHTIG für jeden neuen Chat:** Diese Datei zuerst lesen. Sie beschreibt das
> Vorhaben, den aktuellen Stand und den Plan. Ergänzende technische Details zum
> JSON-Format stehen in **`LottoNumberFormat_Info.md`** (im selben Projektordner)
> — diese Datei immer mitlesen, wenn es um die Datenstruktur geht.

---

## 1. Worum geht es?

Es existieren zwei eigenständige HTML-Dateien (jeweils komplett selbst-enthalten,
ohne externe lokale Dateien, da Bedienung u. a. vom Handy aus erfolgt):

| Datei | Rolle | Kurzbeschreibung |
|-------|-------|------------------|
| `Lotto_Manager_Pro.html` | **Datenverwaltung** | Ziehungen laden, hinzufügen, suchen, löschen, als JSON speichern |
| `Lotto.html` | **Analyse / Prognose** | Häufigkeiten, Hot/Cold, Chi², Entropie, Übergangs-Heatmap, KI-Vorhersage, Dieter-Prognose + Auto-Optimierung |

Beide nutzen dieselben Lottodaten (Lotto 6aus49, Datenbestand ab 1955).

---

## 2. Das aktuelle Hauptziel (Phase 1)

**Umstellung beider Dateien auf das neue, immer aktuelle JSON-Format (Tidy).**

### Warum?
Bisher laden beide Dateien eine **Breitformat-Datei über eine GitHub-URL mit
festem Commit-Hash** → die Daten sind dadurch eingefroren und veralten.

Neuer Link (immer aktuell, ohne Commit-Hash, meist direkt nach jeder Ziehung
aktualisiert):

```
https://johannesfriedrich.github.io/LottoNumberArchive/Lottonumbers_tidy_complete.json
```

### Der Haken
Das neue Format ist das **Tidy-/Langformat** — strukturell anders als der
bestehende Code erwartet. Details siehe `LottoNumberFormat_Info.md`. Kurzfassung:

**Tidy-Format (NEU, zum Laden):** flaches Array, eine Zeile pro Zahl, kein Wrapper.
```json
[
  {"id":1,"date":"09.10.1955","variable":"Lottozahl","value":3},
  {"id":1,"date":"09.10.1955","variable":"Lottozahl","value":12},
  ...
  {"id":<n>,"date":"...","variable":"Superzahl","value":<0-9>}
]
```

**Breitformat (ALT, was der Code intern erwartet):**
```json
{ "data": [ { "id":1, "date":"09.10.1955", "Lottozahl":[3,12,13,16,23,41], "Superzahl":2 } ] }
```

### Lösungsansatz (sicher & minimal-invasiv)
Zwei kleine Konverter-Funktionen in **jeder** HTML (vollständig enthalten):

- **`tidyToWide(tidyArray)`** — wandelt direkt nach dem Laden das Tidy-Array in
  das alte Breitformat um. Dadurch bleibt **der gesamte restliche Code unverändert**
  (Analyse, Backtest, Optimierung, Manager-CRUD laufen weiter wie bisher).
- **`wideToTidy(wideData)`** — wandelt beim Speichern wieder zurück ins Tidy-Format.

**Robustheit:** Superzahl kann fehlen (frühe Ziehungen vor 1991 haben keine). Der
Konverter muss das sauber abfangen (Ziehung gilt als gültig, wenn genau 6
Lottozahlen vorhanden sind; Superzahl optional).

### Speicherformat (Entscheidung)
Gespeichert wird als **reines Tidy-Array** (flach, **ohne** `meta`-Wrapper) —
exakt identisch zum GitHub-Original. Vorteile:
- Gespeicherte Datei ist austauschbar mit dem Original, jederzeit wieder ladbar.
- **Erweiterbar:** Neue Datenarten werden einfach als neue `variable`-Werte
  ergänzt (z. B. `"Wochentag"`, `"Spiel77"`), ohne die Grundstruktur zu ändern.

---

## 3. Was muss aus dem Tidy-Format herausgefiltert werden?

Der bestehende Code benötigt pro Ziehung:
- **`id`** (Integer, fortlaufend)
- **`date`** (String `"TT.MM.JJJJ"`)
- **`Lottozahl`** — Array aus 6 Integers (alle Tidy-Zeilen mit `variable=="Lottozahl"`, gruppiert nach `id`)
- **`Superzahl`** — Integer 0–9 (Tidy-Zeile mit `variable=="Superzahl"`, falls vorhanden)

Gruppierungs-Logik: nach `id` zusammenfassen, `variable`/`value` in die
Zielfelder einsortieren, nach 6 Lottozahlen sortieren.

---

## 4. Rahmenbedingungen (gelten immer)

- **Vollständigkeit:** Sämtlicher Code (inkl. Konverter, Worker, Styles) muss in
  der jeweiligen HTML **komplett enthalten** sein. Kein Laden aus lokalen Pfaden.
- **Versionierung:** Beide angepassten Dateien starten **bei Version 1.0.0**.
  - Versionsnummer als **Kommentar am Anfang** der HTML (mit Stand/Datum + Changelog-Zeile).
  - Versionsnummer **sichtbar in der Oberfläche** anzeigen.
  - Bei Weiterentwicklung hochzählen (1.0.1, 1.1.0, …).
- **Qualität:** Code sorgfältig prüfen, ob alles korrekt zusammenarbeitet. In
  jeder Phase ausgiebig testen, Bugs ausschließen.
- **Funktionsgleichheit:** Nach Phase 1 müssen beide Dateien **exakt** so
  funktionieren wie bisher — nur mit dem neuen Format.

---

## 5. Reihenfolge der Umsetzung (Phase 1)

1. **`Lotto_Manager_Pro.html` zuerst** (erzeugt/verwaltet die Daten; hier müssen
   Laden *und* Speichern im neuen Format getestet werden).
2. **`Lotto.html` danach** (Analyse; nutzt dieselbe `tidyToWide`-Logik).

Pro Datei: Konverter einbauen → Lade-Funktion auf neuen Link umstellen →
Speichern auf Tidy umstellen → testen → Version auf 1.0.0 + sichtbar machen.

---

## 6. Nebenwunsch (nicht vorrangig)

Im `Lotto_Manager_Pro.html` lädt „Aktuelle Ziehung" über den WestLotto-RSS-Feed.
Das funktioniert **in Deutschland**, aber **nicht in Portugal** (vermutlich
Geo-/CORS-Blockade). Schön wäre eine Lösung, die auch aus Portugal funktioniert
(z. B. robusterer Proxy-Fallback oder alternative Quelle). **Niedrige Priorität** —
zuerst läuft die Format-Umstellung.

> **Hinweis:** Sobald der neue Tidy-Link genutzt wird, ist die „aktuelle Ziehung"
> ohnehin meist schon in den Daten enthalten (Datei ist nach jeder Ziehung aktuell).
> Der RSS-Abruf wird dadurch teils überflüssig — das beim Neubau bedenken.

---

## 7. Zukunftsplanung (Phase 2+) — schon jetzt mitdenken

### 7a. Kompletter Neubau beider Dateien
- Von Grund auf neu, nach besten aktuellen Methoden, **leicht erweiterbar**.
- **Optimal & schnell** auf Handy, Laptop, PC (responsives Design).
- Beste Darstellung (CSS oder bessere Methoden — Entscheidung beim Neubau).
- **Overlay-/Modal-Fenster** für bessere Handy-Darstellung in Betracht ziehen
  (Funktionsbereiche per Klick öffnen statt alles auf einer langen Seite).
- Saubere Trennung: Datenschicht (Laden/Konvertieren/Speichern) ↔ Analyse ↔ UI,
  damit Erweiterungen einfach einzuhängen sind.

### 7b. Zusammenführung zu einer Gesamt-HTML
- `Lotto.html` als Basis; den Manager als **Overlay** integrieren.
- Idee: Ein Overlay öffnet automatisch **12 Spielfelder** (optisch wie das
  Klick-Raster im Manager) und füllt sie mit den besten berechneten Tipps.
- Berechnete Zahlen per **Button** in die Spielfelder übernehmen (oder ähnliche
  Mechanik).
- Diese Integration **bereits in der Architektur des Neubaus berücksichtigen**
  (z. B. wiederverwendbare „Spielfeld-Komponente", gemeinsame Datenschicht).

---

## 8. Vorschläge für nützliche Erweiterungen (Backlog, später)

Kandidaten für zusätzliche Auswertungen/Anzeigen (nach und nach):
- **Wochentag** der Ziehung (Mi/Sa) aus dem Datum → getrennte Statistiken.
- **Letzte Ziehung sichtbar anzeigen** (Datum + Zahlen) als Kontrolle, dass
  aktuelle Daten geladen wurden.
- **Gerade/Ungerade-** und **Hoch/Niedrig-Verteilung** als zusätzliche Filter.
- **Zahlensumme** pro Tipp (typische Gewinnsummen liegen in einem Bereich).
- **Paar-/Nachbarschaftsanalyse** (welche Zahlen treten oft gemeinsam auf).
- **Spiel77/Super6** falls im Datenformat verfügbar (prüfen).

> Grundhaltung des Projekts: Lottozahlen sind nicht real vorhersagbar. Ziel ist,
> aus vielen Daten **Wahrscheinlichkeiten** einzugrenzen — Zufall mit
> Wiederholungen. Prognose-Qualität soll schrittweise verbessert werden. Erst
> muss aber alles wie bisher laufen (nur mit neuem Format).

---

## 9. Statusübersicht

| Aufgabe | Status |
|---------|--------|
| Projekt.md angelegt | ✅ erledigt |
| JSON-Format dokumentiert (`LottoNumberFormat_Info.md`) | ✅ vorhanden |
| Konverter-Konzept festgelegt (`tidyToWide` / `wideToTidy`) | ✅ geplant |
| `Lotto_Manager_Pro.html` auf Tidy umstellen (v1.0.0) | ✅ erledigt |
| `Lotto.html` auf Tidy umstellen (v1.0.0) | ✅ erledigt |
| **v1.0.1 beide:** Selbstschliessende Toasts | ✅ erledigt |
| **v1.0.1 Analyzer:** Auto-Analyse nach Laden | ✅ erledigt |
| **v1.0.1 Analyzer:** Optimierung 16–56× schneller (identisches Ergebnis) | ✅ erledigt |
| **v1.0.1 Analyzer:** Letzte Ziehung sichtbar | ✅ erledigt |
| **v1.0.1 Manager:** Auto-Laden beim Start + zeitversetzt aktuelle Ziehung | ✅ erledigt |
| **v1.0.1 Manager:** Sprungleiste (Erster/Letzter/zu ID) + lesbare Liste | ✅ erledigt |
| Portugal-Tauglichkeit „Aktuelle Ziehung" (mehrere Proxy-Fallbacks) | ✅ erledigt (v1.0.1, Test im Ausland steht aus) |
| Neubau Analyzer responsiv + Overlays (Phase 2) → **Lotto_2-0-0.html** | ✅ erledigt |
| **v2.0.0:** 4 neue Auswertungen (Wochentag, Gerade/Ungerade, Hoch/Niedrig, Summe) | ✅ erledigt |
| **v2.0.0:** Engine geprüft — identische Ergebnisse wie v1 (Dieter/KI/Chi²/Optimizer) | ✅ erledigt |
| Neubau Manager responsiv + Overlays (Phase 2) → **Lotto_Manager_Pro_2-0-0.html** | ✅ erledigt |
| **Manager v2.0.0:** CRUD geprüft — identisches Verhalten wie 1.0.1 | ✅ erledigt |
| **Analyzer v2.0.1:** Superzahl per Defizit-Logik für Dieter & KI (ab 1991), 7. Kugel | ✅ erledigt |
| **Analyzer v2.0.1:** Coupon-Vorschau führt Superzahl separat + Ring bei Überschneidung | ✅ erledigt |
| **Analyzer v2.0.2:** Backtest bewertet Superzahl getrennt (Trefferquote, Zufall ~10 %) | ✅ erledigt |
| **Analyzer v2.0.3:** 12 Spielfelder (3 Methoden + 9 Variationen), gemeinsame Superzahl, bearbeitbar + würfeln | ✅ erledigt |
| Entscheidung: Manager bleibt eigenständig, nur Spielfelder wandern in den Analyzer | ✅ entschieden |
| **Analyzer v2.0.4:** Optimierungszeitraum einstellbar (letzte N statt fest 50) | ✅ erledigt |
| **Analyzer v2.0.4:** Übernehmen-Buttons (Dieter/KI → wählbares Feld 1–12 + Superzahl) | ✅ erledigt |

> Diese Tabelle in jedem Chat aktuell halten, wenn sich der Stand ändert.

---

## 10. Wichtige Referenzen

- **Neuer Daten-Link (Tidy, immer aktuell):**
  `https://johannesfriedrich.github.io/LottoNumberArchive/Lottonumbers_tidy_complete.json`
- **Projektseite mit allen Infos:**
  `https://johannesfriedrich.github.io/LottoNumberArchive/`
- **Repository:**
  `https://github.com/JohannesFriedrich/LottoNumberArchive`
- **Format-Detaildoku:** `LottoNumberFormat_Info.md` (im Projektordner)
