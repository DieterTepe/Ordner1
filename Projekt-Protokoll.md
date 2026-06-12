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
> - Wenn der Projektordner `/mnt/project/` Skip-Bo-Dateien enthält
> - Wenn der User Begriffe wie "Tuner", "KONFIG", "Phase 1/2", "SkipBo",
>   "BASE_GENES", "Turbo", "Spielstärke", "Suchraum" verwendet
> - Wenn die Memory-Einträge auf Skip-Bo verweisen
>
> **Bei Unklarheiten:**
> - Erst hier im Protokoll nachschauen (Abschnitt 4 = Erkenntnisse,
>   Abschnitt 9 = Architektur-Details)
> - Dann Memory-Einträge und ggf. den Code direkt prüfen
> - Erst dann den User fragen
>
> **Dieses Protokoll wurde am 12. Juni 2026 vollständig aktualisiert.**

---

## 1. Was ist das Projekt?

Dieter (der User) entwickelt ein mobiles **Skip-Bo Kartenspiel** als einzige
HTML-Datei mit KI-Gegner. Parallel dazu existiert ein **KI-Tuner** der die
Score-Werte der KI mit genetischer Optimierung verbessert.

**Zwei Haupt-Komponenten:**
- **`SkipBo_6_6_0.html`** — die Spielversion
- **`SkipBo_Tuner_v2_7.html`** — der Tuner (inkl. Turbo-Update v2.7b)

Der Tuner gibt am Ende einen `let KONFIG = {...}` Block aus den der User in
die Spielversion kopiert. Umgekehrt wandelt der **BASE_GENES-Konverter** im
Tuner jeden KONFIG-Block zurück in `const BASE_GENES = {...}` – damit wird
das letzte Optimum zum Startpunkt des nächsten Laufs (**Self-Tuning-Loop**).
Beide Dateien teilen dieselbe Engine-Logik: Der Tuner v2.7 simuliert exakt
die KI der Spielversion 6.6.0.

---

## 2. Aktueller Projekt-Status (Stand 12. Juni 2026)

### Dateien im Projektordner `/mnt/project/`

| Datei | Größe | Zweck |
|-------|-------|-------|
| `SkipBo_6_6_0.html` | ~280 KB | Spielversion v6.6.0 – 17-Modul-Neuaufbau, KONFIG in Modul 01, KI_PLANNER-Block direkt darunter, 4 Sprachen (DE/EN/PT/UK), 3 kritische Bugs gefixt (Overlay, Geister-KI, Feldzähler). |
| `SkipBo_Tuner_v2_7.html` | ~197 KB | Tuner v2.7 + Turbo-Update + v2.7b-Feinschliff. Engine = exakt 6.6.0. Mehrkern-Worker, Turbo-Sieben, Schieber-Empfehlung, Auto-Fokus, Mirror-Paare, ±Konfidenz, Suchraum-Dehnung. Anzeigen: „Spielstärke" statt „Fitness". |
| `SkipBo_Tuner_v2_7_Handbuch.pdf` | ~95 KB | Echtes PDF (18 Seiten, A4), beschreibt v2.7b vollständig. |
| `Projekt-Protokoll.md` | – | **Diese Datei.** |
| `SkipBo_Test_Protokoll.html` | ~11 KB | Vorlage für Tester. Soll noch überarbeitet werden. |

### Was läuft gerade?

Real-World-Tests mit SkipBo_6_6_0.html laufen gut. Tuner v2.7b läuft stabil.
Ein erster Tuner-Lauf speziell gegen die neue 6.6.0-Engine (mit Planer) steht
noch aus – die aktuellen BASE_GENES stammen noch aus dem Phase-1-Lauf vom
3.5.2026 (vor dem Zugketten-Planer).

---

## 3. Versionshistorie (chronologisch)

### Spielversion
- **v6.5.0 → v6.5.9:** Schrittweise Entwicklung, 86 Funktionen, Gruppen A–N,
  Settings-Menü, 5-Spiele-Auswertung.
- **v6.6.0 (10.–11.6.2026):** Kompletter Neuaufbau als 17-Modul-Struktur per
  Build-Pipeline. Optik/Regeln/Meldungen 1:1 wie 6.5.9, KONFIG byte-identisch.
  - **KI-Verbesserungen:** Zugketten-Planer (DFS, MAX_DEPTH 14, MAX_NODES 6000,
    eigener KI_PLANNER-Block), Sofort-Nachziehen, neue Pflichtablage (alle
    Handkarten × alle 4 Stapel), `predictEnemyStock` repariert.
  - **FIX Overlay-Bug:** `.ai-prediction-overlay` saß auf Baustapel-DIV → `el.remove()`
    löschte ganze Felder. Fix: `clearAiPredictionMarkers()` entfernt nur Klasse + Tags.
  - **FIX Geister-KI (kritisch):** `aiTurn_stockPriority` startete KI-Zug ohne
    `await` → zwei parallele Stränge → Baustapel leerde sich scheinbar grundlos
    mitten im Spielerzug. Fix: awaited Rekursion + `restarted`-Flag + `aiTurnActive`-Guard.
  - **FIX Feldzähler:** „Stock (20)" standen eingefroren → `refreshFieldLabels()`
    setzt sie jetzt bei jedem Render live (inkl. nächstem benötigten Wert).
  - **NEU 🌐 Mehrsprachigkeit:** Menüpunkt „Sprache", 4 Sprachen (DE/EN/PT/UK),
    42 Meldungsvorlagen, Wörterbuch `t(key)`. Key: `skipbo-lang`.

### Tuner-Entwicklung
- **v2.0–v2.4:** Aufbau. v2.3 (Gen 26): Spielstärke 848, WR 80 %. v2.4:
  volle 6.5.9-Engine, 4-Faktor-Spielstärke. Problem: Glücks-Drift.
- **v2.5 (3.5.2026):** **Anker-Spiele + Zwei-Phasen-Konzept.** Phase 1 fand
  WR 65 %, Stockabbau 17.6/20 → bis heute die BASE_GENES.
- **v2.6:** Regler je Phase, Live-Top-5, Verlaufs-Graph, Phase 1 wiederholbar,
  BASE_GENES-Konverter (8.5.).
- **v2.7 (10.6.2026) – Engine-Wechsel + Genauigkeitspaket:**
  - Engine = exakt Spiel 6.6.0 (Planer, neue Ablage, Sofort-Nachziehen)
  - Spiegel-Gegner (Gegner spielt volle Engine mit BASE_GENES)
  - Mirror-Paare (jedes Deck 2× normal + gespiegelt, Kartenglück hebt sich auf)
  - Voll-deterministisch (Nachmischen über Seed), Margen-Spielstärke (·600/250/100/50) + ±95%-CI
  - Datenaustausch zu 6.6.0 hart bewiesen (71 Keys, real getauscht + Smoke grün)
- **v2.7 Turbo-Update (11.6.2026):**
  - 🧵 Mehrkern-Worker (Engine aus `<script id="engine-code">` als Blob, Fallback sequentiell)
  - ⚡ Turbo-Sieben (Vorrunde ⅓ Decks, Sieb-Boden = BASE-Referenz evo_siftFloor)
  - 🎛️ Schieber-Empfehlungs-Panel (Korrelation + Champion-Profil, 🔼/⏸/🔽 + %, Übernehmen-Button)
  - 🤖 Auto-Fokus (Mutation gewichtet je Abschnitt lernend)
  - Lauf-Champion-Tracking (`evo_runChampGenes`), BASE-Referenz-Cache
- **v2.7b (12.6.2026) – Feinschliff & kritischer Fix:**
  - **FIX 🆚 Endvergleich (kritisch):** Verlaufszeile griff auf entfernte
    Einzelspiel-Variablen zu → ReferenceError → Vergleich brach STILL ab,
    kein Banner, `cmp_running` blieb hängen, jeder Folge-Vergleich blockiert.
    Fix: Paket-Verlauf aus Summen, `try/finally`-Absicherung, klare
    Gleichstand-Entscheidung per Stockabbau.
  - **🧱 Suchraum-Dehnung:** Klebt Champion an GENE_LIMITS-Grenze → Limit
    weitet sich automatisch (×1.5/Treffer, max 3× Original, persistiert via
    `skipbo_tuner_v27_limits`, per Checkbox abschaltbar, Reset stellt Original
    wieder her). Anschlag-Warnung in Panel + Log.
  - 🎛️ Empfehlungs-Panel: „Treiber im Detail" (Top-6-Einzelgene des Champions),
    Anschlag-Hinweis mit Dehnungs-Status; Panel + Top-5 vertikal scrollbar
    (Mobil-Fix). Tabelle hat `min-width:560px` (kein Abschneiden).
  - 📊 „Fitness" → „Spielstärke" überall in sichtbaren Texten/Logs (Skala
    unverändert 0–1000; interne Variablennamen unverändert).
  - resetAll räumt alle neuen States + gedehnte Limits + Panel.

---

## 4. Wichtige Erkenntnisse aus der Entwicklung

### Stille Fehler sind die gefährlichsten
Der Vergleichs-Bug (v2.7b) ist das beste Beispiel: kein Crash, keine sichtbare
Fehlermeldung – der Vergleich brach einfach ab, das Banner blieb leer.
Regel: Jede kritische Funktion in einen `try/finally`-Block, und Tests müssen
das **Ergebnis** prüfen, nicht nur „es stürzt nicht ab".

### Async-Rekursion IMMER awaiten (Geister-KI-Lektion)
Ein `aiTurn(rek+1)` ohne `await` → unkontrollierter Parallel-Strang → KI
legte Karten im Spielerzug. Jede async-Rekursion awaiten, Aufrufer braucht
ein „restarted"-Signal, Wurzel-Wächter gegen Doppelstarts.

### Latente Bugs werden durch Fixes „aktiviert"
Overlay-Bug schlummerte seit 6.5.9 – erst der reparierte `predictEnemyStock`
machte ihn sichtbar. Bei Fixes immer fragen: Welche toten Pfade werden lebendig?

### Suchraum-Grenzen können das Ergebnis verzerren
Wenn wiederholte Läufe Werte an die GENE_LIMITS-Grenze drücken, kann die
Suche nicht mehr über die Grenze hinaus – das ist systematisch falsch.
Deshalb jetzt: Anschlag-Erkennung + automatische Dehnung.

### Headless-Testbarkeit ist der Qualitäts-Standard
Jede Änderung wird in Node mit DOM-Stubs getestet. Aktuelle Suiten in
`/home/claude/build/`: 28er-Smoke (Spiel), 8er-Overlay, 7er-Geister, 19er-i18n,
42er-Tuner-Kompatibilität, 29er-Turbo, 34er-v2.7b, KONFIG-Tausch-Smoke.
**Testprinzip:** Repro-Test VOR dem Fix (Beweis, dass Bug existiert), danach
Regressionstest + alle Bestands-Suiten.

### Spiegel-Gegner + Mirror-Paare eliminieren das Restglück
Seit v2.7: Gegner spielt volle Engine, jedes Deck gespiegelt. Zusammen mit
deterministischen Anker-Spielen ist die Spielstärke-Messung praktisch glücksfrei.

### Vergleichs-Zahlen müssen exakt stimmen
Der neue Test-Ansatz für runComparison: dieselbe Rechnung parallel über die
Engine als Referenz laufen lassen und UI-Werte dagegen prüfen. Garantiert, dass
„Neue KONFIG ist besser!" auch wirklich besser bedeutet.

### Dieters Beobachtungsstil ist zuverlässig
Präzise Beschreibungen (Version + Aktion + Ergebnis) haben jeden Bug auf einen
echten Code-Fehler zurückgeführt. Auch scheinbar kleine Meldungen ernst nehmen.

### Real-Test > Tuner-Spielstärke
Tuner-Punktzahl ≠ echte Spielstärke. Erst Dieters Spielgefühl und Tester-
Protokolle entscheiden.

---

## 5. Wie der User arbeitet

### Arbeitsumgebung
- **Mobil-first:** Dieter entwickelt und testet vom Handy/Tablet
- Code kann nicht direkt editiert werden → Claude liefert vollständige Dateien
- Browser-Konsole gelegentlich für Debug-Inspektion

### Erwartungen an Claude
- **Vollständige Dateien** (keine Diffs, keine Auslassungen)
- **Alle technischen Entscheidungen** delegiert an Claude mit Ziele + Constraints
- **Viele Kommentare** im Code (deutsch)
- Vor großen Umbauten: erst Plan/Optionen, dann Bau
- Bei Verbesserungsvorschlägen: erst Meinung äußern, dann auf Bestätigung warten

### Workflow
1. Dieter beschreibt Beobachtung, Wunsch oder Bug
2. Claude plant (bei Großem), baut, testet headless, liefert vollständige Datei
3. Datei via `present_files` ausgegeben
4. Dieter speichert, lädt in den Projektordner hoch, testet, meldet zurück

---

## 6. Wie Claude Code zur Verfügung stellt

### Standard bei Änderungen
1. Projektstand aus `/mnt/project/` in `/home/claude/` kopieren und verifizieren
2. Änderungen per `str_replace` (klein) oder Python-Skript (groß)
3. **Spiel:** `python3 assemble.py` in `/home/claude/build/`; Segmente `js_a…js_i`
4. **Syntax-Pflicht:** Script-Blöcke extrahieren → `node --check`
5. **Test-Pflicht:** Repro → Fix → Regression → alle Suiten
6. Datei nach `/mnt/user-data/outputs/` + `present_files`

### Build-Pipeline Spiel (`/home/claude/build/`)
Segmente `js_a`…`js_h` + `js_i_i18n.js`, `body_block.txt`, `css`, `konfig_block.txt`
→ `assemble.py` → `/home/claude/SkipBo_6_6_0.html`

### 2-Script-Architektur des Tuners (WICHTIG)
- **TEIL B** `<script id="engine-code">`: komplette 6.6.0-Sim (`sim_*`), `SIM_PLANNER`,
  `sim_swapSides`, `sim_runOneGame(genes, oppGenes, seed, swapStart)`,
  `sim_evaluateGenesSums`, Worker-Botschafter.
  Die `id="engine-code"` ist PFLICHT – Pool-Builder holt den Blob daraus.
- **TEIL C:** GA, Pool, UI, Analytics, Vergleich, Phasen.
- Beide Blöcke separat `node --check`-en.
- Engine-Änderungen im Spiel müssen in die Tuner-Sim gespiegelt werden!

### Datenaustausch-Regeln (kritisch!)
- Tuner-Output `let KONFIG = {…};` → ins Spiel: **nur KONFIG-Block ersetzen**,
  `KI_PLANNER`-Block direkt darunter **bleibt stehen** (wird nicht getunt!)
- Rückweg: KONFIG-Block in Konverter → `const BASE_GENES = {…};` → in Tuner ersetzen
- Booleans: Spiel `true/false` ↔ Tuner-Gene `1/0` (Konverter regelt)
- 71 KONFIG-Keys (inkl. DEBUG_N1–N4), 67 BASE_GENES-Keys (ohne DEBUG)

### LocalStorage-Keys (aktuell)
| Key | Inhalt |
|-----|--------|
| `skipbo_tuner_v27_phase1` | Phase-1-Ergebnis |
| `skipbo_tuner_v27_best` | Bestes Phase-2-/Gesamt-Ergebnis |
| `skipbo_tuner_v27_limits` | Gedehnte Suchraum-Grenzen (neu v2.7b) |
| `skipbo-lang` | Sprachauswahl Spielversion (de/en/pt/uk) |

---

## 7. Aktuelle Score-Werte (BASE_GENES Stand 12.6.2026)

Unverändert **Phase-1-Ergebnis vom 3.5.2026** (Gen 70, WR 65 %, Stockabbau 17.6/20).
War noch nicht gegen die 6.6.0-Engine (mit Planer) optimiert – erster v2.7-Lauf steht aus.

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

**Bemerkenswert:** kein Gegner-Blockieren, Hand-Ketten erst ab 4, JOKER_COMBO_ENABLED false.
**Achtung:** Spielstärke-Skala (0–1000) ist seit v2.7 nicht mit v2.6-Zahlen vergleichbar
(Margen-Spielstärke gegen Spiegel-Gegner). Referenzlinie = „📏 BASE-Referenz" im Log.

---

## 8. Offene Punkte / Anstehende Themen

### Erster Tuner-Lauf gegen 6.6.0-Engine
BASE_GENES wurden nie gegen den Zugketten-Planer optimiert. Ein v2.7-Lauf
(Szenario C) steht aus.

### Real-Tests laufen
Tester spielen 6.6.0 – Ergebnisse abwarten, dann nächste Schritte.

### Test-Protokoll überarbeiten
- Auto-Fill aus eingefügter KONFIG
- Einfüge-Button-Problem (Browser-Sicherheit)
- Phase-Erkennung: Option B (Tuner-Header gibt Phase mit aus)
- Phase-2-Daten werden noch nicht erfasst

### Handbuch im Projektordner
`SkipBo_Tuner_v2_7_Handbuch.pdf` wurde durch echtes PDF ersetzt (v2.7b-Stand).

---

## 9. Technische Architektur-Details

### Spielversion 6.6.0
- **17 Module:** 01 Konstanten/KONFIG/KI_PLANNER · 02 State · 03 Engine ·
  04 Rendering · 05 Overlay/Input · 06–09 Spielablauf · 10–11 KI-Steuerung +
  Planer · 12–13 Scoring + Vorhersage · 14 Joker/Hand/Tiefe · 15 Endgame/Tracking ·
  16 Menüs/Init · 17 🌐 i18n
- **KI_PLANNER-Block** (Modul 01, direkt nach KONFIG): MAX_DEPTH 14,
  MAX_NODES 6000, MAX_JOKERS 2, DISCARD_KEEP_COMBO_MALUS 400 – nicht getunt!
- **i18n:** showMessage → `translateMessage()` (42 MSG_RULES) + `t(key)` Wörterbuch.
  Strukturklasse `.discard-field` (nicht mehr an deutschen data-labels!)
- **Wichtige Funktionen:** `clearAiPredictionMarkers`, `refreshFieldLabels`,
  `aiTurnActive`-Guard, `translateMessage`/`setLanguage`

### Tuner v2.7b
- **Spielstärke-Formel:** winRate·600 + stockNorm·250 + marginNorm·100 + consistency·50
- **Suchraum-Dehnung:** `ORIG_LIMITS`, `GENE_LIMITS` (zur Laufzeit dehnbar),
  `maybeStretchLimits()`, `detectLimitHits()`, `persistStretchedLimits()`,
  `loadStretchedLimits()`, `restoreOriginalLimits()`.
  Nur „echte Wertspannen" (> 10 als Obergrenze) werden gedehnt, keine Flags/Anteile.
- **Vergleich:** `runComparison(neueGenes, fixedSeeds?)` – fixedSeeds für Tests.
  Paket-Verlauf aus `so.wins/sn.wins`, `try/finally` → `cmp_running` immer frei.
  Gleichstand → Stockabbau entscheidet (mit klarer Empfehlung).
- **Panel:** `buildSliderAdvice()` → `fineDrivers` (Top-6-Einzelgene) + `hitTxt`
  (Anschlag-Warnung). `renderSliderAdvice()` → scrollbares HTML.
- **MS_PER_GAME = 14** (gemessen ~13 ms/Spiel)
- **Checkboxen:** `cfg-turbo`, `cfg-autofocus`, `cfg-stretch` (alle default AN)

### Orientierung im Code
Zeilennummern verschieben sich – immer per `grep -n` suchen:
`let KONFIG = {`, `const KI_PLANNER`, `function aiTurn(`, `const BASE_GENES`,
`evaluateGenerationParallel`, `async function runComparison`, `maybeStretchLimits`

---

## 10. Tipps für Claude im neuen Chat

1. Erst dieses Protokoll lesen, dann `ls /mnt/project/`
2. Projektstand verifizieren (diff gegen Output oder bekannte Stände)
3. Arbeitskopie in `/home/claude/`, beim Spiel über Segmente + `assemble.py`
4. `/mnt/project/` ist read-only, nie direkt schreiben
5. Bugfix-Disziplin: erst headless reproduzieren, dann fixen, dann Regression + Suiten
6. Engine-Parität wahren: Spiel-KI-Änderung → Tuner-Sim nachziehen
7. KONFIG-Tausch: nur KONFIG-Block, KI_PLANNER bleibt stehen
8. Vergleichs-Tests: Zahlen gegen direkte Engine-Referenz prüfen (nicht nur „kein Crash")
9. Real-Test-Feedback > Tuner-Spielstärke

---

## 11. Kontakt-Tonalität

- **Locker und freundlich** auf Deutsch
- **Emojis sparsam** (🎮 Spiel, 🧬 Tuner, ⚡ Turbo, ✅ Erledigt, 🧱 Suchraum)
- **Bei Vorschlägen:** erst Meinung äußern, auf Bestätigung warten
- **Keine Schmeicheleien**, fachliche Zusammenarbeit auf Augenhöhe

---

*Ende des Protokolls. Stand: 12. Juni 2026.*
