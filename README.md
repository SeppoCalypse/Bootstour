# Bootstour

Navigationshilfe für die 4-Stunden-Tour ab Cala Figuera (`index.html`).
Eine einzelne HTML-Datei: Karte, Live-Position über das Geräte-GPS, Distanz und
Peilung zum nächsten Ziel, Umkehr-Countdown auf 17:20 Uhr.

## Datei im Browser öffnen

### Auf dem Mac, schnell zum Anschauen

1. Auf GitHub `index.html` öffnen, oben rechts auf **Raw**, dann sichern
   (`⌘S`), oder das ganze Repo über **Code → Download ZIP** laden.
2. Die Datei doppelklicken. Safari oder Chrome zeigt sie sofort an.

Karte, Zeitplan und Entscheidungspunkte funktionieren so vollständig.
Nur die Live-Position bleibt leer: Chrome gibt bei `file://`-Adressen kein GPS
frei, Safari ist unzuverlässig damit.

### Auf dem Mac, mit GPS zum Testen

Im Ordner mit der Datei:

```sh
python3 -m http.server 8000
```

Dann `http://localhost:8000/` im Browser öffnen. `localhost` gilt als sicherer
Kontext, der Standortzugriff wird also abgefragt und die Live-Anzeige läuft.

### Auf dem iPhone an Bord

Dafür braucht die Seite eine echte HTTPS-Adresse — iOS gibt den Standort sonst
nicht frei. GitHub Pages erledigt das aus diesem Repo heraus:

1. Repo → **Settings → Pages**
2. Unter *Build and deployment*: Source **Deploy from a branch**,
   Branch **main**, Ordner **/ (root)**, **Save**
3. Nach ein bis zwei Minuten liegt die Seite unter
   `https://seppocalypse.github.io/Bootstour/`
4. Auf dem iPhone in Safari öffnen, **Teilen → Zum Home-Bildschirm**. Dann
   startet sie wie eine App, ohne Adressleiste.

Zu beachten: Bei einem privaten Repo ist GitHub Pages nur mit einem
bezahlten Plan verfügbar. Auf dem kostenlosen Plan muss das Repo dafür auf
öffentlich gestellt werden (Settings → General → Change repository
visibility) — in der Datei stehen keine persönlichen Daten, nur Wegpunkte und
Zeiten.

## Version

Die Seite zeigt ihre Version oben rechts und im Fuß unter „Plan". Gepflegt wird sie an
einer einzigen Stelle in `index.html` (`const VERSION`), die Änderungen stehen in
[CHANGELOG.md](CHANGELOG.md). Zeigt das Handy eine ältere Nummer als der Changelog,
hängt der Browser im Cache und die Seite muss neu geladen werden.

## Aufbau

Zwei Modi, oben umschaltbar:

- **Fahren** — Umkehr-Countdown, Karte, Instrumente, Zielwahl
- **Plan** — Entscheidungspunkte, Zeitplan, Regeln vor Ort

Der Countdown bleibt in beiden Modi oben stehen.

### Karte im Vollbild

Der Knopf direkt unter der Karte blendet alles Übrige aus, die Karte füllt den Schirm.
Zurück geht es über den Knopf unten links oder mit Escape. Die Layer-Schalter bleiben
stehen, der Umkehr-Countdown ist im Vollbild nicht sichtbar.

Solange das Vollbild an ist, bleibt der Bildschirm wach — ohne das schaltet das Handy nach
etwa einer halben Minute ab. Beim Verlassen wird die Sperre sofort wieder freigegeben.

## Die Route

Gefahren wird an der Küste entlang und auf derselben Spur zurück:

```
Cala Figuera → Ansteuerung → Cala Santanyí → Cala Llombards → Caló des Moro → und zurück
```

Zusammen 6,1 sm, die Rückfahrt ab Caló des Moro allein 3,0 sm.

Die frühere Darstellung verband die Ziele direkt, wodurch die Rückfahrt als gerade Linie
quer über die Landzunge lief. Belegbar an den Koordinaten selbst: Cala Santanyí und Cala
Llombards liegen 111 m bzw. 53 m seewärts dieser Linie, obwohl beide Punkte der Küste
bereits vorgelagert sind.

Die Zwischenpunkte sind keine berechneten Küstenabstände, sondern die vorhandenen
Anlaufpunkte in gefahrener Reihenfolge. An der Steilküste zwischen Cala Figuera und Cala
Santanyí kürzen die Etappen daher weiterhin Land ab.

Küstendaten in brauchbarer Genauigkeit sind nicht frei verfügbar: GSHHS in Vollauflösung
liegt in diesem Ausschnitt über 200 m daneben und verortet den Wartepunkt vor Cala Figuera
im Land. Deshalb liegt die Korrektur in der Seite selbst.

### Route korrigieren

Unter **Fahren** auf **Route bearbeiten**:

- Tipp auf die Karte setzt einen Zwischenpunkt in die nächstgelegene Etappe
- Alle Punkte ziehen — auch Start, Ziel und die Anlaufpunkte. Tipp auf einen Zwischenpunkt
  bietet „löschen"
- Darunter alle Punkte mit Breite und Länge in Dezimalgrad zum genauen Eintippen
- **Sichern** legt die Route im Browser ab — sie gilt dann sofort und auch ohne Empfang
- **Koordinaten** gibt die Liste zum Weitergeben aus, **Zurücksetzen** stellt die
  eingebauten Koordinaten wieder her

Maßgeblich ist der Satellitenlayer: einmal durchzoomen, bevor es losgeht.

Auf der Karte sind drei Stufen unterschieden — Start und Ziel als dunkles Quadrat, die drei
Badebuchten als rote Kreise, Ansteuerung und Zwischenpunkte als helle Ringe.

## Was die Seite zur Laufzeit nachlädt

- Leaflet 1.9.4 von cdnjs.cloudflare.com
- Satellitenkacheln von ArcGIS World Imagery, Straßenkarte von OpenStreetMap,
  Seezeichen von OpenSeaMap

Ohne Netz bleibt die Karte also leer. Vor dem Ablegen einmal mit Empfang
öffnen und die Kacheln des Fahrgebiets durchzoomen, dann liegen sie im
Browser-Cache. Als Rückfallebene zusätzlich die Offline-Karte in Navionics
oder Apple Karten laden — das steht so auch im Zeitplan um 14:30.
