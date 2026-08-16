# Changelog

Format nach [Keep a Changelog](https://keepachangelog.com/de/1.1.0/),
Versionierung nach [Semantic Versioning](https://semver.org/lang/de/).

Die angezeigte Version steht oben rechts auf der Seite und im Fuß unter „Plan".
Steht dort eine ältere Nummer als hier, zeigt der Browser eine zwischengespeicherte
Fassung — Seite neu laden.

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
