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

## 1. Projekt-Familien — Stand 27.06.2026

| Projekt | Version | Struktur | Link |
|---|---|---|---|
| Lotto 6aus49 — Analyse-Konsole | 2.1.0 | Einzeldatei | dietertepe.github.io/Lotto/Lotto_2-1-0.html |
| Lotto 6aus49 — Daten-Manager | 2.0.0 | Einzeldatei | dietertepe.github.io/Lotto/Lotto_Manager_Pro_2-0-0.html |
| EuroJackpot — Analyse-Konsole | 1.0.1 | Einzeldatei | dietertepe.github.io/Eurolotto/Eurolotto_1-0-1.html |
| EuroJackpot — Daten-Manager | 0.1.8 | Einzeldatei | dietertepe.github.io/Eurolotto/EuroJackpot_Manager_0-1-8.html |
| Skip-Bo — Basisversion | 6.6.0 | Einzeldatei | dietertepe.github.io/Ordner1/SkipBo_6_6_0.html |
| Skip-Bo — Klassisches Kartenspiel | 7.0.0 | Einzeldatei | dietertepe.github.io/Skipo/SkipBo_7_0_0.html |
| Skip-Bo — KI-Tuner | 2.7 (Turbo + 2.7b) | Einzeldatei | dietertepe.github.io/SkipBo_Tuner/SkipBo_Tuner_v2_7.html |
| DT-ProfiDreieck (Test & Pro) | 1.1.0 (Engine 3.0.0) | Einzeldatei | dt-profidreieck.de |
| Wärmeverlust- & Gebäude-Analyse (Heizungs-Check) | 1.0 | Einzeldatei | dietertepe.github.io/Heizungsanlage/waermeverlust.html |

Volltexte (Was es kann / Was es auszeichnet) zu jedem dieser Tools stehen in
`info_1.md` — dort bei Bedarf nachschlagen, nicht hier duplizieren.

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
- **Design:** Dunkles Konsolen-/Schaltpult-Design. Fünf Akzentfarben nach
  Projektfamilie (Lotto = Gold, EuroJackpot = Türkis, Skip-Bo = Karmesinrot,
  DT-ProfiDreieck = Stahlblau-Grau, Wärmeverlust-Analyse = Ember-Orange).
- **Stand v1.4.0 (fertig):**
  - Alle 9 Tools als Kacheln, gruppiert nach Familie (inkl. Heizungs-Check)
  - Familien-Filter-Schalter oben (Kippschalter-Optik, LED-Puls)
  - Eigenes Icon pro Kachel (handgezeichnetes Inline-SVG)
  - Kachel-Klick → Overlay mit vollem Text + „Öffnen"-Link
  - Optionaler dritter Overlay-Abschnitt „So wird es genutzt" für Tools mit
    eigener Schritt-für-Schritt-Anleitung (bisher nur der Heizungs-Check)
  - Favoriten-Funktion: Stern pro Kachel markiert einen Favoriten (immer nur
    einer aktiv), erscheint oben im großen Favoriten-Display mit Start-Button
  - Direktstart pro Kachel: „Direkt starten"-Link, der das Tool sofort öffnet,
    ohne erst die Beschreibung lesen zu müssen
  - Favorit wird lokal im Browser gespeichert (localStorage, kein Server,
    kein Tracking — gleiches Prinzip wie die Theme-Speicherung bei Skip-Bo)
  - Optik „echtes Schaltpult": Panel-Tiefe (Schraubenkopf-Punkte, Groove),
    Hover-Glow + nachzeichnende Icons, Boot-Animation beim Laden + dauerhaft
    pulsierende Status-LEDs, dezente Farbverläufe im Hintergrund
- **Code-Stand (seit v1.4.0):** Daten (TOOLS/FAMILIES/ICONS) strikt von der
  Logik getrennt; Kacheln werden EINMAL gebaut, der Filter schaltet nur
  Sichtbarkeit; alle Inhalts-Texte über textContent (robust gegen
  Sonderzeichen), nur statische SVG-Icons via innerHTML; Boot-Verzögerung
  skaliert automatisch mit der Familienanzahl. Neues Tool = ein Eintrag im
  TOOLS-Array; neue Familie = Eintrag in FAMILIES + Akzentfarbe + Icon.
- **Geplant, noch offen (zu besprechen):**
  - Weitere optische Verfeinerungen nach Bedarf — konkrete Richtung offen.

---

## 3. Notizen / offene Fragen

- Reihenfolge der Familien auf der Übersichtsseite aktuell: Lotto →
  EuroJackpot → Skip-Bo → DT-ProfiDreieck. Bislang keine Rückmeldung, dass
  das geändert werden soll.
- Keine bekannten offenen Bugs in den Einzeltools selbst (Stand dieser Notiz);
  diese Datei verfolgt nur die Übersichtsseite als aktuell aktives Projekt.
