# Changelog

Format nach [Keep a Changelog](https://keepachangelog.com/de/1.1.0/),
Versionierung nach [Semantic Versioning](https://semver.org/lang/de/).

Die angezeigte Version steht oben rechts auf der Seite und im Fuß unter „Plan".
Steht dort eine ältere Nummer als hier, zeigt der Browser eine zwischengespeicherte
Fassung — Seite neu laden.

## [1.4] – 2026-08-17

Zwei Geräte hatten zwei Routen und jedes sah nur seine eigene. `localStorage` gehört dem
einzelnen Browser auf dem einzelnen Gerät — es gab bisher keine Stelle für eine gemeinsame
Fassung. In normalem Safari löscht ITP diese Ablage zudem nach sieben Tagen ohne
Interaktion; vom Home-Bildschirm gestartete Apps haben einen eigenen Zähler.

### Hinzugefügt
- **`route.json`** als gemeinsame Route. Die Seite holt sie beim Laden — jedes Gerät sieht
  damit dieselbe. Geändert wird die Datei im Repo, das geht auf github.com auch vom Handy.
- **Route laden** — Knopf, der die gemeinsame Fassung neu holt, ohne die Seite neu zu
  starten. So kommt man an die Änderung des anderen Geräts.
- **Route teilen** — erzeugt einen Link, in dem die Route steckt. Wo das Gerät es kennt,
  öffnet sich das Teilen-Blatt, sonst steht der Link zum Kopieren im Feld. Die Route liegt
  im Anker der Adresse und geht damit an keinen Server.
- **Hinweisleiste** über der Karte: fragt vor dem Übernehmen einer fremden Route und nennt
  die Punktzahl, dient sonst als kurze Rückmeldung.
- Die zuletzt geholte gemeinsame Route wird zwischengespeichert, damit ein Start ohne
  Empfang nicht auf die eingebauten Werte zurückfällt.

### Geändert
- „Koordinaten" heißt jetzt **„Für route.json"** und gibt das vollständige Dokument samt
  frischer Marke aus — kopieren, im Repo einsetzen, fertig.
- Vorrang beim Start: eigene Bearbeitung, sonst zuletzt geholte gemeinsame, sonst
  eingebaute Route. Eine neuere gemeinsame Fassung wird angeboten, nie aufgezwungen.
  Einmal verworfen wird nicht bei jedem Neustart erneut gefragt — beim Laden von Hand schon.
- Speicherformat `v3` mit `basis`, der Marke, auf der die eigene Bearbeitung beruht.
  Stände aus `v1` und `v2` laden weiterhin.

## [1.3] – 2026-08-17

### Hinzugefügt
- **Karte im Vollbild.** Knopf direkt unter der Karte, zurück über den Knopf unten links,
  über Escape oder über das Beenden des Browser-Vollbilds. Die Karte wächst dabei von
  46 % der Höhe auf das ganze Fenster.
- Der Bildschirm bleibt im Vollbild wach (Wake Lock) und wird beim Verlassen sofort wieder
  freigegeben. Nach einem Wechsel in eine andere App wird die Sperre neu angefordert.

### Umsetzung
- Das Vollbild läuft über eine Klasse am `<body>`, nicht über die Fullscreen-API. Die fehlte
  auf dem iPhone für gewöhnliche Elemente jahrelang, kam erst mit iOS 17.4 und steckte
  zunächst hinter einem Schalter in den Safari-Einstellungen. Vom Home-Bildschirm aus hätte
  sie ohnehin nichts mehr zu verbergen. Zusätzlich wird sie gerufen, wo der Browser sie
  kennt — dann verschwinden am Rechner und auf Android auch Adressleiste und Tabs.
- Sichtbar bleibt allein die Karte samt ihrer eigenen Schalter für Satellit, Karte,
  Seezeichen und Folgen. Der Umkehr-Countdown ist im Vollbild nicht zu sehen; der
  Zurück-Knopf ist deshalb dauerhaft eingeblendet.
- Kerbe und Home-Indikator werden über `env(safe-area-inset-*)` freigehalten.

### Behoben
- `setModus()` setzte `body.className` und hätte damit den Vollbild-Zustand weggewischt;
  die Funktion arbeitet jetzt mit `classList`.

## [1.2] – 2026-08-17

### Hinzugefügt
- **Alle Punkte sind verschiebbar**, nicht mehr nur die Zwischenpunkte. Start, Ziel und die
  Anlaufpunkte lassen sich ziehen und werden mitgespeichert. Grund: Der Start- und Zielpunkt
  in Cala Figuera stammt aus der ursprünglichen Datei und sitzt an der falschen Stelle.
- **Zahleneingabe** im Bearbeitungsmodus: Liste aller Punkte mit Breite und Länge in
  Dezimalgrad, Schrittweite 0,0001 (etwa 11 m). Unbrauchbare Eingaben werden verworfen,
  der alte Wert bleibt stehen.
- **Drei Symbolstufen auf der Karte**: Start und Ziel als dunkles Quadrat mit Beschriftung,
  die drei Badebuchten als rote Kreise, Ansteuerung und Zwischenpunkte als helle Ringe.

### Geändert
- Wegpunkt-Marker sind `L.marker` statt `L.circleMarker`, weil nur Marker ziehen können.
- Verschobene Punkte schlagen auf Zielliste, Kartenpopup und Zahlenfelder durch.
- Speicherformat `v2` mit Koordinaten auch bei den benannten Punkten. Ein `v1`-Stand aus
  Version 1.1 wird weiter gelesen, seine Wegpunkte behalten die eingebauten Werte.

## [1.1] – 2026-08-17

### Hinzugefügt
- **Route bearbeiten.** Ein Tipp auf die Karte setzt einen Zwischenpunkt in die
  nächstgelegene Etappe, Punkte lassen sich ziehen und löschen. Gesichert wird im Browser,
  die korrigierte Route gilt damit sofort und auch ohne Empfang. „Koordinaten" gibt die
  Liste zum Weitergeben aus, „Zurücksetzen" stellt die eingebaute Route wieder her.
  Die fünf benannten Wegpunkte bleiben dabei fest.
- **Bild je Ziel** in der Zielliste, zugeklappt. Fotos von Wikimedia Commons mit
  Quellenangabe und Link auf Autor und Lizenz. Zugeklappt wird nichts geladen.

### Bekannte Einschränkung
- Die eingebauten Etappen kürzen an der Steilküste zwischen Cala Figuera und Cala Santanyí
  weiterhin Land ab. Küstendaten in brauchbarer Genauigkeit sind nicht frei verfügbar —
  GSHHS in Vollauflösung liegt hier über 200 m daneben und verortet den Wartepunkt
  `fig_out` im Land. Deshalb der Bearbeitungsmodus: Das Satellitenbild vor Ort ist die
  einzige verlässliche Quelle.
- Die Bilddateinamen sind recherchiert, aber nicht gegengeprüft. Lädt ein Bild nicht,
  erscheint an seiner Stelle der Link zur Quelle.

## [1.0] – 2026-08-16

Erster versionierter Stand. Die Seite bekommt eine eigene Gestalt, getrennt von der
Bauart der übrigen Projekte, und trennt Fahrbetrieb von Nachschlagematerial.

### Hinzugefügt
- Zwei Modi, umschaltbar im Kopf: **Fahren** (Karte, Instrumente, Zielwahl) und
  **Plan** (Entscheidungspunkte, Zeitplan, Regeln). Die Wahl übersteht einen Reload.
- Peilung zusätzlich als gezeichneter Zeiger mit Nordmarke.
- Kursabweichung „17° nach steuerbord", sobald das GPS bei über 1 kn Fahrt eine
  Richtung liefert.
- Versionsanzeige im Kopf und im Fuß, gepflegt an einer Stelle im Skript.
- Diese Datei.

### Geändert
- Umkehr-Countdown bleibt beim Scrollen oben stehen, statt aus dem Bild zu laufen.
- Instrumente neu gewichtet: Reststrecke dominant, Knoten und Ankunft daneben.
- Layerschalter sitzen als Chips auf der Karte statt in einer eigenen Leiste.
- Palette von warmem Papierbeige auf kühles Papierweiß mit Seekarten-Signalen.
- Alle Schaltflächen auf mindestens 44 px Höhe, Sekundärtext auf mindestens 12 px.
- Versalien nur noch für Sektionstitel.

## Vor der Versionierung

- Route folgt der Küste und fährt auf derselben Spur zurück, statt vom Caló des Moro
  quer über die Landzunge abzukürzen. Distanz und Peilung folgen dieser Route.
- Seite als `index.html` für GitHub Pages, Anleitung zum Öffnen im README.
