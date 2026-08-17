# Changelog

Format nach [Keep a Changelog](https://keepachangelog.com/de/1.1.0/),
Versionierung nach [Semantic Versioning](https://semver.org/lang/de/).

Die angezeigte Version steht oben rechts auf der Seite und im Fuß unter „Plan".
Steht dort eine ältere Nummer als hier, zeigt der Browser eine zwischengespeicherte
Fassung — Seite neu laden.

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
