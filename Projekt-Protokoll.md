# Skip-Bo KI Tuner – Projekt-Protokoll

> **⚠️ WICHTIG – Hinweis an Claude (lies dies zuerst!):**
>
> **Was du IMMER tun sollst sobald du dieses Projekt erkennst:**
> 1. Diese Datei (`Projekt-Protokoll.md`) als allererstes vollständig lesen
> 2. Bei Code-Fragen anschließend die relevanten HTML-Dateien im
>    Projektordner `/mnt/project/` aufrufen
> 3. Erst dann auf die Frage des Users antworten
>
> **Wann ist klar dass es das Skip-Bo-Projekt ist?**
> - Wenn der Projektordner `/mnt/project/` Skip-Bo-Dateien enthält (immer der Fall in diesem Projekt)
> - Wenn der User Begriffe wie "Tuner", "KONFIG", "Phase 1/2", "SkipBo", "v2.7", "BASE_GENES", "Turbo" verwendet
> - Wenn die Memory-Einträge auf Skip-Bo verweisen
>
> **Bei Unklarheiten:**
> - Schaue erst hier im Protokoll nach (Erkenntnisse in Abschnitt 4, Architektur in Abschnitt 9)
> - Dann prüfe Memory-Einträge zur Konversations-Historie
> - Schaue gegebenenfalls direkt in den Code (`/mnt/project/SkipBo_*.html`)
> - Erst dann den User fragen
>
> **Was im Protokoll steht – Was du direkt aus den Code-Dateien holen kannst:**
> - Konkrete KONFIG-Werte → KONFIG-Block in `SkipBo_6_6_0.html` (Modul 01, suche `let KONFIG = {`)
> - Aktuelle Tuner-Logik → `SkipBo_Tuner_v2_7.html`
> - Versionshistorie und Erkenntnisse → dieses Protokoll
> - Vereinbarungen über Arbeitsweise → dieses Protokoll
>
> **Dieses Protokoll wurde am 11. Juni 2026 vollständig neu geschrieben
> (Vorversion: 7. Mai 2026) und sollte bei größeren Entwicklungssprüngen
> aktualisiert werden.**

---

## 1. Was ist das Projekt?

Dieter (der User) entwickelt ein mobiles **Skip-Bo Kartenspiel** als einzige
HTML-Datei mit KI-Gegner. Parallel dazu existiert ein **KI-Tuner** der die
Score-Werte der KI mit genetischer Optimierung verbessert.

**Zwei Haupt-Komponenten:**
- **`SkipBo_6_6_0.html`** — die Spielversion die Dieter und Tester spielen
- **`SkipBo_Tuner_v2_7.html`** — der Tuner der die KI-Werte optimiert

Der Tuner gibt am Ende einen `let KONFIG = {...}` Block aus den der User in
die Spielversion kopiert. Umgekehrt wandelt der **BASE_GENES-Konverter** im
Tuner jeden KONFIG-Block zurück in einen `const BASE_GENES = {...}` Block –
damit wird das letzte Optimum zum Startpunkt des nächsten Laufs
(**Self-Tuning-Loop**). Beide Dateien teilen sich die identische
Engine-Logik: Der Tuner v2.7 simuliert exakt die KI der Spielversion 6.6.0.

---

## 2. Aktueller Projekt-Status (Stand 11. Juni 2026)

### Dateien im Projektordner `/mnt/project/`

| Datei | Größe | Zweck |
|-------|-------|-------|
| `SkipBo_6_6_0.html` | ~280 KB | Spielversion v6.6.0 – kompletter Neuaufbau in 17 Modulen (01–17). KONFIG-Block in Modul 01 (byte-identisch zu 6.5.9-Werten, Phase 1 vom 3.5.2026). NEU: Zugketten-Planer, 4 Sprachen, Live-Feldzähler. Drei kritische Bugs gefixt (siehe Abschnitt 3). |
| `SkipBo_Tuner_v2_7.html` | ~188 KB | Tuner v2.7 mit Turbo-Update. Engine = exakt 6.6.0 (Planer, Spiegel-Gegner). Mehrkern-Worker, Turbo-Sieben, Schieber-Empfehlung, Auto-Fokus, Mirror-Paare, ±Konfidenz. |
| `SkipBo_Tuner_v2_6_1_Handbuch.pdf` | ~3 MB | **Veraltet** (beschreibt v2.6). Achtung: Die Datei ist in Wahrheit ein ZIP mit 23 Seiten-Screenshots + Textdateien, kein echtes PDF. Wird durch `SkipBo_Tuner_v2_7_Handbuch.pdf` ersetzt. |
| `SkipBo_Test_Protokoll.html` | ~11 KB | Vorlage für Tester. 7 Abschnitte. Soll später überarbeitet werden (siehe offene Punkte). |
| `Projekt-Protokoll.md` | – | **Diese Datei.** |

### Was läuft gerade?

Dieter führt **Real-World-Tests mit mehreren Personen** durch – jetzt mit
der neuen Spielversion 6.6.0. Die Tester-Bugmeldungen der letzten Tage
("Baustapel plötzlich leer", verschwindende Felder) wurden alle auf echte
Code-Fehler zurückgeführt und behoben. Ein Tuner-Lauf gegen die neue
6.6.0-Engine steht noch aus.

---

## 3. Versionshistorie kurz (chronologisch)

### Spielversion
- **v6.5.0 → v6.5.9:** In vielen Schritten weiterentwickelt. v6.5.9 hatte
  Gruppe N (Gegner-Analyse), ⚙️-Menü, 5-Spiele-Auswertung, 86 Funktionen.
- **v6.6.0 (aktuell, 10.–11.6.2026):** Kompletter Neuaufbau als
  17-Modul-Struktur. Optik, Regeln und Meldungen 1:1 wie 6.5.9, KONFIG
  byte-identisch übernommen. Per Build-Pipeline aus Segmenten assembliert.
  - **KI-Verbesserungen:** Zugketten-Planer (Tiefensuche, garantierte
    Stock-Ketten VOR der Heuristik, eigener `KI_PLANNER`-Block),
    Sofort-Nachziehen bei leerer Hand mitten im Zug, Pflichtablage bewertet
    alle Handkarten × alle 4 Stapel, `predictEnemyStock` repariert
    (Doppel-Subtraktion + Joker-Zählung 18→12).
  - **FIX „Overlay-Bug":** Das Blockade-Overlay (⛔-Glow) saß als Klasse auf
    dem Baustapel-DIV; das Aufräumen per `el.remove()` löschte das ganze
    Feld. In 6.5.9 maskiert, weil die kaputte Gegner-Vorhersage fast nie ein
    Overlay setzte. Jetzt: `clearAiPredictionMarkers()` entfernt nur
    Klasse + Schildchen.
  - **FIX „Geister-KI" (kritisch):** `aiTurn_stockPriority` startete den
    KI-Zug rekursiv **ohne await** → zwei parallele KI-Stränge; der
    Spieler war scheinbar dran, während der Geister-Strang weiterspielte
    (Userbericht: "Baustapel plötzlich leer beim Legen"). Fix: awaited
    Rekursion + `restarted`-Flag + Wurzel-Wächter `aiTurnActive`.
  - **FIX Feld-Zähler:** „Stock (20)" / „Bau 1 (1)" standen seit Spielstart
    eingefroren im HTML – jetzt setzt `refreshFieldLabels()` sie bei jedem
    Render live (beim Bau inkl. nächstem benötigten Wert).
  - **NEU 🌐 Mehrsprachigkeit:** Menüpunkt „Sprache" mit Deutsch, English,
    Português, Українська. Architektur: Spiellogik bleibt deutsch;
    `showMessage` übersetzt zentral über Muster-Regeln (42 Vorlagen),
    statische Texte über Wörterbuch `t(key)`. Auswahl in
    localStorage `skipbo-lang`.

### Tuner-Entwicklung (alle relevanten Versionen)
- **v2.0–v2.3:** Schrittweiser Aufbau – Engine-Übernahme, Verifikation,
  Konvergenz-Erkennung. v2.3 (Gen 26): Fitness 848.0, WR 80% → BASE_GENES.
- **v2.4:** Volle v6.5.9-Engine, 4-Faktor-Fitness. **Problem Glücks-Drift**
  → führte zur Idee mit Anker-Spielen.
- **v2.5:** **Zwei-Phasen-Konzept + Anker-Spiele** als Lösung. Phase 1
  fand WR 65%, Stockabbau 17.6/20 (3.5.2026 – bis heute die BASE_GENES).
- **v2.6:** Verbesserte Bedienung (Regler je Phase, Live-Top-5,
  Verlaufs-Graph, Phase 1 wiederholbar). Am 8.5. kam der
  **BASE_GENES-Konverter** dazu (KONFIG → BASE_GENES).
- **v2.7 (10.6.2026) – Engine-Wechsel + Genauigkeitspaket:**
  - Engine = exakt Spiel 6.6.0 (Planer, neue Ablage, Sofort-Nachziehen)
  - **Spiegel-Gegner:** Der Gegner spielt dieselbe volle Engine mit
    BASE_GENES → Fitness misst reinen Parameter-Unterschied
  - **Mirror-Paare:** Jedes Anker-Deck 2× (normal + Seiten getauscht) –
    Kartenglück hebt sich auf
  - **Voll-deterministisch:** Auch das Nachmischen läuft über den Seed
  - **Margen-Fitness** (winRate·600 + stockNorm·250 + marginNorm·100 +
    consistency·50) + **±95%-Konfidenzintervall** bei jeder Win-Rate
  - Datenaustausch zu 6.6.0 hart bewiesen (71 Keys, Tausch real getestet)
- **v2.7 Turbo-Update (11.6.2026, gleiche Versionsnummer – kompatibel):**
  - 🧵 **Mehrkern:** Web-Worker-Pool (Engine wird aus dem eigenen
    `<script id="engine-code">` in Worker geladen, Fallback sequentiell
    mit identischen Zahlen)
  - ⚡ **Turbo-Sieben:** Vorrunde mit ⅓ der Decks siebt klar Schwache;
    Überlebende exakt vollbewertet (Teilsummen-Kombination); Sieb-Boden =
    vorab gemessene **BASE-Referenz** („📏" im Log)
  - 🎛️ **Schieber-Empfehlungs-Panel:** Nach jedem Lauf pro Regler
    🔼/⏸/🔽 + konkreter %-Wert + Vertrauen, per Klick übernehmbar
  - 🤖 **Auto-Fokus:** Mutation gewichtet erfolgreiche Abschnitte
    während des Laufs stärker
  - Lauf-Champion-Tracking (Empfehlungen auch ohne BASE-Schläger)

---

## 4. Wichtige Erkenntnisse aus der Entwicklung

### Async-Rekursion IMMER awaiten (Geister-KI-Lektion, 11.6.)
Ein `aiTurn(rek+1)` ohne `await` erzeugte einen unkontrollierten
Parallel-Strang – der gravierendste Bug des Projekts. Regel: Jede
async-Rekursion awaiten, der Aufrufer braucht ein Signal („restarted")
ob er selbst noch abschließen darf, plus Wurzel-Wächter gegen Doppelstarts.

### Latente Bugs werden durch Fixes „aktiviert"
Der Overlay-Lösch-Bug schlummerte seit 6.5.9 – erst der reparierte
`predictEnemyStock` machte ihn sichtbar. Bei Fixes immer fragen: Welche
toten Pfade werden dadurch lebendig?

### Dieters Beobachtungsstil ist zuverlässig
„Ab und zu funktioniert X nicht" oder ein einzelner Tester-Satz
(„Baustapel war plötzlich leer") haben jedes Mal zu einem echten,
reproduzierbaren Code-Fehler geführt. Solche Berichte ernst nehmen und
headless reproduzieren BEVOR gefixt wird.

### Spiegel-Gegner + Mirror-Paare eliminieren das Restglück
Seit v2.7 spielt der Gegner dieselbe Engine und jedes Deck wird gespiegelt
doppelt gespielt. Zusammen mit voll-deterministischen Anker-Spielen ist die
Fitness-Messung jetzt praktisch glücksfrei. Die alte Erkenntnis
(Anker-Spiele gegen Glücks-Drift) bleibt das Fundament.

### Headless-Testbarkeit ist der Qualitäts-Standard
Jede Änderung wird in Node mit DOM-Stubs getestet: Repro-Test VOR dem Fix
(Beweis), Regressionstest danach, plus Bestands-Suiten. Aktuelle Suiten in
`/home/claude/build/`: 28er-Smoke, 8er-Overlay, 7er-Geister, 19er-i18n,
42er-Tuner-Kompatibilität, 29er-Turbo, KONFIG-Tausch-Smoke.

### Kartenerhaltung als Invariante
Summe aller Karten (drawPile + Baustapel + Hände + Stocks + Ablagen) muss
konstant 156 sein – über 12er-Clears, komplette Züge, ganze Spiele. Starker
Generaltest gegen Schwund-Bugs.

### Tuner-kalibrierte Parameter nie „aufräumen"
Werte wie SCORE_44/SCORE_49 oder scheinbare No-ops sind vom Tuner
mitkalibriert. Nicht ohne explizite Entscheidung ändern – dokumentieren ja,
löschen nein.

### Real-Test ist die wichtigste Validierung
Tuner-Fitness ≠ echte Spielstärke. Erst Dieters Spielgefühl und die
Tester-Protokolle entscheiden.

### Strategie-Slider behutsam, jetzt mit Datenhilfe
Weiterhin gilt: nie mehrere Slider gleichzeitig stark verstellen. NEU:
Das 🎛️-Empfehlungs-Panel nach jedem Lauf liefert datenbasierte Vorschläge
pro Regler – der alte Trial-and-Error wird damit gezielter.

### DISCARD_LOOKAHEAD_DEPTH = 1 ist optimal
Mehrfach vom Tuner bestätigt. Höhere Werte bringen nichts Messbares.

---

## 5. Wie der User arbeitet

### Arbeitsumgebung
- Dieter arbeitet **vom Mobile aus** (Handy/Tablet) – kann Code nicht direkt
  editieren
- Tester verteilen sich auf mehrere Personen die Real-Spiele machen
- Browser-Konsole gelegentlich für Debug-Inspektion (Sekundär-Tool)

### Erwartungen an Claude
- **Vollständige Dateien als Output** – keine Diff-Snippets. Dieter braucht
  **die ganze HTML als fertige Datei zum Speichern**.
- **Jede Zeile sichtbar im Code** – keine Auslassungen mit "..."
- **Viele nützliche Kommentare** im Code (deutsch)
- **Style 1:1 zwischen Versionen beibehalten**
- **Versionsnummer explizit bestätigen** vor Lieferung
- **Alle technischen Entscheidungen delegiert Dieter an Claude** – Ziele
  und Constraints kommen von ihm, Umsetzung ohne Rückfragen wenn der
  Auftrag klar ist

### Bug-Reports
Dieter schreibt sehr präzise und reproduzierbar: Version, Aktion, Ergebnis,
Beobachtungen aus echten Spieltests, konkrete Werte als Beleg. Auch
weitergegebene Tester-Berichte sind verlässliche Bug-Indizien.

### Workflow
1. Dieter beschreibt Beobachtung oder Wunsch
2. Bei Großem zuerst Plan/Optionen besprechen, bei klaren Aufträgen direkt los
3. Claude baut, testet headless, liefert vollständige Datei
4. Datei via `present_files` ausgegeben
5. Dieter speichert, lädt in den Projektordner hoch, testet, meldet zurück

---

## 6. Wie Claude Code zur Verfügung stellt

### Standard-Vorgehen bei Änderungen
1. Stand aus `/mnt/project/` gegen eigene Arbeitskopie diffen (Verifikation)
2. Arbeitskopie in `/home/claude/` (Tuner) bzw. Segmente in
   `/home/claude/build/` (Spiel) bearbeiten – `str_replace` für kleine,
   Python-Skripte für große Blöcke
3. **Spiel:** `python3 assemble.py` baut `SkipBo_6_6_0.html` aus den
   Segmenten; Header-Changelog dort pflegen
4. **Syntax-Check Pflicht:** Script-Block(s) extrahieren → `node --check`
5. **Tests Pflicht:** Bei Bugfixes erst Repro-Test (rot), dann Fix (grün),
   dann alle Bestands-Suiten
6. Datei nach `/mnt/user-data/outputs/` kopieren + `present_files`
7. Lockere deutsche Zusammenfassung

### Build-Pipeline der Spielversion (in `/home/claude/build/`)
- Segmente: `js_a` (Konstanten/KONFIG) … `js_h` (Endgame/Menüs),
  `js_i_i18n.js` (Sprachen), dazu `body_block.txt`, `css`-Anteile,
  `konfig_block.txt` (byte-identische KONFIG-Referenz)
- `assemble.py` fügt alles zu `/home/claude/SkipBo_6_6_0.html` zusammen
- Test-Runner: `run_smoke.js`, `run_overlay_regression.js`, `run_ghost.js`,
  `run_i18n.js`, `run_swap_smoke.js`, `run_tuner_tests.js`,
  `run_turbo_tests.js` (+ zugehörige Stubs/Testkörper)

### Wichtige Engine/Tuner-Trennung (v2.7)
- **2-Script-Architektur:** `<script id="engine-code">` (TEIL B, komplette
  6.6.0-Sim inkl. `sim_evaluateGenesSums` + Worker-Botschafter) und TEIL C
  (GA, Pool, UI). Die id ist PFLICHT – daraus baut der Worker-Pool seinen
  Blob. Beide Blöcke separat `node --check`-en.
- Engine-Änderungen im Spiel müssen in die Tuner-Engine gespiegelt werden,
  sonst optimiert der Tuner gegen eine andere KI!

### Datenaustausch-Regeln (wichtig!)
- Tuner-Output `let KONFIG = {…};` ersetzt im Spiel NUR den KONFIG-Block
  in Modul 01 – **der `KI_PLANNER`-Block direkt darunter bleibt stehen**
  (wird nicht getunt, gehört nicht zum Tausch!)
- Rückweg: kompletten KONFIG-Block in den Konverter unten im Tuner →
  erzeugt `const BASE_GENES = {…};` → ersetzt den Block im Tuner
- Booleans: Spiel `true/false` ↔ Tuner-Gene `1/0` (Konverter regelt das)
- 71 KONFIG-Keys (inkl. DEBUG_N1–N4), 67 BASE_GENES-Keys (ohne DEBUG)

### LocalStorage-Keys (aktuelle)
- `skipbo_tuner_v27_phase1` – Phase-1-Ergebnis
- `skipbo_tuner_v27_best` – bestes Phase-2-/Gesamt-Ergebnis
- `skipbo-lang` – Sprachauswahl der Spielversion (de/en/pt/uk)

Bei neuen Versionen: Keys umstellen wenn Ergebnisse NICHT mehr vergleichbar
sind (wie v2.6→v2.7 wegen Engine-Wechsel). Bei kompatiblen Updates (wie dem
Turbo-Update) Versionsnummer und Keys behalten, Changelog im Datei-Header.

---

## 7. Aktuelle Score-Werte (BASE_GENES Stand 11.6.2026)

Unverändert das **Phase-1-Ergebnis vom 3.5.2026** (Generation 70,
WR 65%, Stockabbau 17.6/20) – identisch in beiden Dateien:

```
Wichtige Werte:
SCORE_1: 300, SCORE_2: 193, SCORE_3: 55
SCORE_5: 4912, SCORE_7: 3000, SCORE_10: 11867
SCORE_24: 27495 (Stock-Maximum-Score)
HAND_COMBO_BONUS_PER_CARD: 5000, HAND_COMBO_MIN_LENGTH: 4
DISCARD_LOOKAHEAD_DEPTH: 1
JOKER_STOCK_AGGRESSION: 0.24, JOKER_PROTECT_DISCARD: true
OPPONENT_BLOCK_WEIGHT: 0.00 (KI ignoriert Gegner-Blockade!)
```

**Bemerkenswerte Tuner-Strategien:** kein Gegner-Blockieren
(OPPONENT_BLOCK_WEIGHT 0), Hand-Ketten erst ab 4 Karten,
JOKER_COMBO_ENABLED: false.

**Achtung Fitness-Skala:** Die alte Fitness 609.7 stammt aus der
v2.6-Formel. Seit v2.7 gilt die **Margen-Fitness** gegen den
Spiegel-Gegner – Zahlen sind NICHT mit alten Läufen vergleichbar.
Referenzlinie ist jetzt die „📏 BASE-Referenz" im Log jedes Laufs.

---

## 8. Offene Punkte / Anstehende Themen

### Erster Tuner-Lauf gegen die 6.6.0-Engine
Die BASE_GENES wurden noch nie gegen den neuen Planer-Gegner optimiert.
Ein v2.7-Lauf (Szenario C) steht aus – gut möglich dass der Planer die
optimalen Parameter verschiebt.

### Real-Tests mit 6.6.0 laufen
Tester spielen die neue Version (inkl. der drei Bugfixes und Sprachen).
Ergebnisse abwarten, dann nächste Schritte entscheiden.

### Test-Protokoll überarbeiten (besprochen, noch nicht umgesetzt)
- **Auto-Fill aus eingefügter KONFIG** (Datum, Slider, Fitness, WR …)
- **Einfüge-Button-Problem** (Browser-Sicherheit, manuelles Einfügen nötig)
- **Phase-Erkennung:** Empfohlen war Option B – Tuner-Header gibt die
  Phase mit aus (in v2.7 noch nicht umgesetzt)
- **Phase-2-Daten** werden im Protokoll noch nicht erfasst
- **Datum-Konflikt:** Tuner-Datum vs. Test-Datum beide erhalten

### Handbuch-Datei im Projektordner ersetzen
`SkipBo_Tuner_v2_6_1_Handbuch.pdf` (ZIP-Screenshots) durch das neue echte
`SkipBo_Tuner_v2_7_Handbuch.pdf` ersetzen.

---

## 9. Technische Architektur-Details

### Spielversion 6.6.0
- **17 Module** (01 Konstanten/KONFIG/KI_PLANNER · 02 State · 03 Engine ·
  04 Rendering · 05 Overlay/Input · 06–09 Spielablauf · 10–11 KI-Steuerung
  + Zugketten-Planer · 12–13 Scoring + Gegner-Vorhersage · 14 Joker/Hand/
  Tiefenanalyse · 15 Endgame/Tuner-Tracking · 16 Menüs/Init · 17 🌐 i18n)
- **KI_PLANNER-Block** (Modul 01, direkt nach KONFIG): MAX_DEPTH 14,
  MAX_NODES 6000, MAX_JOKERS_PER_CHAIN 2, DISCARD_KEEP_COMBO_MALUS 400 –
  bewusst NICHT im Tuner-Suchraum
- **Wichtige neue Funktionen:** `planner_search/RunChains` (DFS-Ketten),
  `clearAiPredictionMarkers`, `refreshFieldLabels`, `aiTurnActive`-Guard,
  `translateMessage`/`t()`/`setLanguage` (Modul 17)
- **DEBUG-Flags:** nur `DEBUG_N1`–`DEBUG_N4`
- **i18n-Architektur:** showMessage-Hook → MSG_RULES (42 Regex-Vorlagen) +
  PHRASE_RULES; statisch via T-Wörterbuch; Ablage-Felder tragen die
  Strukturklasse `.discard-field` (Selektoren hängen NICHT mehr an
  deutschen data-labels!)

### Tuner v2.7
- **TEIL B** `<script id="engine-code">`: komplette 6.6.0-Sim (`sim_*`),
  `SIM_PLANNER`, `sim_swapSides` (Spiegel-Gegner), `sim_runOneGame(genes,
  oppGenes, seed, swapStart)`, `sim_evaluateGenesSums` (Summen-Evaluator),
  Worker-Botschafter (`self.onmessage` wenn kein `window`)
- **TEIL C:** `statsFromSums`/`combineSums` (Fitness zentral aus Summen),
  Worker-`POOL` (Blob aus engine-code, init mit BASE+Seeds, eval-Tasks),
  `evaluateGenerationParallel` (Racing: Stufe 1 = ⅓ Decks → Sieb gegen
  `evo_siftFloor` → Stufe 2 exakt kombiniert), `buildSliderAdvice`/
  `renderSliderAdvice`/`applyAdvisedSliders`, `updateAutoFocus` +
  `evo_focusW` in `mutate()`, `evo_runChampGenes` (Lauf-Champion),
  `computeBaseReference` (Cache, invalidiert bei neuem Anker-Pool)
- **Fitness:** winRate·600 + stockNorm·250 + marginNorm·100 +
  consistency·50; Skala 0–1000; ci95 = 1.96·SE der Win-Rate
- **Determinismus:** `SIM.rng` aus Seed (eigener Strom fürs Nachmischen);
  gleicher Seed ⇒ byte-gleiches Spiel
- **MS_PER_GAME = 14** (gemessen ~13 ms/Spiel in Node)
- **Checkboxen:** `cfg-turbo` (⚡), `cfg-autofocus` (🤖), beide default an

### Orientierung im Code
Zeilennummern verschieben sich bei jedem Edit – **nicht** auf gemerkte
Zeilen verlassen, sondern per `grep -n` auf Funktionsnamen/Anker suchen
(z.B. `let KONFIG = {`, `function aiTurn(`, `const BASE_GENES`,
`evaluateGenerationParallel`).

---

## 10. Tipps für Claude im neuen Chat

1. **Erst dieses Protokoll lesen**, dann `ls /mnt/project/`
2. **Bei Code-Änderungen:** Projektstand verifizieren (diff gegen eigene
   Historie wenn vorhanden), Arbeitskopie in `/home/claude/`, beim Spiel
   über die Build-Segmente + `assemble.py` gehen
3. **Nicht direkt im Projektordner schreiben** – read-only
4. **Bugfix-Disziplin:** Erst headless reproduzieren (Beweis), dann fixen,
   dann Regressionstest + alle Bestands-Suiten
5. **Engine-Parität wahren:** Spiel-KI-Änderung ⇒ Tuner-Sim nachziehen
6. **KONFIG-Tausch:** nur den KONFIG-Block, KI_PLANNER bleibt stehen
7. **User möchte ausführliche Erklärungen, lockerer Stil, viele Kommentare**
8. **Versions-Sprünge nicht überstürzen** – erst Plan, dann Bau
9. **Real-Test-Feedback > Tuner-Fitness** – im Zweifel auf Dieters
   Spielgefühl hören

---

## 11. Kontakt-Tonalität

- **Locker und freundlich** ("Du klickst auf...")
- **Auf Deutsch** (Code-Kommentare auch deutsch)
- **Emojis sparsam** (🎮 Spiel, 🧬 Tuner, ⚡ Turbo, ✅ Erledigt)
- **Bei großen Entscheidungen** erst Optionen vorstellen und dann fragen
- **Keine Schmeicheleien**, sondern fachliche Zusammenarbeit auf Augenhöhe

---

*Ende des Protokolls. Bei Updates: Datum oben aktualisieren und ggf.
einzelne Abschnitte überarbeiten.*
