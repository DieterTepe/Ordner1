# info_1.md — Beschreibungstexte für die Programm-Übersichtsseite

> Vorlagen-Texte zum Einbinden neben den GitHub-Links. Für jedes Programm ein
> eigener Block (aktuelle Version · was es kann · was es auszeichnet · Link).
> Die Blöcke sind durch Trennlinien und mehrere Leerzeilen voneinander abgesetzt,
> damit sie sich einzeln herauskopieren lassen — der Link steht dabei immer
> als eigene Zeile unterhalb des Beschreibungstextes, nicht im Fließtext.
> Formulierungen bewusst gut lesbar und ehrlich gehalten: Die Analyse-Tools
> werten aus und unterstützen die Spielauswahl — sie sagen keine Ziehung voraus.
>
> **Stand: 11.08.2026 · passend zu Übersichtsseite v1.11.0 (17 Tools, 9 Familien)**
>
> **Reihenfolge der Blöcke = Reihenfolge der Familien auf der Übersichtsseite:**
> Lotto → EuroJackpot → Skip-Bo → DT-ProfiDreieck → DT-ProfiSchraube →
> DT-ProfiSchweissnaht → DT-ProfiPassung → Wärmeverlust-Analyse → Speicher-Studio.
>
> **Hinweis zu den Links:** Angegeben ist jeweils der *stabile GitHub-Name*, unter
> dem die Datei dort liegt (z. B. `speicher-studio_aktuell.html`). Dieter verwaltet
> die Dateien lokal versioniert unter dem richtigen Namen und benennt sie beim
> Hochladen selbst auf den stabilen Namen um, damit Verknüpfungen nicht brechen.

═══════════════════════════════════════════════════════════════════════

## Lotto 6aus49 — Analyse-Konsole
**Aktuelle Version: 2.1.0**

Eine umfassende Analyse-Konsole für die deutsche Lotterie 6aus49. Sie wertet die
komplette Ziehungshistorie seit 1955 aus und macht Muster, Häufigkeiten und
Verteilungen auf einen Blick sichtbar — übersichtlich aufgeteilt in einzelne
Auswertungs-Fenster, die man per Fingertipp öffnet.

**Was sie kann:** Häufigkeiten und „heiße/kalte" Zahlen, statistische Tests
(Chi-Quadrat, Entropie), Übergangs-Muster, sowie Verteilungen nach Wochentag,
Gerade/Ungerade, Hoch/Niedrig und Zahlensumme. Dazu zwei eigenständige
Prognose-Methoden inklusive passender Superzahl, ein Backtest, der jede Methode
gegen echte vergangene Ziehungen prüft, und eine automatische Gewichte-Optimierung.
Aus den Ergebnissen erzeugt die Konsole zwölf fertige Spielfelder und ein
Abdeck-System (Wheeling), das mehrere Tipps geschickt bündelt — alles bearbeitbar,
ausdruckbar und als PDF speicherbar.

**Was sie auszeichnet:** Ehrlichkeit. Ein eingebautes „Forschungslabor" prüft mit
echten statistischen Verfahren, ob aufeinanderfolgende Ziehungen zusammenhängen —
das Ergebnis bestätigt: Lotto ist Zufall, keine Methode schlägt auf Dauer den
Erwartungswert. Das Tool verspricht deshalb keine Gewinnzahlen, sondern grenzt
Wahrscheinlichkeiten sauber ein und zeigt mit dem Wheeling den einzigen Hebel, der
wirklich etwas bewirkt. Die Daten sind dank angebundenem Online-Archiv stets aktuell,
und die Oberfläche läuft flüssig auf Handy, Tablet und PC.

**Link:** https://dietertepe.github.io/Lotto/Lotto_2-1-0.html



═══════════════════════════════════════════════════════════════════════

## Lotto 6aus49 — Daten-Manager
**Aktuelle Version: 2.0.0**

Das Werkzeug, das die Ziehungsdaten für die 6aus49-Analyse-Konsole pflegt und sauber
hält. Schlank, robust und auf das Wesentliche konzentriert: Daten rein, Daten geprüft,
Daten gespeichert.

**Was er kann:** Die vollständige Ziehungshistorie laden, neue Ziehungen bequem über
ein Zahlenraster eingeben — mit automatischer Plausibilitätsprüfung, die Tippfehler
abfängt — sowie einzelne Einträge suchen, kontrollieren und löschen. Gespeichert wird
in einem schlanken, offenen Datenformat, das die Analyse-Konsole direkt weiterverwenden
kann.

**Was ihn auszeichnet:** Verlässlichkeit ohne Ballast. Der Manager erkennt fehlerhafte
oder unvollständige Einträge, meldet sie klar und bewahrt den Datenbestand vor
Beschädigung. Er arbeitet mit einem standardisierten, gut austauschbaren Format und
läuft — wie alle Tools dieser Reihe — vollständig im Browser auf jedem Gerät, ohne
Installation.

**Link:** https://dietertepe.github.io/Lotto/Lotto_Manager_Pro_2-0-0.html



═══════════════════════════════════════════════════════════════════════

## EuroJackpot — Analyse-Konsole
**Aktuelle Version: 1.0.1**

Die Analyse-Konsole für EuroJackpot, das europäische Lotteriespiel mit fünf
Hauptzahlen (1–50) und zwei Eurozahlen (1–12). Sie überträgt das bewährte Konzept der
6aus49-Konsole auf das doppelte Zahlensystem — und behandelt dabei die Eurozahlen als
vollwertige zweite Zahlengruppe mit eigener, ausführlicher Auswertung.

**Was sie kann:** Sämtliche Auswertungen laufen doppelt, für Haupt- und Eurozahlen:
Häufigkeiten, heiße/kalte Zahlen, statistische Tests, Übergänge, Wochentag
(Dienstag/Freitag), Gerade/Ungerade, Hoch/Niedrig und Summe. Zwei Prognose-Methoden
liefern je fünf Hauptzahlen und zwei echte Eurozahlen, ein Backtest bewertet beide
Zahlengruppen getrennt, und das Forschungslabor prüft die Unabhängigkeit der
Ziehungen. Zwölf Spielfelder werden erzeugt — jedes mit seinem eigenen Eurozahlen-Paar
— dazu ein Abdeck-System (Wheeling) und eine Druck-/PDF-Funktion.

**Was sie auszeichnet:** Epochensicherheit. Der Eurozahlen-Bereich ist über die Jahre
gewachsen (erst 1–8, dann 1–10, heute 1–12) — die Konsole rechnet das korrekt heraus,
sodass neuere Zahlen nicht fälschlich als „überfällig" erscheinen. So entsteht ein
faires, mathematisch sauberes Bild beider Zahlengruppen. Wie ihr 6aus49-Pendant bleibt
sie dabei ehrlich (sie sagt nichts voraus, sie ordnet ein) und läuft reibungslos auf
Handy, Tablet und PC.

**Link:** https://dietertepe.github.io/Eurolotto/Eurolotto_1-0-1.html



═══════════════════════════════════════════════════════════════════════

## EuroJackpot — Daten-Manager
**Aktuelle Version: 0.1.8**

Die Datenzentrale für die EuroJackpot-Analyse-Konsole. Sie hält die Ziehungshistorie
aktuell und vollständig — mit einem besonders bequemen Import direkt von der offiziellen
Quelle.

**Was er kann:** Die geprüfte Ziehungshistorie laden, neue Ziehungen über zwei
Zahlenraster eingeben (mit Validierung, die sowohl die gewachsenen Eurozahlen-Bereiche
als auch die Ziehungstage Dienstag und Freitag kennt) sowie Einträge suchen und
löschen. Der Import akzeptiert wahlweise eine **ZIP- oder eine CSV-Datei**: Die offizielle
WestLotto-ZIP wird automatisch entpackt und eingelesen — ein Entpacken von Hand
entfällt. Verschiedene Dateiformate werden dabei selbsttätig erkannt.

**Was ihn auszeichnet:** Ein Schutz, der keine Daten verlieren lässt. Beim Import werden
ausschließlich fehlende Ziehungen ergänzt, bereits vorhandene bleiben unangetastet — so
kann man die Daten gefahrlos aktualisieren, ohne den Bestand zu gefährden. Das direkte
ZIP-Einlesen gelingt ohne jede Zusatzsoftware, und der Manager läuft vollständig im
Browser auf jedem Gerät.

**Link:** https://dietertepe.github.io/Eurolotto/EuroJackpot_Manager_0-1-8.html



═══════════════════════════════════════════════════════════════════════

## Skip-Bo — Die Basisversion
**Aktuelle Version: 6.6.0**

Der Ursprung des Skip-Bo-Projekts: eine einzelne, komplett in sich geschlossene
HTML-Datei mit dem gesamten Spielcode — Spielregeln, Spielfeld und Computergegner
in nur einer Datei, ohne weitere Bauschritte. Diese Version bildet die fachliche
Grundlage, auf der die neue, modular aufgebaute Version 7.0.0 entstanden ist.

**Was sie kann:** Das vollständige Skip-Bo-Spielprinzip gegen einen Computergegner
— den eigenen Stapel zuerst leeren, indem auf den gemeinsamen Baustapeln Reihen von
1 bis 12 gelegt werden, gespeist aus Handkarten, den vier eigenen Ablagestapeln und
den Skip-Bo-Jokern (Wild-Karten). Gespielt wird kostenlos und ohne Installation direkt
im Browser, auf Handy, Tablet und PC.

**Was sie auszeichnet:** Schlichtheit als Fundament. Im Unterschied zur neuen Version
ist sie noch nicht modular aufgebaut, optisch nicht überarbeitet und nicht mit
mehreren Sprachen ausgestattet — dafür bleibt sie als einzelne, abgeschlossene Datei
unverändert spiel- und nachvollziehbar, genau so, wie das Projekt begonnen hat.

**Link:** https://dietertepe.github.io/Ordner1/SkipBo_6_6_0.html



═══════════════════════════════════════════════════════════════════════

## Skip-Bo — Das klassische Kartenspiel
**Aktuelle Version: 7.0.0**

Eine werktreue, mit viel Liebe zum Detail gestaltete Browser-Umsetzung des klassischen
Kartenspiels Skip-Bo — der direkte Nachfolger der Basisversion 6.6.0, jetzt modular
aufgebaut und optisch überarbeitet. Gespielt wird direkt im Browser gegen einen
Computergegner — kostenlos, ohne Werbung und ohne Installation, auf Handy, Tablet
und PC.

**Was es kann:** Das vollständige Skip-Bo-Spielprinzip — den eigenen Stapel zuerst
leeren, indem auf den gemeinsamen Baustapeln Reihen von 1 bis 12 gelegt werden, gespeist
aus Handkarten, den vier eigenen Ablagestapeln und den Skip-Bo-Jokern (Wild-Karten).
Gespielt wird gegen einen Computergegner. Das Kartenbild ist im Original-Look nachgebaut:
die typischen Strudel-Karten in Blau, Grün und Rot, die orange Skip-Bo-Karte und passende
Rückseiten. Dazu eine wählbare Spielgeschwindigkeit, ein eigener Spielername, vier
Sprachen (Deutsch, Englisch, Portugiesisch, Ukrainisch) und ein Design-Menü mit sechs
Hintergrund-Themen sowie Reglern für Helligkeit und Farbton — die Auswahl wird auf dem
Gerät gespeichert.

**Was es auszeichnet:** Liebe zum Detail. Von den Karten über die plastischen
Spielfeld-Rahmen bis zum animierten Ring, der den aktiven Spieler anzeigt, ist alles
darauf ausgelegt, sich wie das echte Spiel anzufühlen — aufgeräumt und hochwertig. Skip-Bo
ist persönlich anpassbar (die gewählten Hintergrund-Themen bleiben dauerhaft gespeichert)
und läuft vollständig im Browser, ganz ohne Installation. Es ist gratis und werbefrei; es
wird nichts getrackt — alle Einstellungen bleiben lokal auf dem Gerät. Impressum und
Datenschutzerklärung sind direkt eingebunden. Zu dieser Version gehört außerdem ein
eigenständiger KI-Tuner, der die Spielstärke des Computergegners verbessert (siehe
eigenen Eintrag weiter unten).

**Link:** https://dietertepe.github.io/Skipo/SkipBo_7_0_0.html



═══════════════════════════════════════════════════════════════════════

## Skip-Bo — KI-Tuner
**Aktuelle Version: 2.7 (Turbo-Update + Feinschliff 2.7b)**

Das Begleitwerkzeug zur Skip-Bo-Version 7.0.0: ein eigenständiges Browser-Tool, das die
Score-Parameter des Computergegners per genetischer Optimierung verbessert, statt sie von
Hand zu justieren. Tuner und Spiel teilen sich exakt dieselbe Spiel-Engine, damit die
gefundenen Werte 1:1 übertragbar sind.

**Was er kann:** In zwei Phasen — erst breite Erkundung, dann Feinschliff — lässt der
Tuner tausende simulierte Partien gegen einen Spiegel-Gegner mit identischer Engine laufen,
gepaart in Mirror-Paaren, damit sich Kartenglück gegenseitig aufhebt, und beschleunigt
durch Mehrkern-Web-Worker. Eine vorgeschaltete „Turbo-Sieb"-Vorrunde mit einem Drittel-Deck
sortiert schwache Kandidaten schon früh aus. Am Ende steht ein fertiger `KONFIG`-Block zum
direkten Einfügen ins Spiel, ergänzt durch ein Empfehlungs-Panel mit Schiebereglern, das
zeigt, welche Werte den größten Einfluss auf die Spielstärke haben.

**Was ihn auszeichnet:** Der Selbstoptimierungs-Kreislauf — das Ergebnis eines Laufs lässt
sich per Konverter wieder in den Startpunkt des nächsten Laufs zurückverwandeln, sodass
jeder Tuning-Durchgang auf dem vorherigen aufbaut. Eine automatische Suchraum-Dehnung
erkennt, wenn die Optimierung an ihre eigenen Wertegrenzen stößt, und erweitert sie
selbsttätig, statt das Ergebnis künstlich zu begrenzen. Wie das Spiel läuft auch der Tuner
vollständig im Browser, ohne Installation oder Cloud-Anbindung.

**Link:** https://dietertepe.github.io/SkipBo_Tuner/SkipBo_Tuner_v2_7.html



═══════════════════════════════════════════════════════════════════════

## DT-ProfiDreieck — Profi-Dreiecksrechner für Werkstatt & CNC
**Aktuelle Version: Test 1.1.0 & Pro 1.1.0 (Engine 3.0.0)**

> Auf der Übersichtsseite in zwei Kacheln geteilt: **Testversion** (kostenlos,
> alle Standardfälle, freier Export) und **Pro-Version** (zusätzlich die
> Spezialfälle Umkreis/Inkreis/Fläche/Höhen, Lizenz-Wasserzeichen).

Ein Werkstatt-Werkzeug, das aus beliebigen bekannten Dreiecksgrößen (Seiten,
Winkel, Umkreis-/Inkreisradius, Fläche, Höhen) das vollständige Dreieck löst und
direkt als fertige CAD-Zeichnung ausgibt. **Hauptaufgabe des Projekts:** die
hauseigene Dreiecksberechnung (Engine 3.0.0) als zwei eigenständige, einmalig
verkaufte Produkte zu vermarkten — eine kostenlose **Testversion** als Köder und
eine kostenpflichtige **Pro-Version** (69 €, einmalig, über Digistore24) für
CNC-, Metallbau- und Tischlerei-Profis. Beide laufen als einzelne HTML-Datei,
offline und ohne Installation, auf Handy, Tablet und PC.

**Was es kann:** Alle gängigen Eingabefälle (SSS, SWS, WSW, SWW, SSW) sowie die
fortgeschrittenen Spezialfälle mit Umkreis, Inkreis, Fläche oder Höhen — inklusive
numerischer Lösungen mit Plausibilitätsprüfung (z. B. Euler-Ungleichung R≥2r).
Jedes Ergebnis kommt mit vollständigem, nachvollziehbarem Rechenweg sowie einer
maßstäblichen CAD-Zeichnung. Export als PNG, SVG, PDF und — als Alleinstellung —
direkt verwertbares **DXF** für die CNC-Maschine. Die Testversion rechnet alle
Standardfälle und exportiert frei; die Pro-Version schaltet zusätzlich die
Spezial-Eingabefälle (R/r/Fläche/Höhen) frei und trägt ein persönliches
Lizenz-Wasserzeichen (Name + Digistore24-Lizenzschlüssel).

**Was es auszeichnet:** Ehrlichkeit und Nachvollziehbarkeit — der Rechenweg wird
unabhängig vom eigentlichen Lösungsprozess neu berechnet, damit jede angezeigte
Formel sich selbst bestätigt. Die Spezialfälle (Umkreis/Inkreis/Fläche/Höhe als
Eingabe) sind der eigentliche Burggraben, den kaum ein anderes frei verfügbares
Tool abdeckt. Dazu kommt der direkte DXF-Export, der die Geometrie ohne Umwege an
die Werkstatt-Maschine bringt. Beide Versionen laufen als einzelne, offline
funktionierende Datei ohne Cloud-Anbindung und ohne laufende Kosten — einmal
kaufen, dauerhaft nutzen. Vertrieb und Auslieferung laufen automatisiert über
Digistore24, die Landingpage unter dt-profidreieck.de ist DSGVO-konform ohne
externe Ressourcen.

**Link (Testversion):** https://www.dt-profidreieck.de/
**Link (Pro-Version):** https://dietertepe.github.io/Ordner1/DT-ProfiDreieck_Pro_1-1-0.html



═══════════════════════════════════════════════════════════════════════

## DT-ProfiSchraube — Schraubenauslegung nach VDI 2230 Blatt 1
**Aktuelle Version: Testversion & Vollversion 4.9.5**

Ein Werkstatt-/Ingenieur-Werkzeug, das Schraubenverbindungen nach der Richtlinie
VDI 2230 Blatt 1 auslegt — nachvollziehbar von der Klemmkraft bis zur
Einschraubtiefe. Läuft als einzelne HTML-Datei, offline und ohne Installation,
auf Handy, Tablet und PC. Auf der Übersichtsseite in zwei Kacheln geteilt:
**Testversion** (rechnet alles, aber ohne Export/Laden/Speichern) und
**Vollversion** (mit Export, Laden und Speichern).

**Was es kann:** Die komplette Schraubenauslegung nach VDI 2230 Blatt 1: von der
Klemmkraft bis zur Einschraubtiefe fünf Sicherheits-Nachweise mit
Ampel-Bewertung. Jeder Rechenschritt ist dokumentiert — mit Formel, eingesetzten
Werten und Normverweis, also vollständig nachvollziehbar. Die Testversion rechnet
alles vollständig durch; die Vollversion schaltet zusätzlich Export sowie Laden
und Speichern von Berechnungen frei, sodass sich Auslegungen sichern und
weitergeben lassen.

**Was es auszeichnet:** Nachvollziehbarkeit statt Blackbox — jeder der fünf
Nachweise wird mit Formel, Zahlenwerten und Verweis auf die Norm gezeigt und per
Ampel (grün/gelb/rot) bewertet. So sieht man nicht nur das Ergebnis, sondern auch
den Weg dorthin. Läuft vollständig im Browser, ohne Installation, auf Handy,
Tablet und PC.

**Link (Testversion):** https://dietertepe.github.io/dt-profischraube-web/DT-ProfiSchraube_Test.html
**Link (Vollversion):** https://dietertepe.github.io/dt-profischraube-web/DT-ProfiSchraube-4-9-5.html



═══════════════════════════════════════════════════════════════════════
## DT-ProfiSchweissnaht — Schweißnahtberechnung mit vollem Rechenweg
**Aktuelle Version: Testversion & Vollversion (öffentliche Nummer noch offen;
interner Programmstand N12 / Plan 2.70, Stand der Werbe-Grundlage 07.08.2026)**

> Auf der Übersichtsseite als eigene Familie mit zwei Kacheln, direkt nach
> DT-ProfiSchraube: **Testversion** (rechnet alles vollständig, gesperrt sind nur
> die Ausgaben) und **Vollversion** (mit Drucken/PDF, Word und eigenem
> Speicherformat). Vertrieb und Updates über Digistore24. Das Programm selbst ist
> dreisprachig (DE/EN/PT).

Rechnet Schweißnähte im Stahlbau nach EN 1993-1-8 und im klassischen Maschinenbau
— und zeigt dabei jeden einzelnen Schritt: vom Nahtbild über Schwerpunkt,
Flächenmomente und Hauptachsen bis zur Vergleichsspannung am maßgebenden Punkt.
Kein Nachweis ohne Rechenweg, keine Zahl ohne Quelle. Läuft im Browser, ohne
Installation, ohne Internet und ohne dass eine Eingabe das Gerät verlässt.

**Was es kann:** Bemessung nach EN 1993-1-8 (richtungsbezogenes und vereinfachtes
Verfahren), nichtrostende Stähle nach EN 1993-1-4, Aluminium nach EN 1999-1-1 und
klassischer Maschinenbau nach Roloff/Matek und Decker — getrennt gehalten, nie
vermischt. Zwei Rechenrichtungen: Nachweis (a-Maß gegeben, Ausnutzung gesucht)
und Auslegung (erforderliches a-Maß gesucht). Kehl- und Stumpfnaht, umlaufend
oder abschnittsweise, an Profilen von Blech und Flachstahl über Winkel, U und I
bis Rohr und Rechteckrohr; ausgewählt wird, welche Kanten wirklich geschweißt
sind, samt Endkraterabzug, Mindest- und Höchst-a-Maß und wirksamer Nahtlänge.
Lasten N, Q_y, Q_z, M_y, M_z und T, direkt oder aus Kraft und Hebelarm; Beiwerte
(γ_M2, β_w, Sicherheitsbeiwert, Nahtgütefaktor) je Tabellenwert überschreibbar mit
sichtbarer Kennzeichnung. Dazu Wärmeführung und Vorwärmung nach EN 1011-2
(Methode B) als eigene Rechnung — CET, CEV, Pcm, kombinierte Dicke,
Wärmeeinbringen, Mindest-Vorwärmtemperatur und Abkühlzeit t8/5 mit Zielfenster —
sowie Kosten, Zeit und Drahtbedarf und Zeichnungssymbole nach EN ISO 2553.

**Was es auszeichnet:** Gerechnet wird mit dem echten Nahtbild statt mit einer
angesetzten Nahtlänge: aus Profil und geschweißten Kanten entstehen Segmente,
Schwerpunkt, Flächenmomente I_y, I_z und I_yz, polares Flächenmoment,
Hauptachsen und Widerstandsmomente, daraus wird der maßgebende Punkt gesucht;
unsymmetrische Nahtbilder werden mit allgemeiner schiefer Biegung gerechnet, nicht
genähert. Über dreißig Rechenschritte nennen Formel, eingesetzte Zahlen, Ergebnis
und Quelle — Norm, Fachbuch oder ausdrücklich ein Praxisrichtwert ohne normative
Regelung. Neunzehn Rechenproben laufen bei jeder Berechnung mit (etwa: sind die
statischen Momente um den Schwerpunkt null, ergibt I_p wirklich I_y + I_z); ein
fehlendes Häkchen bedeutet einen Rechenfehler im Programm und wird getrennt von
einem nicht erfüllten Nachweis ausgewiesen. Jede Ausgabe trägt zudem eine Liste
von dreizehn Punkten, die das Programm bewusst nicht prüft — nicht im
Kleingedruckten, sondern im Nachweis selbst.

**Unterschied Test / Vollversion:** Die Testversion rechnet alles vollständig, mit
dem kompletten Rechenweg am Bildschirm; gesperrt sind ausschließlich die Ausgaben
— Speichern, Öffnen, Drucken und Word. Die Vollversion schaltet diese frei:
Drucken und PDF mit vollständigem Rechenweg, Nahtbild und Lückenliste, Word (.rtf)
mit eingebettetem Nahtbild sowie ein eigenes Dateiformat (.dts) zum Speichern und
Weiterarbeiten — es sichert die Eingaben und nicht die Ergebnisse, damit darin
keine Zahl veralten kann.

**Ehrliche Einordnung (Vorgabe aus Werbung.md):** Das Programm ersetzt nicht den
Fachingenieur. Die fachliche Verantwortung für Lastannahmen, Werkstoffwahl,
Ausführung und Abnahme bleibt beim Anwender; jedes Ergebnis ist gegen die
Originalnormen und die eigene Abnahme zu prüfen. Der Nachweis ist vollständig für
die Naht, nicht für das Bauteil. **Nicht bewerben:** Ermüdungsnachweis und
Verzug/Schrumpfung (folgen in einem späteren, kostenpflichtigen Update) sowie die
Wörter normkonform, normgerecht, geprüft, zertifiziert oder zugelassen.

**Link (Testversion):** https://dietertepe.github.io/dt-profischweissnaht-web/DT-ProfiSchweissnaht_Testversion.html
**Link (Vollversion):** https://dietertepe.github.io/dt-profischweissnaht-web/DT-ProfiSchweissnaht_Vollversion.html


═══════════════════════════════════════════════════════════════════════

## DT-ProfiPassung — Toleranz- und Passungsrechner nach ISO 286
**Aktuelle Version: Testversion & Vollversion (öffentliche Nummer noch offen —
wird laut Werbe-Grundlage kurz vor Verkauf gesetzt)**

> Auf der Übersichtsseite als eigene Familie mit zwei Kacheln: **Testversion**
> (voller Rechenumfang, aber ohne Speichern/Laden, Word-Bericht/Druck, Export)
> und **Vollversion** (mit Speichern, Word-Bericht .rtf, Druck und Export).
> Vertrieb geplant über Digistore24, Einmalkauf. Das Programm selbst ist
> dreisprachig (DE/EN/PT). Farbkonvention der App: Bohrung = Grün, Welle = Blau.

Ein interaktiver Toleranz- und Passungsrechner nach ISO 286 — mit Pressverband
(DIN 7190), Allgemeintoleranzen (ISO 2768), Thermik und einem geführten
Passungs-Assistenten. Komplett offline im Browser, auf dem Handy ebenso bedienbar
wie am Rechner.

**Was es kann:** Rechnet Passungen nach ISO 286 (obere/untere Abmaße, Höchst- und
Mindestmaß, Spiel bzw. Übermaß, Passtoleranz) als Einheitsbohrung oder
Einheitswelle, per Auswahl oder Schnelleingabe wie „Ø50 H7/g6". Dazu
Toleranzfeld-Schaubild, Allgemeintoleranzen nach ISO 2768, Pressverband nach
DIN 7190 (Fugendruck, zulässige Drücke, Sicherheiten, übertragbares Moment/Kraft,
Fügetemperatur inkl. Werkstoffkennwerten und Reibwerttabelle), Thermik
(Passungsänderung bei Temperatur) und ein geführter Passungs-Assistent. Zu jeder
Berechnung gibt es einen aufklappbaren, selbstprüfenden Rechenweg (Formel,
eingesetzte Werte, Häkchen je Schritt). Die Testversion hat den vollen
Rechenumfang; Speichern/Laden, Word-Bericht (.rtf)/Druck und Kopieren/Export sind
der Vollversion vorbehalten.

**Was es auszeichnet:** Der selbstprüfende Rechenweg macht sichtbar, wie ein
Ergebnis zustande kommt, nicht nur was herauskommt — das schafft Vertrauen in
Konstruktion, Fertigung, QS und Ausbildung. Jedes Eingabefeld hat ein
antippbares ⓘ mit einfacher Erklärung, Bereich und Empfehlung: für Profis ein
Beschleuniger, für Einsteiger und Ausbildung ein Lehrmittel. Läuft 100 % offline
(kein Konto, keine Cloud, keine Datenübertragung), von Grund auf fürs Handy
gebaut. Ehrlicher Hinweis auch in der App-Fußzeile: „Berechnung ohne Gewähr — vor
Produktivnutzung gegen die Originalnorm prüfen." Normbezug transparent (ISO 286-2,
DIN 7190-1, ISO 2768-1), Ergebnisse mit Rechenweg belegt.

**Link (Testversion):** https://dietertepe.github.io/dt-profipassung-web/DT-ProfiPassung_Testversion.html
**Link (Vollversion):** https://dietertepe.github.io/dt-profipassung-web/DT-ProfiPassung_Vollversion.html
═══════════════════════════════════════════════════════════════════════

## Wärmeverlust- & Gebäude-Analyse — Heizungs-Check fürs eigene Zuhause
**Aktuelle Version: 1.0**

Ein persönliches Analyse-Werkzeug, das anhand realer Temperatur- und Durchflussmessungen
zeigt, wie gut ein Haus gedämmt ist und wie effizient die Heizungsanlage arbeitet. Anders
als die übrigen Tools dieser Übersicht ist es kein eigenständig veröffentlichtes Projekt,
sondern für eine konkrete eigene Heizungsanlage gebaut — mit mehreren Heizkreisen
(Fußbodenheizung, Heizkörper, Warmwasser-Puffer) und einem manuell bedienten Mischer.

**Was es kann:** Aus einer Messreihe berechnet die Konsole den UA-Wert
(Wärmeverlust-Koeffizient) des Gebäudes und ordnet das Ergebnis einer
Energieeffizienzklasse (A+ bis H) zu. Dazu kommen Normheizlast und eine Jahresprognose
über die Heizgradtage-Methode, abgestimmt auf elf deutsche Klimaregionen oder eine frei
definierbare. Nutzungsprofile für Lüftungsverhalten und Sonneneinstrahlung fließen als
Korrekturfaktoren mit ein. Ein Szenario-Rechner („Was wäre, wenn?") zeigt für jede
gewünschte Innen-/Außentemperatur die nötige Vorlauftemperatur, die passende
Mischer-Stellung, den Durchfluss und die zu erwartenden Tageskosten — ergänzt durch eine
vollständige Heizkurven-Tabelle von −15 °C bis +15 °C mit Vorlauf, Rücklauf, Spreizung,
Durchfluss, Mischer-Stufe und Kosten pro Tag. Bei mehreren Messpunkten mit
unterschiedlichen Mischerstellungen kalibriert sich die Mischer-Skala automatisch und
zunehmend genauer, inklusive Plausibilitäts-Hinweis bei stark abweichenden Werten.
Optional lässt sich zusätzlich der Leitungsverlust zwischen Kessel und
Heizkreis-Verteiler berechnen, sobald Kessel-Temperaturen vorliegen.

**So wird es genutzt:**
1. Messwerte eintragen — Außentemperatur, Innentemperatur, Vor- und Rücklauf am
   Verteiler sowie der Durchfluss; optional ergänzt um Kessel-Vor-/Rücklauf und die
   aktuelle Mischer-Stufe
2. Auf „Messreihe & Gebäude auswerten" klicken — die Konsole berechnet daraus UA-Wert,
   Effizienzklasse und Jahresprognose
3. Im Szenario-Rechner eine Wunsch-Innentemperatur und eine Außentemperatur eingeben,
   um die passende Mischereinstellung und die Tageskosten für genau diese Situation zu
   sehen
4. Die Heizkurven-Tabelle durchsehen, um die optimale Mischerstellung für verschiedene
   Außentemperaturen abzulesen
5. Bei wiederholten Messungen mit unterschiedlichen Mischerstellungen wird die
   Mischer-Skala mit jedem weiteren Messpunkt präziser

**Was es auszeichnet:** Die Mischer-Kalibrierung lernt direkt aus der eigenen Anlage
statt aus theoretischen Annahmen — je mehr Messpunkte mit unterschiedlicher
Mischerstellung vorliegen, desto genauer wird die Empfehlung. Komma oder Punkt als
Dezimaltrennzeichen, alle Eingaben werden automatisch lokal im Browser gespeichert,
keine Cloud-Anbindung, keine Installation nötig.

**Link:** https://dietertepe.github.io/Heizungsanlage/waermeverlust.html



═══════════════════════════════════════════════════════════════════════

## Speicher-Studio — Browser-Speicher einsehen und verwalten
**Aktuelle Version: (noch keine Nummer vergeben — Dateiname „…_aktuell")**

Ein Werkzeug, das den lokalen Browser-Speicher sichtbar und bearbeitbar macht.
Speicher-Studio ist eine einzelne HTML-Datei, die komplett offline auf PC, Handy
und Tablet läuft. Sie zeigt die Konfigurationen, die Web-Programme lokal im
Browser ablegen (localStorage und sessionStorage), macht sie als Text lesbar und
lässt sie bearbeiten, überschreiben und gezielt löschen — einzeln, gruppenweise
oder komplett.

**Was es kann:** Macht sichtbar, was Web-Programme im Browser ablegen
(localStorage und sessionStorage): alle Einträge übersichtlich, automatisch nach
Programm gruppiert, mit Suche und JSON-Formatierung samt Gültigkeitsprüfung.
Einträge lassen sich bearbeiten, neu anlegen, überschreiben und gezielt löschen —
einzeln, gruppenweise oder komplett, jeweils mit Sicherheitsabfrage. Ganze
Konfigurationen können als JSON-Datei gesichert und wieder geladen werden, um sie
zu übertragen — etwa zwischen Chrome und Edge, die getrennte Speicher haben.

**Was es auszeichnet:** Das Besondere ist die „Brücke": zwei Lesezeichen-
Werkzeuge (Bookmarklets), mit denen sich Daten aus anderen Tabs oder echten
Websites erfassen und nach dem Bearbeiten wieder zurückschreiben lassen — über
Tab-, Website- und Browsergrenzen hinweg. So wird aus einem reinen Betrachter ein
Werkzeug, das Konfigurationen dorthin bringt, wo man sie braucht. Läuft als
einzelne, offline funktionierende Datei auf PC, Handy und Tablet.

**Link:** https://dietertepe.github.io/Ordner1/speicher-studio_aktuell.html


═══════════════════════════════════════════════════════════════════════
