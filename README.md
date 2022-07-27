# GeoVisAR
Visualization of Geodata with WebAR

## Einführung
Dieses Repository bietet eine Grundlage um GeoDaten mit WebAR im Browser darzustellen.

Es soll die Möglichkeit bieten ohne tiefgreifende Programmierkenntnisse eigene Anwendungen im Internet bereitzustellen, z.B. für GeoCaching oder Schnitzeljagden.

Die Nutzerinnen und Nutzer müssen dann keine eigene App herunterladen sondern benötigen nur den Link bzw. den QR-Code zur Seite und ihr Smartphone.

GeoVisAR ist im Rahmen eines Studierendenprojekts an der FOM Hochschule für Oekonomie & Management Hochschulzentrum München entstanden.

Für das sichere und kostenlose Hosting der Websiten wird [GitHub Pages](https://pages.github.com/) verwendet.
## Bereitstellung eigener Anwendungen

1. Fork des Repositorys in den eigenen GitHub Account (Button rechts oben)
2. Anpassen des Forks:
    - In Datei [_config.yml](_config.yml) die Variablen `title`, `email`, `description`, `baseurl`, `url`, `github_username` an das eigene Projekt anpassen
    - In Datei [index.markdown](index.markdown) die Texte an das eigene Projekt anpassen, QR-Code wird automatisch generiert
        - es können eigene Beispielbilder verlinkt werden, diese unter [assets](assets/) ablegen und analog dem Beispiel verlinken
    - In Datei [hints.markdown](hints.markdown) die Texte an das eigene Projekt anpassen, Tabelle und Karte wird automatisch generiert
    - In Datei [about.markdown](about.markdown) die Texte an das eigene Projekt anpassen
3. Anlegen der eigenen GeoDaten:
    - Die GeoDaten werden in der Datei [geodata.json](assets/geodata.json) angelegt.
    - Für jeden Marker gibt es einen Datensatz im JSON-Format in der Liste `data` mit folgenden Feldern:
        - `id` => String (Zeichenkette) zur Identifizierung
        - `text` => String (Zeichenkette) die den Marker beschreibt (für Hilfeseite)
        - `type` => Form des Markers, Wahl zwischen:
            - `box` => Würfel
            - `sphere` => Kugel
            - `cone` => spitzer Zylinder
            - `gltf-model` => 3D-Modell im GLTF-Format
        - `model` => nur für GLTF-Modelle, mitgeliefert wird "#arrow"
        - `color` => Farbe des Markers (z.B. "red", "green", "blue"), leer lassen für 3D-Modelle
        - `scale` => Skalierung des Markers, Standard ist 10, für 3D-Modelle ggf. anpassen
        - `lat` => Breitengrad/Latitude des Markers (z.B. aus Google Maps) mit Punkt . als Dezimalzeichen und ohne Anführungszeichen
        - `lon` => Längengrad/Longitude des Markers (z.B. aus Google Maps) mit Punkt . als Dezimalzeichen und ohne Anführungszeichen
    - falls eigene 3D-Modelle verwendet werden müssen diese wie folgt angelegt werden:
        - Ablage im Ordner [assets](assets/)
        - Einbinden in der Datei [app.html](app.html) im HTML-Tag `a-assets` analog dem Beispiel "arrow"
4. Hosten mit GitHub Pages
    - Im GitHub Repository auf "Settings"
    - Anschließend links auf "Pages" unter Source folgende Einstellungen vornehmen:
        - Branch: main
        - Folder: /(root)
    - Die Seite wird dann erstellt (kann einige Minuten dauern) und ist dann unter dem unter dem angegebenen Link öffentlich zugänglich und nutzbar

## Bekannte Einschränkungen

- Das dem AR-Teil zugrunde liegende AR.js Projekt unterstützt derzeit (07/2022) **keine Apple/iOS-Geräte**.
- Das Einblenden von Text oder Anklicken/Antouchen von Marker funktioniert derzeit nicht.

## Verwendete Libraries / Projekte:
- [AR.js](https://github.com/AR-js-org/AR.js)
- [Jekyll](https://github.com/jekyll/jekyll)
- [Jekyll Minima Theme](https://github.com/jekyll/minima)
- [QRCode.js](https://github.com/davidshimjs/qrcodejs)
- [Leaflet](https://github.com/Leaflet/Leaflet)
- [Leaflet.IconMaterial](https://github.com/ilyankou/Leaflet.IconMaterial)